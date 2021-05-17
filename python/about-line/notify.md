# Notify

## 傳送圖片

一定要傳送 `message`，不然沒辦法顯示圖片。  
`img` 就是圖檔，要嘛用 `open` 打開，不然就是傳送 `byte`

```python
import requests

def send_image(message, img):
    headers = {"Authorization": "Bearer " + YOUR_NOTIFY_TOKEN}
    param = {"message": f"{message} : 圖片"}
    # image = {"imageFile" : open(str(img), 'rb')}
    image = {"imageFile" : img}
    r = requests.post("https://notify-api.line.me/api/notify", 
        headers = headers, 
        params = param, 
        files = image
    )
    return r.status_code
```

