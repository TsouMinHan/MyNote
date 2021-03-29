---
description: 紀錄 logging 套件
---

# logging 套件

### 安全等級

#### 預設安全等級

| 等級 | 說明 | 數值 | 輸出函式 |
| :--- | :--- | :--- | :--- |
| NOTEST |  | 0 |  |
| DEBUG | 除錯 | 10 | logging.debug\(\) |
| INFO | 訊息 | 20 | logging.info\(\) |
| WARNING | 警告 | 30 | logging.warning\(\) |
| ERROR | 錯誤 | 40 | logging.error\(\) |
| CRITICAL | 嚴重錯誤 | 50 | logging.critical\(\) |

#### 自訂安全等級

```python
logging.addLevelName(35, "test")
print(logging.getLevelName("test")) # 35
```

### 輸出訊息

預設輸出等級是 `warning` ，大於等於 `warning` 數值的等級才會被記錄下來。  
可以透過 `basicConfig` 設定輸出等級。

```python
import logging

# logging.basicConfig(level=logging.DEBUG)

logging.debug("debug message")
logging.info("info message")
logging.warning("warning message")
logging.error("error message")
logging.critical("critical message")

# DEBUG:root:debug message                                                                                               
# INFO:root:info message                                                                                                            
# WARNING:root:warning message                                                                                                      
# ERROR:root:error message                                                                                                          
# CRITICAL:root:critical message
```

### 自訂 logging 輸出的格式

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x683C;&#x5F0F;</th>
      <th style="text-align:left">&#x8AAA;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">%(asctime)s</td>
      <td style="text-align:left">
        <p>&#x7576; LogRecord &#x5EFA;&#x7ACB;&#x6642;&#x7684;&#x6642;&#x9593;&#x683C;&#x5F0F;&#xFF0C;&#x4F8B;&#x5982;&#xFF1A;2021-03-27
          18:30:54,896</p>
        <p>&#xFF08;&#x9017;&#x865F;&#x5F8C;&#x9762;&#x70BA;&#x6BEB;&#x79D2;&#xFF09;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">%(created)f</td>
      <td style="text-align:left">&#x7576; LogRecord &#x5EFA;&#x7ACB;&#x6642;&#x7684;&#x6642;&#x9593;&#x6233;</td>
    </tr>
    <tr>
      <td style="text-align:left">%(filename)s</td>
      <td style="text-align:left">&#x6A94;&#x540D;&#xFF08;&#x542B;&#x526F;&#x6A94;&#x540D;&#xFF09;</td>
    </tr>
    <tr>
      <td style="text-align:left">%(funcName)s</td>
      <td style="text-align:left">&#x51FD;&#x5F0F;&#x540D;&#x7A31;</td>
    </tr>
    <tr>
      <td style="text-align:left">%(levelname)s</td>
      <td style="text-align:left">&#x5B89;&#x5168;&#x7B49;&#x7D1A;&#xFF08;&#x6587;&#x5B57;&#xFF09;</td>
    </tr>
    <tr>
      <td style="text-align:left">%(levelno)s</td>
      <td style="text-align:left">&#x5B89;&#x5168;&#x7B49;&#x7D1A;&#xFF08;&#x6578;&#x5B57;&#xFF09;</td>
    </tr>
    <tr>
      <td style="text-align:left">%(lineno)d</td>
      <td style="text-align:left">&#x884C;&#x6578;</td>
    </tr>
    <tr>
      <td style="text-align:left">%(message)s</td>
      <td style="text-align:left">&#x8A0A;&#x606F;</td>
    </tr>
    <tr>
      <td style="text-align:left">%(module)s</td>
      <td style="text-align:left">&#x6A21;&#x7D44;&#x540D;&#x7A31;&#xFF08;&#x6C92;&#x526F;&#x6A94;&#x540D;&#xFF09;</td>
    </tr>
    <tr>
      <td style="text-align:left">%(msecs)d</td>
      <td style="text-align:left">&#x7576; LogRecord &#x5EFA;&#x7ACB;&#x6642;&#x7684;&#x6BEB;&#x79D2;</td>
    </tr>
    <tr>
      <td style="text-align:left">%(name)s</td>
      <td style="text-align:left">logger &#x7684;&#x540D;&#x7A31;</td>
    </tr>
    <tr>
      <td style="text-align:left">%(pathname)s</td>
      <td style="text-align:left">&#x8DEF;&#x5F91;</td>
    </tr>
    <tr>
      <td style="text-align:left">%(process)d</td>
      <td style="text-align:left">process &#x7684; ID</td>
    </tr>
    <tr>
      <td style="text-align:left">%(processName)s</td>
      <td style="text-align:left">process &#x7684;&#x540D;&#x7A31;</td>
    </tr>
    <tr>
      <td style="text-align:left">%(relativeCreated)d</td>
      <td style="text-align:left">&#x76F8;&#x5C0D;&#x65BC; LogRecord &#x5EFA;&#x7ACB;&#x6642;&#x7684;&#x6BEB;&#x79D2;&#x6578;&#xFF08;&#x73FE;&#x5728;
        - &#x7576;&#x6642;&#xFF09;</td>
    </tr>
    <tr>
      <td style="text-align:left">%(thread)d</td>
      <td style="text-align:left">thread &#x7684; ID</td>
    </tr>
    <tr>
      <td style="text-align:left">%(threadName)s</td>
      <td style="text-align:left">thread &#x7684;&#x540D;&#x7A31;</td>
    </tr>
  </tbody>
