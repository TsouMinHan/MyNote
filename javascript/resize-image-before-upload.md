# 壓縮圖片後傳至伺服器

```javascript
function imageResize(image) {
    return new Promise((resolve, reject) => {
        let img = new Image();
        let reader = new FileReader();
        
        reader.readAsDataURL(image);
        reader.name = image.name;
        reader.size = image.size;
        reader.onload = function (event) {
            img.src = event.target.result;
            img.name = event.target.name;
            img.size = event.target.size;
            img.onload = function (el) {
                var elem = document.createElement("canvas");
                elem.width = el.target.width;
                elem.height = el.target.height;

                while (elem.width * elem.height > 1000000){
                    elem.width = elem.width * 0.75;
                    elem.height = elem.height * 0.75;
                }

                var ctx = elem.getContext("2d");
                ctx.drawImage(el.target, 0, 0, elem.width, elem.height);

                ctx.canvas.toBlob(function (blob) {
                    resolve(blob); // 感覺就像 return
                });
            }
        }
    });
}
```

```javascript
await imageResize(image)
```

## 參考資料

1. [TheRogerLAB \| resize an image using javascript](https://www.therogerlab.com/how-can-i/javascript/resize-an-image.html#resizeImage#resizeImage#resizeImage#resizeImage#resizeImage#resizeImage#resizeImage#resizeImage)
2. [圖片純前端JS壓縮的實現 \| IT人](https://iter01.com/11677.html)
3. [在canvas.ToBlob（）異步函數之外訪問blob值 - 優文庫](http://hk.uwenku.com/question/p-kazofnyr-vq.html)
4. [await - JavaScript \| MDN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Operators/await)
5. [基本概念 · 從Promise開始的JavaScript異步生活](http://promise.eddychang.me/docs/contents/ch2_before_start/)

