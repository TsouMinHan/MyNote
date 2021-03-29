---
description: 記下一些自己不常用或者常常會忘記的指令
---

# BeautifulSoup

## 取得 parent tag

```python
"""
<a href="..."> 
    <span>child</span>
</a>
"""
for ele in soup.select("span"):
    print(ele.text)
    print(urllib.parse.urljoin(pre_url, ele.parent["href"]))
```

