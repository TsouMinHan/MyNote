---
description: >-
  在看了些文章之後決定寫部落格來玩玩看，文中提到部落格可以讓別人了解自己會哪些技術或喜歡哪些事物或者當作自己的作品集，並透過輸出的方式加深自己的印象。查了相關資料後和根據自己對於各平台的了解，最後我選擇github
  page +
  Hexo，優點是免費、方便管理和佈署，而且我當初看到一個很喜歡的主題是在Hexo使用的，缺點是github是開源的因此大家有你的檔案，但我認為這沒有什麼影響啦。我把
---

# github pages + Hexo架設個人靜態部落格

## 辦github pages

照著教學做吧 [教學網址](https://pages.github.com/)

## 安裝 Hexo 環境

安裝需求\(Windows\)：

* [Node.js](https://nodejs.org/en/)
* [git](https://git-scm.com/)

## 安裝Hexo套件

打開terminal，輸入指令安裝hexo：

裝好之後初始化部落格：

## 修改網站配置

### 基本資料

修改的內容會呈現在網站中。

### 網站連結

將網址改成你的網站連結：

### 佈署資訊

設定佈署資訊： 因為hexo可以佈署在不同的平台，因此這邊的repo和branch要自己添加。 另外當時我在`:`後沒有空格會無法成功佈署，若有類似問題可以增加空白試試看。

也可以用`hexo server`在本機先進行測試後再佈署

## 佈署到github

輸入`hexo d`會要求登入github。

每次佈署都要手動打開終端機輸入指令滿麻煩的，所以寫了個`bat`檔案，往後只要執行該檔案就可以自動佈署了，方便許多。

最後打開自己的網頁就可以看到結果了。 架好自己的網站之後就要把網站弄得漂漂亮亮的，可以看下一篇文章。

## 參考來源

1. [\[教學\] 使用 GitHub Pages + Hexo 來架設個人部落格](https://ed521.github.io/2019/07/hexo-install/)
2. [如何搭建個人 Blog 使用 Hexo + Gitpage](https://medium.com/@bebebobohaha/%E4%BD%BF%E7%94%A8-hexo-gitpage-%E6%90%AD%E5%BB%BA%E5%80%8B%E4%BA%BA-blog-5c6ed52f23db)

