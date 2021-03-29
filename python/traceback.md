---
description: >-
  記錄一下 traceback 套件的指令，會顯示詳細的錯誤訊息，在 debug
  時很方便，有許多的指令，但我看不太懂介紹，測試幾個指令之後覺得就只是顯示錯誤的訊息數量跟形式不太一樣，所以我就只記下我覺得好用的指令，其實也就一個而已，但是要用的時候總是會忘記。
---

# traceback 套件



在`try/except`時使用起來很方便。

正常情況下：

```python
try:
    int("asd")
except Exception as e:
    print(e)
```

```bash
invalid literal for int() with base 10: "asd"
```

使用`traceback`：

```python
import traceback


try:
    int("asd")
except Exception as e:
    traceback.print_exc(e)
```

```bash
Traceback (most recent call last):
  File "d:\pyCharm\test\test.py", line 5, in <module>
    int("asd")
ValueError: invalid literal for int() with base 10: "asd"

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "D:\python\lib\runpy.py", line 193, in _run_module_as_main
    "__main__", mod_spec)
  File "D:\python\lib\runpy.py", line 85, in _run_code
    exec(code, run_globals)
  File "c:\Users\tsou\.vscode\extensions\ms-python.python-2020.5.86398\pythonFiles\lib\python\debugpy\wheels\debugpy\__main__.py", line 45, in <module>
    cli.main()
  File "c:\Users\tsou\.vscode\extensions\ms-python.python-2020.5.86398\pythonFiles\lib\python\debugpy\wheels\debugpy/..\debugpy\server\cli.py", line 430, in main
    run()
  File "c:\Users\tsou\.vscode\extensions\ms-python.python-2020.5.86398\pythonFiles\lib\python\debugpy\wheels\debugpy/..\debugpy\server\cli.py", line 267, in run_file
    runpy.run_path(options.target, run_name=compat.force_str("__main__"))
  File "D:\python\lib\runpy.py", line 263, in run_path
    pkg_name=pkg_name, script_name=fname)
  File "D:\python\lib\runpy.py", line 96, in _run_module_code
    mod_name, mod_spec, pkg_name, script_name)
  File "D:\python\lib\runpy.py", line 85, in _run_code
    exec(code, run_globals)
  File "d:\pyCharm\test\test.py", line 7, in <module>
    traceback.print_exc(e)
  File "D:\python\lib\traceback.py", line 163, in print_exc
    print_exception(*sys.exc_info(), limit=limit, file=file, chain=chain)
  File "D:\python\lib\traceback.py", line 104, in print_exception
    type(value), value, tb, limit=limit).format(chain=chain):
  File "D:\python\lib\traceback.py", line 508, in __init__
    capture_locals=capture_locals)
  File "D:\python\lib\traceback.py", line 337, in extract
    if limit >= 0:
TypeError: ">=" not supported between instances of "ValueError" and "int"
```

可以很明確的知道哪個檔案的第幾行程式出問題。

## 參考資料

1. [traceback — Print or retrieve a stack traceback¶](https://docs.python.org/3/library/traceback.html)

