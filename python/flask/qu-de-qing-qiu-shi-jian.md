# 取得請求時間

在 request 前執行的動作，存在 g 變數中\(g 是當前 request 的全域變數）。

```python
from flask import g
from app import app

@app.before_request
def before_request():
    g.request_start_time = time.time()
    g.request_time = lambda: "%.5fs" % (time.time() - g.request_start_time)
    
@app.after_request
def after(response):
    browser = request.user_agent.browser
    app.logger.info(
        f"{request.method}, {response.status}, {request.url}, {browser}, {g.request_time()} "
    )
    return response
```

## 參考資料

1. [flask: show request time in template](https://gist.github.com/lost-theory/4521102)
2. [Python Flask\_變量與請求 - HackMD](https://hackmd.io/@shaoeChen/rJnJWaq1z?type=view)

