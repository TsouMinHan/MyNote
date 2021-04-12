---
description: >-
  使用 Google Scheduler 排定時程觸發 Pub/Sub  去執行 Cloud Function
  的任務。我的理解是這樣啦，應該差不多是這個意思。
---

# Google 定時排程

## 建立 Pub/Sub 主題

進入 Pub/Sub &gt; 建立主題 &gt; 輸入 ID，例如：Job1。

## 建立 Cloud Scheduler 

進入 Cloud Scheduler &gt; 輸入名稱、頻率、時區（ / 代表每Ｘ做一次）、類型（選 Pub/Sub）&gt; 選擇一個 Pub/Sub 主題，例如：Job1 &gt; 酬載（我不知道是什麼）跟主題一樣。

## 建立 Cloud Function

建立函式 &gt; 填一些基本內容 &gt; 下一步，選擇自己要的程式語言 &gt; 上傳 zip 檔案，記得主程式要用 main（Python），要執行的函式要帶入 event, content 參數。

