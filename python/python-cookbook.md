# Python 錦囊妙計, 3/e \(Python Cookbook, 3/e\)

在寫裝飾器時，永遠要記得要使用 `functool` 的 `wraps`。

`wraps` 可以呼叫內部的函式屬性。

```python
import time
from functools import wraps

def timethis(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(func.__name__, end-start)
        return result
     return wrapper

countdown.__name__
countdown.__doc__
countdown.__annotations__
countdown.__wrapped__ # 取得未使用裝飾器的函式
```

## Concurrency

### 啟動 / 停止 thread

```python
from threading import Thread

t = Thread(target=countdown, args=(10,))
t.start() # 開始執行 thread

if t.is_alive(): # 確認 thread 是否執行中
    print('Still running')
else:
    print('Completed')

t.join() # 加入 thread 等待 thread 終止
```

如果有一個背景執行任務會一直執行，考慮使用 thread daemonic。  
 thread daemonic 無法被 join，當 thread 終止時，會自動銷毀

```python
t = Thread(target=countdown, args=(10,), daemon=True)
t.start()
```

如果想要控制 thread 中的任務，可以用以下方式

```python
class CountdownTask:
    def __init__(self):
        self._running = True
    def terminate(self):
        self._running = False
    def run(self, n):
        while self._running and n > 0:
        print('T-minus', n)
        n -= 1
        time.sleep(5)
        
c = CountdownTask()
t = Thread(target=c.run, args=(10,))
t.start()

c.terminate() # Signal termination
t.join() # Wait for actual termination (if needed)
```

### 判斷 thread 是否啟動

等到執行第七行 後才會繼續執行，`Event` 適合用在單次 thread 

```python
from threading import Thread, Event
import time

# Code to execute in an independent thread
def countdown(n, started_evt):
    print('countdown starting')
    started_evt.set()
    while n > 0:
        print('T-minus', n)
        n -= 1
        time.sleep(5)

# Create the event object that will be used to signal startup
started_evt = Event()

# Launch the thread and pass the startup event
print('Launching countdown')
t = Thread(target=countdown, args=(10,started_evt))
t.start()

# Wait for the thread to start
started_evt.wait()
print('countdown is running')
```

### thread 間傳遞資料

用 `queue`

### 密碼輸入工具

在 Terminal 中輸入密碼這樣，會自動隱藏你輸入的密碼。

{% hint style="danger" %}
有些系統可能沒辦法隱藏密碼
{% endhint %}

```python
import getpass

def svc_login(user, pwd):
    if user == "tsouminhan" and pwd == "123":
        return True
    return False


user = getpass.getuser() # 電腦環境的使用者名稱
# user = input("insert your username:")
passwd = getpass.getpass()

if svc_login(user, passwd): 
    print('Yay!')
else:
    print('Boo!')
```

## 打開瀏覽器網頁

```python
import webbrowser

webbrowser.open("http://www.python.org")
webbrowser.open_new("http://www.python.org")
webbrowser.open_new_tab("http://www.python.org")

c = webbrowser.get('firefox')
c.open("http://www.python.org")
```

## 加快程式執行速度

### 使用 function

值些寫程式碼的話，變數會是 global，用 function 變數會是 local，local 速度 &gt; global。

### 導入部分套件

`import math` 比 `from math import sqrt` 來得慢，導入太多東西了，自然就比較慢。

### Understand locality of variables

```python
import math

# faster
def compute_roots(nums):
    sqrt = math.sqrt
    result = []
    result_append = result.append
    for n in nums:
        result_append(sqrt(n))
    return result

# slower
def compute_roots(nums):
    result = []
    result_append = result.append
    for n in nums:
        result_append(math.sqrt(n))
    return result
```

```python
# Slower
class SomeClass:
...
    def method(self):
        for x in s:
            op(self.value)

# Faster
class SomeClass:
...
    def method(self):
        value = self.value
            for x in s:
            op(value)
```

### 避免不必要的抽象

`print` 的速度 `A.x` 是 `A.y` 的四倍多，所以在不必要的情況下可以不用 `@property`。

我才想說來試試看這樣子的寫法的說 ...，但看到書上說的很有到底，不一定要將其他語言的寫法挪用到拍森上，就參考一下吧。

```python
class A:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    @property
    def y(self):
        return self._y
        
    @y.setter
    def y(self, value):
        self._y = value
```

### 使用內建的 containers

list, dict, tuple, set 等等，不一定要自己寫。

### 避免不必要的資料

