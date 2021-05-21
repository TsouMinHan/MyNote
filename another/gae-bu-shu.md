# GAE 部署

## 部署前動作

`pip freeze > requirements.txt`

檢查套件

補上 `gunicorn==19.3.0` 因為 `docker`

## GAE 上安裝 OpenCV

{% code title="requirements.txt" %}
```text
...
numpy=1.19.5
opencv-python--headless
...
```
{% endcode %}

## 時間

在 GAE 上預設時間是 UTC+0，我也不清楚要怎麼修改，目前就是使用 `datetime` [改時區的方式](../python/datetime.md#zhuan-huan-shi-ou)。

## 參考資料

1. [google compute engine - ERROR: \(gcloud.app.deploy\) Error Response: \[9\] Application startup error! Code: APP\_CONTAINER\_CRASHED /bin/sh: 1: exec: gunicorn: not found - Server Fault](https://serverfault.com/questions/1024864/error-gcloud-app-deploy-error-response-9-application-startup-error-code)
2. [Importerror: libgl.so.1: cannot open shared object file: no such file or directory opencv error - Streamlit sharing - Streamlit](https://discuss.streamlit.io/t/importerror-libgl-so-1-cannot-open-shared-object-file-no-such-file-or-directory-opencv-error/7031/9)

