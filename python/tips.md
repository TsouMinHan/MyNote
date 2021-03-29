---
description: Python 有很多指令都很方便使用，但也不是每次都會記起來那些指令怎麼使用，因此在這邊記錄下來。
---

# 好用卻常忘記的指令

## 判斷變數型態

```python
# isinstance(value, type)
isinstance(5, int) # True
# 也可以判斷其他資料型態。
```

我也看到`math`套件下有個方法是用來判斷是不是有限數的。

```python
import math
a = 6
b = 7.54
c = 8+0.54
d = 0*4
e = float("inf")
f = float("NaN")

print(math.isfinite(a)) # True
print(math.isfinite(b)) # True
print(math.isfinite(c)) # True
print(math.isfinite(d)) # True
print(math.isfinite(e)) # False
print(math.isfinite(f)) # False
```

## json 讀/寫檔案

```python
# 讀檔案
def read_json(path):
    with open(path, "r", encoding="utf-8") as json_file:
        data = json.load(json_file)

    return data
# 寫檔案
def save_json(path, dc={})
with open(path, "w", encoding="utf-8") as json_file:
    json.dump(dc, json_file)
```

## 裝飾器 - 顯示執行狀況

```python
import functools

def log(func):
    @functools.wraps(func)
    def wrap():        
        try:
            print(f"Running {func.__name__}")
            func()
            msg = "Finished!!"
            print(msg)

        except Exception as e:
            msg = e
            print(msg)

    return wrap
```

## 顯示變數名稱與值

```python
def debug(variable):
    # 若用locals()，只會顯示 variable = ...
    print ([ k for k,v in globals().items() if v == variable][0], '=', variable)
```

## 參考資料

1. [Introduction Python isfinite\(\) Method with Examples](https://morioh.com/p/029d0f069ce9)
2. [How to get a variable name as a string in Python?](https://www.tutorialspoint.com/How-to-get-a-variable-name-as-a-string-in-Python)

