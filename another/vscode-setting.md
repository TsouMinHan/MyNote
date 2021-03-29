---
description: 單純想要記錄一下我在 VS Code 上安裝的套件跟一些設定，以後換電腦時可以快速設定。
---

# VSCode 設定

## 套件

### flask-snippets

一看才發現原來我有裝這個套件，就可以輸入快捷鍵產生特定指令，好像方便但是我根本沒用過... 慢慢試著來用吧，不然 flask 有些指令真的很繁瑣。

### Jinja

幫程式碼上色，比較好辨識程式碼區塊，但我還是覺得很亂就是了。

### Markdown Preview Enhanced

就 Markdown。

### Power Mode

很好玩的套件，在打程式時會出現些特效，讓寫程式碼比較不會那麼單調，但有些人可能會覺得很礙事。 當初我也是花很多時間找到這個套件呢，可以開啟Json設定相關屬性，但是我也忘記在哪邊弄了，就直接在 VS Code 的 settings 設定吧。

```javascript
Enable Shake: 打字時是否晃動，建議關掉。
Explosion Duration: 特效顯示的時間長短，我是設1000（毫秒）。
Explosion Frequency: 按多少個按鍵後會產生特效，我是設2。
Explosion Offset: 爆炸產生的位置，向上移動，我是設0.35。
Explosion Size: 爆炸特效的大小，我是設10。
Presets: 特效樣式，我就選第一個像素方塊。
```

### Todo Tree

可以看到在程式碼 TODO 的註解處，我通常是用來註記暫時修改的地方，以免自己忘記。

### TabNine

很猛的 AI 提示字插件，看你常打哪些指令或字就會出現相關的，並且它會推測你下一行指令會是什麼，真的不知道怎麼寫的呢，當初用了一段時間，雖然很方便，但是 VS Code 本來的提示字會被覆蓋掉，最後我還是沒有在用。

### Bracket Pair Colorizer

會將成對的括弧用顏色加以標記，比較不會找錯括弧，但是配上 Monokai 樣式會有點花俏，要花點時間習慣。

### Indenticator

會在區塊範圍內用線條顯示，比較好找到區塊範圍，但是配上 Monokai 樣式會有點花俏，要花點時間習慣。

### cdnjs

直接用插件把 library 導入至文件中。

### indent-rainbow

tab 的空格會有顏色

## 相關設定

### Color Threme

Monokai 我的最愛。

### font

大小設 18。

### auto save

自動儲存檔案，改成 onFacusChange。

### rulers

在設定行數的位置畫上線，用來提醒自己程式碼行數過多，像圖片中就是設定在 80 和 100行的位置。

### Word Wrap

改成 on，若超過 rulers 設定的行數，會自行換行。

## 我的 VS code setting.json & Plugin

finename：`settings.json`

```javascript
{
    "todo-tree.tree.showScanModeButton": false,
    "powermode.explosionSize": 10,
    "powermode.enabled": true,
    "powermode.enableShake": false,
    "editor.fontSize": 20,
    "powermode.comboTimeout": 20,
    "editor.rulers": [
        80,
        100
    ],
    "editor.wordWrap": "on",
    "workbench.colorTheme": "Monokai",
    "workbench.startupEditor": "newUntitledFile",
    "python.linting.enabled": true,
    "python.linting.pylintEnabled": true,
    "background.enabled": true,
    "background.useDefault": false,
    "background.customImages": [    
        "C:/Users/Tsou/翰仔/CG圖片/Adventure Time/Adventure Time-BMO.png",
        "C:/Users/Tsou/翰仔/CG圖片/Adventure Time/408789.jpg",
    ],
    "background.style": {
        "content": "''",
        "pointer-events": "none",
        "position": "absolute",
        "z-index": "99999",
        "width": "100%",
        "height": "100%",
        "background-position": "center",
        "background-repeat": "no-repeat",
        "background-size": "100%,100%",
        "opacity": 0.1
    },
    "extensions.ignoreRecommendations": false,
    "workbench.iconTheme": "vscode-icons",
    "[html]": {
        "editor.defaultFormatter": "vscode.html-language-features"
    },
    "[javascript]": {
        "editor.defaultFormatter": "vscode.typescript-language-features"
    },
    "files.autoSaveDelay": 2000,
    "python.linting.mypyEnabled": true,
    "workbench.editorAssociations": [
        {
            "viewType": "jupyter.notebook.ipynb",
            "filenamePattern": "*.ipynb"
        }
    ]
    
}
```

## Plug in

在 VS Code 的 Terminal 輸入指令，接著就會跑出輸出，之後再複製執行就好。

```bash
code --list-extensions | % { "code --install-extension $_" }
```

我目前安裝的套件

```bash
code --install-extension CoenraadS.bracket-pair-colorizer
code --install-extension cstrap.flask-snippets
code --install-extension Gruntfuggly.todo-tree
code --install-extension hoovercj.vscode-power-mode
code --install-extension JakeWilson.vscode-cdnjs
code --install-extension ms-python.python
code --install-extension ms-toolsai.jupyter
code --install-extension oderwat.indent-rainbow
code --install-extension shalldie.background
code --install-extension shd101wyy.markdown-preview-enhanced
code --install-extension SirTori.indenticator
code --install-extension vscode-icons-team.vscode-icons     
code --install-extension wholroyd.jinja
```

## 參考資料

1. [How can you export the Visual Studio Code extension list?](https://stackoverflow.com/questions/35773299/how-can-you-export-the-visual-studio-code-extension-list)

   [Ask Question](https://stackoverflow.com/questions/ask)

