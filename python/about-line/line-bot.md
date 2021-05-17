# Line Bot

## Line Bot 基本結構

```python
from flask import Flask, abort, render_template, make_response, url_for, redirect
from flask import jsonify, request

from linebot import (
    LineBotApi, WebhookHandler
)
from linebot.exceptions import (
    InvalidSignatureError
)
from linebot.models import (
    MessageEvent, TextMessage, TextSendMessage, ImageMessage
)

app = Flask(__name__)

line_bot_api = LineBotApi(YOUR_LINE_CHANNEL_ACCESS_TOKEN)
handler = WebhookHandler(YOUR_LINE_CHANNEL_SECRET)

# decorator 負責判斷 event 為 MessageEvent 實例，event.message 為 TextMessage 實例。所以此為處理 TextMessage 的 handler
@handler.add(MessageEvent, message=TextMessage)
def handle_message(event):
    # 決定要回傳什麼 Component 到 Channel
    msg = event.message.text
    line_bot_api.reply_message(
        event.reply_token,
        TextSendMessage(text=msg))
```

## 一些屬性

### 使用者 ID

`event.source.user_id`

## 取得圖片

```python
...
@handler.add(MessageEvent, message=(TextMessage, ImageMessage)) # 注意要加上 ImageMessage
def handle_message(event):
    file = line_bot_api.get_message_content(event.message.id)
    b = b"" # byte

    for chunk in file.iter_content():
        b += chunk
```

## 參考資料

1. [GitHub - line/line-bot-sdk-python: LINE Messaging API SDK for Python](https://github.com/line/line-bot-sdk-python#source)
2. [Line Notify: 利用Python傳送客製化訊息 — 以吉娃娃長輩圖為例。 - Eason - Medium](https://eason851021.medium.com/line-notify-%E5%88%A9%E7%94%A8python%E5%82%B3%E9%80%81%E5%AE%A2%E8%A3%BD%E5%8C%96%E8%A8%8A%E6%81%AF-%E4%BB%A5%E5%90%89%E5%A8%83%E5%A8%83%E9%95%B7%E8%BC%A9%E5%9C%96%E7%82%BA%E4%BE%8B-2a50c6a5197b)
3. [\[問題\] linebot 接收圖片 - 看板 Python - 批踢踢實業坊](https://www.ptt.cc/bbs/Python/M.1592030912.A.3AB.html)



