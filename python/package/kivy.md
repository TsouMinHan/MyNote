---
description: python app 測試，玩玩看而已。
---

# kivy

## 執行程式

建立視窗並放一顆按鈕。

```python
from kivy.app import App
from kivy.uix.button import Button

class ButtonApp(App):
    def build(self):
        return Button()

    def on_press_button(self):
        print("You pressed the button!")

if __name__ == "__main__":
    app = ButtonApp()
    app.run()
```

## 打包成apk

在 `colab` 上打包，也可以在自己的電腦安裝環境，但我覺得太麻煩了。這個方法是爬[文章](https://towardsdatascience.com/3-ways-to-convert-python-app-into-apk-77f4c9cd55af)找到的，裡面也有提供其他方法，但沒有多加講解指令的意義，我自己是使用 colab 打包，記得要安裝 kivy 套件。

```bash
!pip install buildozer

!pip install cython==0.29.19

!sudo apt-get install -y \
    python3-pip \
    build-essential \
    git \
    python3 \
    python3-dev \
    ffmpeg \
    libsdl2-dev \
    libsdl2-image-dev \
    libsdl2-mixer-dev \
    libsdl2-ttf-dev \
    libportmidi-dev \
    libswscale-dev \
    libavformat-dev \
    libavcodec-dev \
    zlib1g-dev

!sudo apt-get install -y \
    libgstreamer1.0 \
    gstreamer1.0-plugins-base \
    gstreamer1.0-plugins-good

!sudo apt-get install build-essential libsqlite3-dev sqlite3 bzip2 libbz2-dev zlib1g-dev libssl-dev openssl libgdbm-dev libgdbm-compat-dev liblzma-dev libreadline-dev libncursesw5-dev libffi-dev uuid-dev libffi6

!sudo apt-get install libffi-dev

!buildozer init

!buildozer -v android debug

!buildozer android clean
```

## 參考資料

1. [Build a Mobile Application With the Kivy Python Framework – Real Python](https://realpython.com/mobile-app-kivy-python/#packaging-your-app-for-android)
2. [3 Ways to Convert Python App into APK \| by Kaustubh Gupta \| Towards Data Science](https://towardsdatascience.com/3-ways-to-convert-python-app-into-apk-77f4c9cd55af)

