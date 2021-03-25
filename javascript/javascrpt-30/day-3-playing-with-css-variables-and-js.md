# Day 3：Playing with CSS Variables and JS

`:root` 等同於 `html`，指向文件的根。

```css
    :root {
      --base: #ffc600;
      --spacing: 10px;
      --blur: 10px;
    }

    .hl {
      color: var(--base);
    }

    img {
      padding: var(--spacing);
      background: var(--base);
      filter: blur(var(--blur));
    }
```

可以透過以下程式碼去證明。

```jsx
document.querySelector(":root") === document.querySelector("html") === document.documentElement
```

設定 css 值建議使用 `setProperty()`。

`dataset` 會讀取該標籤下 data 開頭的屬性，例如： `data-sizing="px"`，輸入`this.dataset.sizing` 就會得到 `px`。

## 參考資料

1. \*\*\*\*[**\[Alex 宅幹嘛\] 👨‍💻 深入淺出 Javascript30 快速導覽：Day 3：Playing with CSS Variables and JS**](https://www.youtube.com/watch?v=fIE2Lmfbo4k&list=PLEfh-m_KG4dYbxVoYDyT_fmXZHnuKg2Fq&index=3)\*\*\*\*

