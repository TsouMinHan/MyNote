# 上傳圖片至 Firebase Stroage

##  連線至 Storage

### 方法一

```python
import firebase_admin
from firebase_admin import credentials
from firebase_admin import storage

cred = credentials.Certificate('path/to/service_account_key.json')
firebase_admin.initialize_app(cred, {
    'storageBucket': '<BUCKET_NAME>.appspot.com'
})

bucket = storage.bucket()
# 如果有設定 app 的名稱的話，使用下面這個指令
# bucket = storage.bucket(app=firebase_admin.get_app("APP_NAME"))
```

### 方法二

```python
from google.cloud import storage
from firebase import firebase
import os

os.environ["GOOGLE_APPLICATION_CREDENTIALS"]="<add your credentials path>"

firebase = firebase.FirebaseApplication("<your firebase database path>")
client = storage.Client()
bucket = client.get_bucket("<your firebase storage path>")
```

## 上傳圖片

```python
# posting to firebase storage
image_blob = bucket.blob("/") # 設定要上傳的檔名，要用反斜線，不然不會建立資料夾
# blob.delete() # 刪除圖片

image_path = "<local_path>/image.png"
image_blob = bucket.blob("<image_name>")
image_blob.upload_from_filename(image_path)
```

## 將上傳檔案設定為公開

若要上傳時就設定公開，請先上傳檔案後再執行 `make_public()`，否則會找不到檔案。

```python
blob.make_public() # 將圖片設定為開放
blob.public_url # 取得網址
```

## 列出所有文件

```python
# 列出所有在 firestorage 上的資料，prefix 代表資料夾
for blob in bucket.list_blobs(prefix='signInLog'):
    print(str(blob.name))
```

## 下載文件

```python
blob = bucket.blob(f"{filename}")
blob.download_to_filename(filename)
```

## 打包成 exe 錯誤排除

[尝试执行 Google 云 API 时 GRPC 中出现异常](https://www.cnpython.com/qa/575109) [使用 pyinstaller 将导入 Google 客户端库的程序转换为.exe](https://www.codenong.com/afb5164326a2eb6f6259/)

### 資料來源

1. [Image Upload to Firebase Storage with Python](https://medium.com/@preveenraj/image-upload-to-firebase-storage-with-python-ebf18c615f34)
2. [How to retrieve image from Firebase Storage using Python?](https://stackoverflow.com/questions/53304517/how-to-retrieve-image-from-firebase-storage-using-python)
3. [Firebase Storage - error with uploading png image via Python google-cloud-storage lib](https://stackoverflow.com/questions/60080133/firebase-storage-error-with-uploading-png-image-via-python-google-cloud-storag)
4. [尝试执行 Google 云 API 时 GRPC 中出现异常](https://www.cnpython.com/qa/575109)
5. [使用 pyinstaller 将导入 Google 客户端库的程序转换为.exe](https://www.codenong.com/afb5164326a2eb6f6259/)
6. \*\*\*\*[**Find the url of uploaded file, firebase storage + python**](https://stackoverflow.com/questions/52451215/find-the-url-of-uploaded-file-firebase-storage-python)\*\*\*\*
7. [Blobs / Objects — google-cloud-storage documentation](https://googleapis.dev/python/storage/latest/blobs.html) 
8. [Buckets — google-cloud-storage documentation ](https://googleapis.dev/python/storage/latest/buckets.html)

