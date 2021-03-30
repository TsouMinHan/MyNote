# Day 6：Type Ahead

## Ajax 取得資料

分成 `XMLHttpRequest` 和 `fetch` 兩種方法，一個比較繁瑣但支援 progress，一個簡潔但不支援。

```javascript
function requestHandler(){
    console.log(JSON.parse(this.response));
}

let req = new XMLHttpRequest();
req.addEventListener("load", requestHandler);
req.open("get", url);
req.send();

fetch(url)
    .then(blob => blob.json())
    .then(data => console.log(data));
```

`toLocaleString()`: 方法返回這個數字在特定語言環境下的表示字符串，針對數字。

將變數 `* 1`，可以將符合的字串轉成數字，例如：`"123" * 1`。

## **參考資料**

1. [\[Alex 宅幹嘛\] 👨‍💻 深入淺出 Javascript30 快速導覽：Day 6：Type Ahead](https://www.youtube.com/watch?v=_TbG2iuN9kM&list=PLEfh-m_KG4dYbxVoYDyT_fmXZHnuKg2Fq&index=6)

