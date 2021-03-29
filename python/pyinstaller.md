# 打包成 exe 檔 & 虛擬環境

## 打包

### exe

`pyinstaller -F .\main.py` 打包 執行檔案

 `pyinstaller -F -c .\main.py` 帶 cmd 視窗，結束時會關閉

 `pyinstaller -F -D .\main.py` 將相關檔案打包在同個路徑

### Package

```bash
 pip freeze > requirements.txt
 pip install -r requirements.txt
```

## 虛擬環境

```bash
python -m venv venv # for windows
python3 -m venv venv # for Mac OS
```

在 Mac 環境下建立的環境無法在 windows 上執行，但可以打包套件過去，因為路徑的關係。

## PIP 安裝錯誤

在使用者資料夾下新增檔案，為什麼可以執行我也不知道。

{% tabs %}
{% tab title="Plain Text" %}
{% code title="C:\\Users\\Administrator\\pip\\pip.ini" %}
```text
[global]

trusted-host=mirrors.aliyun.com

index-url=http://mirrors.aliyun.com/pypi/simple/
```
{% endcode %}
{% endtab %}
{% endtabs %}

## 參考資料

1. [python pip 错误 Could not install packages due to an EnvironmentError: HTTPSConnectionPool...](https://blog.csdn.net/weixin_41782332/article/details/103673797)