</table>

### 時間格式

| 參數 | 說明 |
| :--- | :--- |
| %Y | 長年份，例如：2021 |
| %y | 短年份，例如：21 |
| %m | 月份 01~12 |
| %b | 完整月份名稱，例如：March |
| %B | 月份名稱縮寫，例如：Mar |
| %d | 日期 01~31 |
| %H | 小時 00~23 |
| %I | 小時 01~12 |
| %w | 星期 0~6 \(0=星期日\) |
| %A | 完整星期名稱，例如：Friday |
| %a | 星期名稱縮寫，例如：Fri |
| %P | PM 或 AM |
| %M | 分鐘 00~59 |
| %S | 秒 00~59 |

### Handler

可以自己定義記錄器，用於不同的情況下使用。

```python
import logging

# 設定記錄器名稱
logger = logging.getLogger(__name__)

# StreamHandler 在 terminal 顯示的，FileHandler 儲存在檔案的
stream_handler = logging.StreamHandler()
file_handler = logging.FileHandler("log.txt")

stream_handler.setLevel(logging.INFO)
file_handler.setLevel(logging.INFO)

stream_formater = logging.Formatter("%(asctime)s | %(levelname)s | Line: %(lineno)d | %(message)s")
file_formater = logging.Formatter("%(asctime)s | %(levelname)s | %(message)s")

stream_handler.setFormatter(stream_formater)
file_handler.setFormatter(file_formater)

logger.addHandler(stream_handler)
logger.addHandler(file_handler)
```

### 參考資料

&lt;&lt;&lt;&lt;&lt;&lt;&lt; HEAD:python/logging.md 1. [**Python - 日誌 \(logging\) 模組**](https://titangene.github.io/article/python-logging.html) 2. [**Python 學習筆記 : 日誌 \(logging\) 模組測試**](http://yhhuang1966.blogspot.com/2018/04/python-logging_24.html) 3. [**logging — Logging facility for Python**](https://docs.python.org/3/library/logging.html#module-logging) 4. [**Logging in Python - Real Python**](https://realpython.com/python-logging/)

1. \*\*\*\*[**2021 solution, no additional packages required, Python 3**](https://stackoverflow.com/questions/384076/how-can-i-color-python-logging-output)\*\*\*\*
2. \*\*\*\*[**Python - 日誌 \(logging\) 模組**](https://titangene.github.io/article/python-logging.html)\*\*\*\*
3. \*\*\*\*[**Python 學習筆記 : 日誌 \(logging\) 模組測試**](http://yhhuang1966.blogspot.com/2018/04/python-logging_24.html)\*\*\*\*
4. \*\*\*\*[**logging — Logging facility for Python**](https://docs.python.org/3/library/logging.html#module-logging)\*\*\*\*
5. \*\*\*\*[**Logging in Python - Real Python**](https://realpython.com/python-logging/)\*\*\*\*

   &lt;&lt;&lt;&lt;&lt;&lt;&lt; HEAD:python/logging.md

   &lt;&lt;&lt;&lt;&lt;&lt;&lt; HEAD:python/logging.md

   > > > > > > > ## parent of c7a841d \(GitBook: \[master\] one page modified\):python/logging-tao-jian.md
   > > > > > > >
   > > > > > > > ## parent of c7a841d \(GitBook: \[master\] one page modified\):python/logging-tao-jian.md
   > > > > > > >
   > > > > > > > parent of c7a841d \(GitBook: \[master\] one page modified\):python/logging-tao-jian.md

