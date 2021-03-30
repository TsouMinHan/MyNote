---
description: 為了測試 zkteco 的指紋辨識程式碼，期望能夠在windows環境下執行。
---

# 安裝 window 10 IOT core 在樹莓派 3，並部署範例程式

> Java 沒辦法在 windows 10 IOT core 上執行。

## 燒錄windows 10 IOT core

要使用 windows 10 IOT core 必須使用 windows 10 系統的電腦才可以進行訪問、寫程式、下載等動作。

下載 [windows 10 IOT core dashboard](https://docs.microsoft.com/en-us/windows/iot-core/downloads)，dashboard 提供了燒錄至記憶卡、連線、部署範例程式、檢視裝置等服務。

插入記憶卡、選擇要燒錄的裝置與記憶卡，設定裝置名稱與密碼（連線與部署時使用），按下確定就開始了，另外程式會自動幫你把記憶卡格式化。

## 安裝

將記憶卡插入樹莓派之後開機，照著步驟設定就好了，沒有特別困難。   

## 部署程式

這邊我沒有進行後續測試，因為指紋辨識範例程式執行不起來，但我有使用 dashbord 提供的範例程式進行部署，連線上裝置（點選 APPs &gt; connect 之後就可以用 dashboard 搜尋裝置）之後點一下就可以部署了，非常的方便，結束部署後你可以在樹莓派上發現已經安裝好程式了。

## 參考資料

1. [Windows 10 IOT core dashboard](https://docs.microsoft.com/en-us/windows/iot-core/downloads)
2. [How to Get Windows 10 IoT Core on the Raspberry Pi](https://www.digikey.com/en/maker/blogs/2019/how-to-get-windows-10-iot-core-on-the-raspberry-pi)
3. [使用 Visual Studio 部署應用程式](https://docs.microsoft.com/zh-tw/windows/iot-core/develop-your-app/appdeployment)
4. [GitHub - microsoft/Windows-iotcore-samples: Official code samples repository for Windows 10 Internet of Things \(IoT\)](https://github.com/microsoft/Windows-iotcore-samples)

