# Day 2：CSS + JS Clock

```jsx
// setInterval、setTimeout、requestAnimationFrame //

setInterval(fnc, 1000) // 設定間隔，持續執行。盡量不要重複執行interval（就是呼叫自己）

// 設定延遲，執行一次。大部份會在fnc內繼續呼叫自己(setTimeout)達到連續的效果
setTimeout(fnc, 1000) 

requestAnimationFrame() // 專門處理畫面的setTimeout - by alex

//IIFE，定義完馬上執行function
;(function(){
    //確保在這個function內的變數與函式不會直接被外部讀取，有點像let那樣
    // ;用來和前面的function做區隔的，保險起見習慣+一下吧
})
```

## 參考資料

1. \*\*\*\*[**\[Alex 宅幹嘛\] 👨‍💻 深入淺出 Javascript30 快速導覽：Day 2：CSS + JS Clock**](https://www.youtube.com/watch?v=O1YsB3qxO4g&list=PLEfh-m_KG4dYbxVoYDyT_fmXZHnuKg2Fq&index=2)\*\*\*\*



