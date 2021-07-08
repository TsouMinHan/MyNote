# Flask 不存圖片 修改圖片大小

```python
image = request.files["image"]
buf = image.read() # byte

npimg = numpy.fromstring(buf, numpy.uint8) # numpy array
img = cv2.imdecode(npimg, 4) # image

# resize
while img.shape[0]*img.shape[1] > 800000:
    img = cv2.resize(img, (0,0), fx=0.5, fy=0.5)

is_success, im_buf_arr = cv2.imencode(".jpg", img)
im_buf_arr.tobytes() # get bytes
```

## 參考資料

1. [curl - Reading image file \(file storage object\) using CV2 - Stack Overflow](https://stackoverflow.com/questions/47515243/reading-image-file-file-storage-object-using-cv2)
2. [Convert PIL or OpenCV Image to Bytes without Saving to Disk - jdhao's blog](https://jdhao.github.io/2019/07/06/python_opencv_pil_image_to_bytes/)

