---
description: 從教學文章中擷取重點部分
---

# cors

出現 CORS 的錯誤代表跨來源呼叫 API，會出現這錯誤是基於安全性的問題。

在瀏覽器上面，CORS 限制的其實是「拿不到 response」，而不是「發不出 request」

在 response 的 header 中加入 `Access-Control-Allow-Origin` 代表欲開放的 origin，只能開放一個來源或者是 `*`

`no-cors` 意思並不是「繞過 cors 拿到資料」，而是「我知道它過不了 cors，但我沒差，所以不要給我錯誤也不要給我 response」

CORS request 分成兩種：簡單請求與非簡單請求，無論是哪一種，後端都需要給 `Access-Control-Allow-Origin` 這個 header。 而最大的差別在於非簡單請求在發送正式的 request 之前，會先發送一個 preflight request，如果 preflight 沒有通過，是不會發出正式的 request 的。 簡單來說，preflight 就是一個驗證機制

跨來源的請求，預設是不會帶 cookie 的，request header 要帶 `credentials: 'include'`，且如果要帶上 cookie 的話，那 `Access-Control-Allow-Origin` 不能是 `*`，一定要明確指定 origin。因為安全性的關係，強制你如果要帶上 cookie，後端一定要明確指定是哪個 origin 有權限。除此之外，後端還要額外帶上 `Access-Control-Allow-Credentials: true` 這個 header。

無論有沒有想要存取 Cookie，都會建議 `Access-Control-Allow-Origin` 不要設定成 `*` 而是明確指定 origin，避免預期之外的 origin 跨站存取資源。若是你有多個 origin 的話，建議在後端有一個 origin 的清單，判斷 request header 內的 origin 有沒有在清單中，有的話就設定 `Access-Control-Allow-Origin`，沒有的話就不管它。

要存取 CORS response 的 header，尤其是自定義的 header 的話，後端要多帶一個 `Access-Control-Expose-Headers` 的 header，這樣前端才拿得到

當你拿到跨來源的 response 的時候，基本上都可以拿到 response body，也就是內容。但是 header 就不一樣了，只有幾個基本的 header 可以直接拿到，例如說 `Content-Type` 就是一個。

如果前端要使用 `GET`、`HEAD` 以及 `POST` 以外的 HTTP method 發送請求的話，後端的 preflight response header 必須有 `Access-Control-Allow-Methods` 並且指定合法的 method，preflight 才會通過，瀏覽器才會把真正的 request 發送出去。

reflight request 的數量實在是太多了，而且就算同一個使用者已經預檢過了，每次都還是需要再檢查，其實滿浪費效能的，後端 header `Access-Control-Max-Age`，可以跟瀏覽器說這個 preflight response 能夠快取幾秒，這段時間內都直接沿用快取。

## 參考資料

1. [CORS 完全手冊（一）：為什麼會發生 CORS 錯誤？ - Huli](https://blog.huli.tw/2021/02/19/cors-guide-1/)

