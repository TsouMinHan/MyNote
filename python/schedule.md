---
description: schedule 是個簡單的排程工具，但僅適用於簡單的工作，需要精確的時間、多線程等問題不建議使用。
---

# schedule 套件

## 安裝

```bash
pip install schedule
```

## 設定工作

```python
def job():
    print("I'm working...")

schedule.every(10).seconds.do(job)
schedule.every(10).minutes.do(job)
schedule.every().hour.do(job)
schedule.every().day.at("10:30").do(job)
schedule.every(5).to(10).minutes.do(job)
schedule.every().monday.do(job)
schedule.every().wednesday.at("13:15").do(job)
schedule.every().minute.at(":17").do(job)

schedule.clear() # clear all job

while True:
    schedule.run_pending()
    time.sleep(1)
```

## 參考資料

1. \*\*\*\*[**schedule**](https://schedule.readthedocs.io/)\*\*\*\*

