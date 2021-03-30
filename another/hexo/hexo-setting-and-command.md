---
description: 這一篇會寫我自己用在這個網站上的設定以及相關指令，如果你喜歡的話可以繼續看下去。另外還沒有架站的朋友可以看上一篇文章後再來看這篇。
---

# Hexo 相關設定和指令

## 主題設定

### 更改主題

[NexT](https://github.com/theme-next/hexo-theme-next)主題我覺得很漂亮，很喜歡。

打開 terminal：

接著打開`_config.yml`，theme 改成 next 就可以了，記得要在重新佈署一次唷! 我記得是因為靜態檔案的關係，佈署之後網頁不會馬上更新，建議使用 Ctrl+F5 更新頁面，不同瀏覽器似乎有不同的方式，若有問題的話再查一下吧!

```yaml
# ./_config.html
theme: next
```

### 修改 icon

```yaml
# ./themes/next/_config.yml
favicon:
    small: /images/icon.png # 設定成你要的圖片，可以放在public/images/裡面
```

### 修改大頭貼

```yaml
# ./themes/next/_config.yml
avatar:
    # 改成你要的大頭貼路徑或網址
    url: /images/apple-touch-icon-next.png
```

### 切換主題布景

預設是 Muse，可以到[這邊](https://github.com/theme-next/hexo-theme-next)查看樣式，另外如果佈署之後發現沒有變化的話輸入`hexo d`清除之前建立的靜態檔案，然後再重新佈署一次，因為css檔案的問題。

```yaml
# ./themes/next/_config.yml
# Schemes
# scheme: Muse
# scheme: Mist
# scheme: Pisces
scheme: Gemini
```

### 社群連結

有很多選項，這邊只顯示部分選項。

```yaml
# ./themes/next/_config.yml
  social:
    # GitHub: https://github.com/yourname || github
    # E-Mail: mailto:yourname@gmail.com || envelope
```

### 友情連結

在`links`輸入網址。

```yaml
# ./themes/next/_config.yml
  # Blog rolls
  links_settings:
    icon: fa fa-link
    title: Links
    # Available values: block | inline
    layout: block

  links:
    # Title: http://yoursite.com
```

### Menu 設定

```yaml
# ./themes/next/_config.yml
  menu:
    home: /
    categories: /categories # 手動增加頁面
    about: /about # 手動增加頁面
    archives: /archives
    tags: /tags # 手動增加頁面
    #commonweal: /404.html # 手動增加頁面
```

### 程式碼區塊主題

[這邊](https://github.com/chriskempson/tomorrow-theme)可以看主題

```yaml
# ./themes/next/_config.yml
  codeblock:
    # normal | night | night eighties | night blue |
    # night bright | solarized | solarized dark | galactic
    highlight_theme: night
    copy_button:
      enable: true # 顯示copy按鈕
      # Show text copy result.
      show_result: true # 按下copy按鈕後會顯示勾勾
      # Available values: default | flat | mac
      style:
```

### 按鈕顯示百分比

```yaml
# ./themes/next/_config.yml
  back2top:
    enable: true
    # Back to top in sidebar.
    sidebar: false # true會顯示在sidebar
    # Scroll percent label in b2t button.
    scrollpercent: true  # 這邊輸入true
```

### 顯示目錄

```yaml
# ./themes/next/_config.yml
  toc:
    enable: true 
    # Automatically add list number to toc.
    number: true
    wrap: true # 是否會顯示子目錄
    expand_all: true # 是否自動展開子目錄
    # Maximum heading depth of generated toc.
    max_depth: 6
```

### 修改標籤樣式

把`#`換成 符號。

```yaml
# ./themes/next/_config.yml
  tag_icon: true
```

### 使用留言板

到 [Disqus](https://disqus.com/) 點 Get Started，接著註冊帳號（我是用 google 的），接著點選 I want to install Disqus on my site。 要進行些設定，Website Name 就是自定的名稱，會顯示在，會顯示在紅色箭頭處。 另外可以選擇語言，有中文的，但是我看參考來源他的留言板是簡體中文的，所以我選擇英文。

![](../../.gitbook/assets/hexo-1.png)

接著把你輸入的Website Name複製到`_config.yaml`就好了。

```yaml
# ./themes/next/_config.yml
  # Disqus
  disqus:
    enable: true
    shortname: KimoBlog
    count: true
    #post_meta_order: 0
```

### 統計瀏覽人數和觀看次數

查了些文章，似乎主要有兩種方法，我選擇用這個方式，只要改`_config.yaml`就好。

```yaml
# ./themes/next/_config.yml
  # Show Views / Visitors of the website / page with busuanzi.
  # Get more information on http://ibruce.info/2015/04/04/busuanzi
  busuanzi_count:
    enable: true
    total_visitors: true
    total_visitors_icon: fa fa-user
    total_views: true
    total_views_icon: fa fa-eye
    post_views: true
    post_views_icon: fa fa-eye
```

### 紀錄文章字數以及閱讀時間

執行安裝指令。

```bash
npm install hexo-symbols-count-time
```

預設字符長度是`4`閱讀速度是`275`，應該是用這些參數來做判斷的依據吧，更詳細的內容在[github](https://github.com/theme-next/hexo-symbols-count-time)內有說明。

```yaml
# ./themes/next/_config.yml
  # Post wordcount display settings
  # Dependencies: https://github.com/theme-next/hexo-symbols-count-time
  symbols_count_time:
    separated_meta: true # 改成flase時，我文章的內容就無法顯示了，所以還是別亂改吧
    item_text_post: true
    item_text_total: true # 是否顯示文字 文章字數、所需閱讀時間
```

另外，或許也會有人跟我遇到一樣的問題，就是安裝完之後會閱讀時間會顯示`NaN：aN`。 解決方法可以輸入`hexo clean`，[來源](https://github.com/theme-next/hexo-symbols-count-time/issues/53)

### 顯示版權資訊

我只是覺得用這個似乎會有點專業的感覺。

```yaml
# ./themes/next/_config.yml
  creative_commons:
    license: by-nc-sa
    sidebar: false
    post: true
    language: deed.zh_TW  # 點開連結時會顯示繁中
```

![](../../.gitbook/assets/hexo-2.png)

## Hexo指令

### 新增文章

在`source/_posts`新增`post_name.md`

打開 terminal：

```bash
hexo new <post_name>
```

### 新增標籤頁面

Terminal 輸入指令：

```bash
hexo new page "tags"
```

把剛剛新生成的檔案進行編輯： 新增`type: "tags"`

```markup
<!-- tags/index.md -->
  ---
  title: 標籤
  date: 2020-04-16 18:58:47
  type: "tags"
```

### 新增分類頁面

Terminal 輸入指令：

```bash
hexo new page "categories"
```

把剛剛新生成的檔案進行編輯： 新增`type: "categories"`

```markup
<!-- ./categories/index.md -->
  ---
  title: 分類
  date: 2020-04-16 19:05:45
  type: "categories"
```

### 新增關於頁面

Terminal 輸入指令

```bash
 hexo new page "about"
```

把剛剛新生成的檔案進行編輯： 新增`type: "about"`

```markup
<!-- ./about/index.md -->
  ---
  title: 分類
  date: 2020-04-16 19:06:43
  type: "about"
```

記得檢查有沒有修改`_config.yml`檔案哦。

### 程式碼區塊

```text
<!-- 效果就是markdownk的程式區塊語法 -->
{% codeblock %}
    print(1)
{% endcodeblock %}
```

```text
<!-- 效果就是markdownk的程式區塊語法，指定語言 -->
{% codeblock lang:python %}
    print(1)
{% endcodeblock %}
```

```text
{% codeblock ./path/filename %}
<!-- 效果就是markdownk的程式區塊語法，並且會顯示檔案路徑 -->
  print(1)
{% endcodeblock %}
```

### 內文連結

```text
    {% post_link 檔案路徑名稱 要顯示的文字 %}
    {% post_link hello-world <<github pages + Hexo架設個人靜態部落格>> %}
```

### 在文章中使用圖片

絕對路徑： 可以把圖片放在`source/images`資料夾中，markdown語法：

```text
![](/images/image.jpg)
```

相對路徑： 把`_config.yml`的`post_asset_folder`設為`true`之後使用`$ hexo new <post_name>`新增文章時，會在`source/post`產生同名的資料夾，直接把圖片放在裡面就好了。

```yaml
# ./_config.yml
  post_asset_folder: true
```

markdown語法：

```text
 ![](image.jpg)
```

另外我在本地寫`.md`檔案時圖片不會顯示，但是部屬之後是正常的，還有這種方式只能在文章中顯示，不能在首頁顯示。

## 結論

有很多地方可以做更改，只需要花時間去查一下如何更改設定就好，不用自己寫程式碼真的很方便。 還有就是如果佈署之後發現怪怪的，`hexo clean`一下應該都可以解決，似乎是一些靜態檔案的關係。

## 參考資料

1. [Hexo博客搭建之在文章中插入圖片](https://yanyinhong.github.io/2017/05/02/How-to-insert-image-in-hexo-post/)
2. [Hexo deploy fail to change scheme \[solved\]](https://github.com/theme-next/hexo-theme-next/issues/421)
3. [主題配置 - NexT 使用文檔](http://theme-next.iissnan.com/theme-settings.html)
4. [Hexo博客NexT主題開啟文章目錄和調整樣式](https://blog.csdn.net/wugenqiang/article/details/88609066)
5. [Posts\|NexT](https://theme-next.org/docs/theme-settings/posts)
6. [Tag Plugins\|Hexo](https://hexo.io/docs/tag-plugins.html#Code-Block)
7. [Cloud F2E Blog: Hexo 架站攻略 - NexT 相關設定](https://syj0905.github.io/Hexo/20190902/hexo-next-setting/)
8. [泰迪熊的程式足跡: Hexo Next人數統計\(Busuanzi & LeanCloud\)](https://teddybearfp.github.io/2019/03/29/Hexo-Next-%E4%BA%BA%E6%95%B8%E7%B5%B1%E8%A8%88-Busuanzi-LeanCloud/)
9. [Amdoing: 使用Hexo的next主题，配置POST文章文末的版權信息](http://blog.amdoing.com/the-post-copyright-in-hexo-next/)

