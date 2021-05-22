---
description: 多年前的使用經驗，當時有留一些簡單的筆記，或許以後有機會用到。
---

# Heroku

## 登入

{% code title="cmd" %}
```text
heroku login
```
{% endcode %}

## 初始化 git \(第一次開啟專案才需要\)

{% code title="cmd" %}
```text
git init 
git config --global user.name "名字"
git config --global user.email "信箱"
```
{% endcode %}

## 用 git 連接 hreoku 專案

{% code title="cmd" %}
```text
heroku git:remote -a HEROKU_APP_NAME
```
{% endcode %}

## 設定 worker 或 web

{% code title="cmd" %}
```text
# 在Procfile打上
# 若是Flask改成web
worker: python script.py

# 上傳之後執行，若要關閉改為0
heroku ps:scale worker=1
```
{% endcode %}

## 將程式碼推上 Heroku

{% code title="cmd" %}
```text
git add .
git commit -m "Add code"
git push -f heroku master 
```
{% endcode %}

## 更新

{% code title="cmd" %}
```text
heroku update
```
{% endcode %}

## 查看 log

```text
heroku logs --tail
```

## 複製到本機

```text
heroku git:clone -a HEROKU_APP_NAME
```

## 查看本月剩餘的 Dyno 扣打

```text
heroku ps -a HEROKU_APP_NAME
```



