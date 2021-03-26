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

轉換時區

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

有轉換時區跟沒轉換時區的做運算可能會出問題，把時區弄掉就好

```python
tw.localize(d).replace(tzinfo=None)
```

