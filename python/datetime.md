# datetime

## 取得時間

```python
# get datetime by timestamp datetime.datetime(2021, 3, 10, 0, 0)
datetime.fromtimestamp(1615305600) 
```

## 轉換型態

```python
# datetime to string
datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")

# string to datetime
datetime.datetime.strptime("2014-12-31 18:20:10", "%Y-%m-%d %H:%M:%S")
```

## 天數相加

```python
datetime.date.today() + datetime.timedelta(days=1)
```

## 計算時間差

```python
(datetime.datetime(2015,1,13,12,0,0) - datetime.datetime.now()).total_seconds()
(datetime.datetime(2015,1,13,12,0,0) - datetime.datetime.now()).days
(datetime.datetime(2015,1,13,12,0,0) + datetime.timedelta(days=1)  
(datetime.datetime(2015,1,13,12,0,0) + datetime.timedelta(minutes=5)  
(datetime.datetime(2015,1,13,12,0,0) + datetime.timedelta(seconds=60)  
(datetime.datetime(2015,1,13,12,0,0) + datetime.timedelta(days=1,minutes=5)
```

## 轉換時區

```python
from datetime import datetime
import pytz

d = datetime.today()
#create Taipei timezone
tw = pytz.timezone('Asia/Taipei')

#set d timezone is 'Asia/Taipei'
twdt = tw.localize(d)

#change to utc time
utc_dt = twdt.astimezone(pytz.utc)
```

第二個方法算是用手動方式自己加上時間

```python
from datetime import datetime, timezone, timedelta

# 設定為 +8 時區
tz = timezone(timedelta(hours=+8))

# 取得現在時間、指定時區、轉為 ISO 格式
datetime.now(tz).isoformat()
```

有轉換時區跟沒轉換時區的做運算可能會出問題，把時區弄掉就好

```python
tw.localize(d).replace(tzinfo=None)
```

## 參考資料

1. [\[Python 3\] 產生 ISO 8601 含時區格式的現在時間（不透過 pytz） \| 小克's 部落格](https://blog.goodjack.tw/2020/04/create-datetime-with-timezone-via-python3-without-pytz.html)

