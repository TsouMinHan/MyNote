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

