# 上傳圖片至 Firebase Stroage

## 上傳圖片

```python
from google.cloud import storage
from firebase import firebase
import os

os.environ["GOOGLE_APPLICATION_CREDENTIALS"]="<add your credentials path>"

firebase = firebase.FirebaseApplication("<your firebase database path>")
client = storage.Client()
bucket = client.get_bucket("<your firebase storage path>")

# posting to firebase storage
imageBlob = bucket.blob("/") # 設定要上傳的檔名，要用反斜線，不然不會建立資料夾
# blob.delete() # 刪除圖片

imagePath = "<local_path>/image.png"
imageBlob = bucket.blob("<image_name>")
imageBlob.upload_from_filename(imagePath)
```

## 打包成 exe 錯誤排除

[尝试执行 Google 云 API 时 GRPC 中出现异常](https://www.cnpython.com/qa/575109) [使用 pyinstaller 将导入 Google 客户端库的程序转换为.exe](https://www.codenong.com/afb5164326a2eb6f6259/)

### 資料來源

1. [Image Upload to Firebase Storage with Python](https://medium.com/@preveenraj/image-upload-to-firebase-storage-with-python-ebf18c615f34)
2. [How to retrieve image from Firebase Storage using Python?](https://stackoverflow.com/questions/53304517/how-to-retrieve-image-from-firebase-storage-using-python)
3. [Firebase Storage - error with uploading png image via Python google-cloud-storage lib](https://stackoverflow.com/questions/60080133/firebase-storage-error-with-uploading-png-image-via-python-google-cloud-storag)
4. [尝试执行 Google 云 API 时 GRPC 中出现异常](https://www.cnpython.com/qa/575109)
5. [使用 pyinstaller 将导入 Google 客户端库的程序转换为.exe](https://www.codenong.com/afb5164326a2eb6f6259/)

