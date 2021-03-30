---
description: CKEditor 4 分成三種樣式，基本、標準、完整。
---

# CKEditor 4 網頁文字編輯器

## 安裝

1. [官網](https://ckeditor.com/ckeditor-4/download/)下載
2. 使用 CDN

## 套至 html

```markup
<!doctype html>
<html lang="en">

<body>
    <textarea name="editor1"></textarea>


</body>
<!-- CDN -->
<script src="//cdn.ckeditor.com/4.16.0/standard/ckeditor.js"></script>

<!-- 使用 CKEDITOR 將原本的 textarea 覆蓋掉 -->
<script>CKEDITOR.replace("editor1");</script>

</html>
```

## 設定 textarea 的內容

```javascript
CKEDITOR.instances["editor"].setData(""); // clear textarea
```

## 取得 textarea 的內容

```javascript
console.log(CKEDITOR.instances['editor1'].getData());
console.log(CKEDITOR.instances.editor1.getData());
```

## 參考資料

1. [CKEditor 4 download](https://ckeditor.com/ckeditor-4/download/)
2. [網頁最強的文字編輯器 CKEditor﹍安裝使用心得整理](https://www.wfublog.com/2017/11/web-wysiwyg-text-editor-ckeditor.html)
3. [Getting and Saving Data in CKEditor 4](https://ckeditor.com/docs/ckeditor4/latest/guide/dev_savedata.html)

