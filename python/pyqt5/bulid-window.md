---
description: 說實在的，我也看不懂我之前在寫啥，ㄏㄏ
---

# 建立視窗

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

