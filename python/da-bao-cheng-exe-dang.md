# 打包成 exe 檔 & 虛擬環境

## 打包

`pyinstaller -F .\main.py` 打包 執行檔案

 `pyinstaller -F -c .\main.py` 帶 cmd 視窗，結束時會關閉

 `pyinstaller -F -D .\main.py` 將相關檔案打包在同個路徑

## 虛擬環境

在 Mac 環境下建立的環境無法在 windows 上執行，但可以打包套件過去。

