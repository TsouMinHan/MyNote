---
description: >-
  Selenium
  是一個可以模擬網頁操作的套件，可以用在爬蟲或者是自動化操作上，自己使用的經驗覺得很方便。因為常常忘記相關指令，所以在這邊記錄一下我自己學到的相關操作。
---

# Selenium 相關操作

## 安裝套件

Windows：`pip install seleniun`

Mac：`pip3 install selenium`

## 下載模擬器

有 Firefox、Chrome 的，我這邊是使用 Chrome，[下載網址](https://chromedriver.chromium.org/downloads)。

下載之後放到 python.exe 的資料夾中（Mac 是在 bin 路徑下，Windows 是在 Script 路徑下），或者在程式中指定路徑。

## 導入與宣告物件

```python
from selenium import webdriver 
from selenium.webdriver.chrome.options import Options # 用來設定模擬器相關設定

chrome_options = Options()
chrome_options.add_argument("--headless") # 隱藏式窗
driver = webdriver.Chrome(chrome_options=chrome_options) 
# 我把driver放在python/Scripts路徑下，所以沒有設路徑，不然的話要設路徑。
# driver = webdriver.Chrome(executable_path="path/her/chromedriver.exe", ... )
```

## 網頁操作

```python
driver.get("your url")  # 進入網頁
driver.page_source # 網頁的內容
driver.quit()      # 關閉模擬器
```

就算程式結束執行了，模擬器還是不會關閉，如果隱藏模擬器的話記得使用`quit()`，不然會像我一樣開了十幾二十個模擬器出來，電腦差點當機。

## 找網頁中元件

注意！使用的是 `find_element` 還是 `find_enements` 有 s 的會回傳串列。

```python
driver.find_element_by_name("name")
driver.find_element_by_id("id") # 沒 s 回傳物件

driver.find_elements_by_id("id") # 有 s 回傳串列
```

## 按鈕操作

```python
driver.find_element_by_name("name").click()
```

## 鍵盤操作

```python
from selenium.webdriver.common.keys import Keys

# 按下 enter
driver.find_element_by_name("Value").send_keys(Keys.RETURN)
# 打出 hello，可以用在 input 輸入使用 
driver.find_element_by_name("name").send_keys("hello")
```

## 清除 input

```python
driver.find_element_by_name("input").clear()
```

## 截圖

網路找到的方法，詳情請看參考資料 \[1\]。

```python
driver.save_screenshot("screenshot.png")
```

## 關閉 alert 

網路找到的方法，詳情請看參考資料 \[1\]。

```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

WebDriverWait(driver, 10).until(EC.alert_is_present())
driver.switch_to.alert.accept()
```

## 使用 JavaScript 尋找元件

透過這個方法可以修改 input 的 value。

```python
driver.execute_script("document.getElementById('id').value = 'abc'")

```

## 參考資料

1. \*\*\*\*[**How to Click the “OK” Button within an Alert using Python + Selenium**](https://stackoverflow.com/questions/61859356/how-to-click-the-ok-button-within-an-alert-using-python-selenium)
2. [Download image with selenium python](https://stackoverflow.com/questions/17361742/download-image-with-selenium-python)
3. [How to send a date directly as text to a calendar control with readonly attribute using Selenium through Python?](https://stackoverflow.com/questions/57449375/how-to-send-a-date-directly-as-text-to-a-calendar-control-with-readonly-attribut) 

