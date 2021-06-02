---
description: 說實在的，我也看不懂我之前在寫啥，ㄏㄏ
---

# 一些指令

ui 檔轉 py 檔指令

```text
pyuic5 -x main.ui -o main.py
```

前後端分離檔案 \(透過繼承的方式\)

```python
from PyQt5 import QtCore, QtGui, QtWidgets
from GUI import Ui_MainWindow # 導入前端介面檔案
class MainGUI(QtWidgets.QMainWindow, Ui_MainWindow): # Ui_MainWindow 指的是前端要繼承的class
    def __init__(self, parent = None):
        super(MainGUI, self).__init__(parent) 
        self.setupUi(self)
    
if __name__ == "__main__":
    import sys 
    app = QtWidgets.QApplication(sys.argv)
    # MainWindow = QtWidgets.QMainWindow() 
    ui = MainGUI() 
    # ui.setupUi(MainWindow) 
    ui.show() 
    sys.exit(app.exec_())
```

使用 QThread 時，因為 class 不同，所以如果要取得 GUI 的物件，使用 ui \(介面的名稱\).object

## MVC 

{% tabs %}
{% tab title="main.py" %}
```python
from PyQt5 import QtWidgets
import sys
from controller import controller

if __name__ == "__main__":
    app = QtWidgets.QApplication([])    
    ctr = controller.Controller()
    
    app.exec_()
```
{% endtab %}

{% tab title="model.py" %}
```python
class Model:
    def __init__(self):
        pass
```
{% endtab %}

{% tab title="view.py" %}
```python
from PyQt5 import QtWidgets
from PyQt5.QtGui import QIcon, QPixmap
from PyQt5.QtCore import Qt

class View(QtWidgets.QWidget):
    def __init__(self):
        super(View, self).__init__()
        
        self.init()

    def init(self):
        self.label = QtWidgets.QLabel(self)
        self.label.setText("HERE")
```
{% endtab %}

{% tab title="controller.py" %}
```python
from view import view
from model import model

class Controller:
    def __init__(self):
        self.view = view.View()
        self.model = model.Model()
        self.view.show()
```
{% endtab %}
{% endtabs %}

## 隱藏視窗（保留物件）

```python
from PyQt5 import QtWidgets
from PyQt5.QtGui import QIcon, QPixmap
from PyQt5.QtCore import Qt

class View(QtWidgets.QWidget):
    def __init__(self):
        super(View, self).__init__()
        
        self.init()

    def init(self):
        self.label = QtWidgets.QLabel(self)
        self.label.setText("HERE")
        
        self.setAttribute(Qt.WA_TranslucentBackground, True)
        self.setWindowFlags(Qt.FramelessWindowHint)
```

## 參考資料

1. [PyQt5之MVC模式\_peixin\_huang的博客-CSDN博客](https://blog.csdn.net/peixin_huang/article/details/104309003)
2. [【转】python--pyqt窗体背景透明的两种应用\_安先生还是没名字的博客-CSDN博客\_python窗体背景透明](https://blog.csdn.net/qiaokelinaicha/article/details/71914833)

