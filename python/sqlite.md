---
description: 紀錄自己在使用 SQLite 的程式碼片段，基本上一個專案只會打一次，所以常常忘記。
---

# sqlite 設定資料庫

我記得以 `with` 的方式進行資料庫操作是在某本書看到的，但忘記書名是什麼了... 是利用 Python `with` 的特性省略每次要**連線**資料庫與**關閉**的程式碼。

```python
    with class_name: # 會先執行 class `__enter__ ` 這個 magic method
        ...

    # 離開區塊時會執行 `__exit__`
```

因此利用這個特性，將**連線**資料庫的程式碼寫在 `__enter__` 內，**關閉**資料庫的部份則是寫在 `__exit__` 內，可以確保每次都會確實關閉資料庫。

## sqlite3

```python
import sqlite3

class DBHandler(object):
    def __init__(self):
        self.db_name = f"{database_path}"

    def __enter__(self):
        self.start_database()
        return self

    def __exit__(self, exc_type, ex_value, ex_traceback):
        self.close_database()

    def start_database(self):
        self.conn = sqlite3.connect(self.db_name)
        self.cur = self.conn.cursor()

    def close_database(self):
        """shut down connect to DB
        """
        self.conn.close()

class MainDB(object):  
    def __init__(self):
        self.db = DBHandler()
        self.table_name = "table_name"

    def _execute(self, sql):
        with self.db:

            self.db.cur.execute(sql)
            self.db.conn.commit()

    def _fetch(self, sql):
        with self.db:
            self.db.cur.execute(sql)
            rows = self.db.cur.fetchall()

        return rows

    def create_table(self):
        with self.db:
            sql = f"""
                    CREATE TABLE IF NOT EXISTS {self.table_name} (
                    id integer PRIMARY KEY,
                    name string(8) NOT NULL,
                    datetime datetime DEFAULT (datetime('now', 'localtime')), /*(Date())*/
                    number integer DEFAULT 0,
                    execution BOOLEAN NOT NULL DEFAULT 0

                );
                """

            self.db.cur.execute(sql)

    def read(self):
        sql = f"""
            SELECT * FROM {self.table_name}
        """

        sql = f"""
            SELECT name FROM {self.table_name}
            WHERE id='5'
        """

        return self._fetch(sql)

    def insert(self, name):
        sql = f"""
                INSERT INTO {self.table_name} (name) 
                VALUES ('{name}')
            """
        self._execute(sql)

    def update(self, name, number):
        sql = f"""
            UPDATE {self.table_name}
            SET name='{name}', number='{number}'
            WHERE id='5';
        """

        self._execute(sql)

    def delete(self, name):
        sql = f"""
                DELETE FROM {self.table_name}
                WHERE name='{name}'
            """
        self._execute(sql)
```

`SELECT changes()` 可以知道資料庫做了多少變動。

