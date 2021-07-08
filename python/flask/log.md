# log

## 設定 logger

使用內建的 logging 套件，綁到 flask 上（？）

```python
import logging

class Formatter(logging.Formatter):
    def format(self, record):
        if record.levelno == logging.INFO:
            self._style._fmt = "%(asctime)s %(levelname)s: %(message)s"
        else:
            self._style._fmt = "%(asctime)s %(levelname)s: %(message)s [in %(pathname)s:%(lineno)d]"
        return super().format(record)

app = Flask(__name__)
...
app.debug = False

if not app.debug:
    handler = TimedRotatingFileHandler("./log/app.log", when="midnight", interval=1)
    handler.setLevel(logging.INFO)
    handler.setFormatter(Formatter())
    handler.suffix = "%Y%m%d.log"
    app.logger.addHandler(handler)
    app.logger.setLevel(logging.INFO)
    app.logger.info("start application")
```

```python
app.logger.info("info")
app.logger.debug("debug")
app.logger.warring("warring")
app.logger.error("error")
```

## 設定流程

flask `logger` 設定： 檔案路徑、輸出格式等

`before_request` & `after_request` 設定：記錄請求時間、訪問裝置等

`api_log` 設定：記錄從前端傳來的錯誤訊息。

```python
@api.route("/api/log/<level>", methods=["POST"])
def api_log(level):
    data = request.get_json()
    msg = ["{"]
    for key, value in data.items():
        msg.append(f"{key}: {value},")
    
    msg.append("}")
    if level == "ERROR":
        app.logger.error("\n".join(msg))
    
    return jsonify({})
```

