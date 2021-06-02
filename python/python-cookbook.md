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

### 鎖 thread 防止 race conditions



