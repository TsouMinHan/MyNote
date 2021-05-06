---
description: >-
  Firebase 有很多好用的功能，其中之一就是資料庫，資料庫又分成 Cloud Firestore 和 Real Time
  Database，各有各的優缺點，我主要是用 Cloud Firestore，目前使用下來我覺得非常的方便，接下來會介紹些我使用過的指令。
---

# Cloud Firestore 新增刪除修改（CRUD）

## Cloud Firestore 介紹

是NoSQL資料庫，具有擴展性，具有擴展性、同步性、支援離線存檔\(這個我還沒有用過\)，不論是IOS、Android、Web應用程式，都可以透過伺服器SDK進行資料存取，支援多種語言（Node.js，Java，Python，Unity，C ++和Go SDK），我主要是使用Python，所以接下來都會介紹Python的指令。

## 創建專案

進入Firebase網頁，登入Google帳號，選擇新增專案。 建立好專案之後到設定頁面，選擇服務帳戶，點選產生新的私密金鑰（這個檔很重要，不要放在開放的伺服器上或者給別人）。

## 安裝套件

`pip install --upgrade firebase-admin`

## 初始化設定

初始化只能設定一次，如果設定第二次會出錯。

```python
import firebase_admin
from firebase_admin import credentials
from firebase_admin import firestore

# Use a service account
cred = credentials.Certificate("path/to/serviceAccount.json")   # 這邊的json檔案就是創建專案時下載的金鑰檔案
firebase_admin.initialize_app(cred)

db = firestore.client()
```

### 判斷是否有連線

```python
import firebase_admin
from firebase_admin import credentials
from firebase_admin import firestore

if (not len(firebase_admin._apps)): # 檢查連線的資料庫數量 0 代表沒連線
    cred = credentials.Certificate("path/to/serviceAccount.json")
    firebase_admin.initialize_app(cred)

db = firestore.client()
```

## 連接多個資料庫

```python
cred = credentials.Certificate("path/to/serviceAccount.json")
firebase_admin.initialize_app(cred, name="server") # 連線命名

db = firebase_admin.firestore.client(firebase_admin.get_app("server"))
```

## 集合和文件

Cloud Firestore的資料格是像是資料夾一樣，每個資料夾是一個集合（Collection，每個資料夾下可以有很多個文件（Document），每個文件底下可以有很多資料，而在文件底下又可以開新的集合，這樣子重複下去。 當時在學習時覺得這樣子的概念很抽象，但是實際創建資料並且去讀取，會發現很簡單。

文件的 key 不要使用 `-`，雖然可以順利新增，但若要修改時會出錯，原因我目前不知道，這樣會導致以後要修改時，必須先把資料抓下來在整個覆蓋過去，會造成多餘的步驟。

## 新增資料

```python
doc_ref = db.collection(u"users").document(u"alovelace")    # 讀取"users"集合裡的"alovelace"文件
# 文件的資料資料型態是dict
doc_ref.set({
    u"first": u"Ada",
    u"last": u"Lovelace",
    u"born": 1815
})
```

## 讀取資料

```python
users_ref = db.collection(u"users")
docs = users_ref.stream() # 取得集合的文件，也可以用get()

for doc in docs:
    # doc.id是每個文件的id，doc.to_dict()是把文件的資料轉成dict型態
    print(u"{} => {}".format(doc.id, doc.to_dict()))
```

## 刪除資料

```python
doc_ref = db.collection(u"users").documetn(u"alovelace")
doc_ref.delete()

# 刪除集合所有文件
docs = db.collection(u"users").stream()

for doc in docs:
    doc.reference.delete()
```

## 修改資料

如果是新的key則是新增，例如本來文件內就有title的key執行後會修改值，但若沒有title的話就是直接新增。

```python
doc_ref = db.collection(u"users").document(u"alovelace")
doc_ref.update({"title": _ls})
```

## 結論

基本上我只使用這幾個功能，使用起來非常的方便。

### 參考資料

1. [check if a Firebase App is already initialized in python](https://stackoverflow.com/questions/44293241/check-if-a-firebase-app-is-already-initialized-in-python)
2. [Google Firebase Document](https://firebase.google.com/docs/firestore/quickstart#python)
3. [firebase\_admin module \| Firebase](https://firebase.google.com/docs/reference/admin/python/firebase_admin)

