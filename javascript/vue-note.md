---
description: 覺得Vue似乎很好玩，就來學看看了，目前感覺不錯玩，把一些筆記寫下來，寫得很爛，要修改。
---

# Vue 筆記

## 設定Vue物件\(?\)

```javascript
<script src='https://cdnjs.cloudflare.com/ajax/libs/vue/3.0.0-beta.20/vue.cjs.js'></script>
//▲必須先匯入(?)，像BootStrap、JQuery那樣要這樣才可以使用他們的框架，關鍵字：cdn。

let vm = new Vue({ // 可以直接 new Vue 前面省略
    el: "#app", // 綁定使用的區塊  <div id="app"> ... </div>  在這個區塊下都在這個vm的使用範圍內
    data: data, // 就是你的資料，data是物件 let data = {...}
    // let data = {
    //     selected: "",
    //     options: [],
    //     result: []
    // }
    mounted: {
    },
    computed: { // 資料處理，隨著資料變動，有catch機制，會一直存在，一些需要運算的可以寫在這邊，大致上就是在讀取資料時需要經過些篩檢時需要用到
        today(){  // 讀取
            return 1
        }
    },
    methods:{ // 方法，就是這麼簡單，一些click事件等等
        function(){
            // do something
        }
    },
    watch:{ //觀察值
        number(){
            console.log()
        }
    },
    ['obj.num'](){ //物件的屬性

    }   
})
```

## 更改分隔符號

像是我在 Flask 使用 Vue 時，會因為 Vue 原本的符號 `{ {` 和 `} }` 會和 Jinja2 的衝突到，所以可以更改符號。

`{` 符號不一定要空格，上面會空格是因為連續在一起的話 hexo 會以為是自己的語法，導致部屬時出現錯誤。

```javascript
var app = new Vue({ 
    el: '#app',
    delimiters: ["[[", "]]"],
    data: data
});
```

## 語法

#### 給標籤值

```markup
<!-- 動態給圖片src，@可省略 -->
<img :src = "url">
<img @:src = "url">
```

## 顯示文字

```markup
<!-- 這邊跟jinja2類似 -->
<p>{{ title }}</p>
```

## if判斷

```markup
<a v-if="條件"></a>
```

## click事件

```markup
<a v-on:click="function()"></a>
<a @click="function()"></a>
```

## for迴圈

```markup
<a v-for="(item, index) in items"></a>
```

## input修改資料

data中會有個name的值，這邊input輸入的值就會帶到後端

```markup
<input v-model="name" @keyup.enter="function" > <!-- enter彈起來時會做的事情 -->
<input v-model.trim="name">  <!-- 去除頭尾空白 -->
```

## 綁定選單

```markup
    <div class="input-group">
        <select class="custom-select" v-model="selected"> <!-- selected代表你選定的那個物件 -->
            <option v-for="option in options" v-bind:value="{ url: option.url, text: option.text}"> 
            <!-- v-bind:value代表selected的值 -->
                {{ option.text }}
            </option>
        </select>
        <div class="input-group-append">
            <button class="btn btn-outline-secondary" type="button">確定</button>
        </div>
    </div>
```

## 其他

#### 設定值

畫面無法更新的話就用`$set()`。

## 參考來源

1. [Alex 宅幹嘛](https://www.youtube.com/watch?v=4hNOhWPqz3k&list=PLEfh-m_KG4dYor8h4Hi2lqKJ0xqNTFh16&index=14)

