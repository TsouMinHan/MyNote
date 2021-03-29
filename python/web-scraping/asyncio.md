---
description: 紀錄一下自己在使用 `asyncio` 的程式碼，下次要用時可以直接複製過去修改。
---

# asyncio 同步執行、下載圖片

## 同步執行

```python
import asyncio
import time

async def some_function(s): 
    await time.sleep(3)
    print(s)

async def acync_thread(s, q):
    while True:
        page = await q.get()
        await some_function(s)
        q.task_done()

async def put_to_queue(q, page):
    await q.put(page)

async def start_async(pages):
    q = asyncio.Queue(maxsize=2)

    producers = [asyncio.create_task(put_to_queue(q, page)) for page in range(1, pages)]
    consumers = [asyncio.create_task(acync_thread("str", q)) for _ in range(1, pages)]

    await asyncio.gather(*producers)
    await q.join()

    for c in consumers:
        c.cancel()

asyncio.run(start_async(pages))
```

## 同步下載圖片

```python
import aiohttp, aiofiles

async with aiohttp.ClientSession() as session:
    async with session.get(download_url) as resp:        
        if resp.status == 200:
            f = await aiofiles.open('{}/{}.jpg'.format(path, page), mode='wb')
            await f.write(await resp.read())
            await f.close()
```

