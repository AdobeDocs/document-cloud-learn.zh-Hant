---
title: 建立嵌入式電子簽名和文件體驗
description: 瞭解如何使用 Acrobat Sign API 將電子簽名和文件體驗內嵌到您的網頁平臺和內容及檔管理系統
feature: Integrations, Workflow
role: Developer
level: Intermediate
topic: Integrations
jira: KT-7489
thumbnail: KT-7489.jpg
kt: 7489
exl-id: db300cb9-6513-4a64-af60-eadedcd4858e
source-git-commit: 0a299592f0616988b6208fc98d3140f4ac22057e
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 0%

---

# 建立嵌入式電子簽名和文件體驗

瞭解如何使用 Acrobat Sign API 將電子簽名和文件體驗內嵌到您的網頁平臺和內容及檔管理系統中。 此實作教學課程有四個部分。

## 第 1 部分：您需要的

第 1 部分中，瞭解如何開始使用第 2 至 4 部分所需的一切。 讓我們先取得API認證。

+++檢視如何取得API認證的詳細資訊

* [Acrobat Sign 開發人員帳戶](https://www.adobe.com/acrobat/business/developer-form.html)
* [入門代碼](https://github.com/benvanderberg/adobe-sign-api-tutorial)
* [VS Code （或您選擇的編輯器）](https://code.visualstudio.com)
* Python 3.x
   * Mac — Homebrew
   * Linux — 內建安裝程式
   * Windows — 卡西擁
   * 全部 — https://www.python.org/downloads/

+++

## 第2部分：低/無程序代碼 — 網頁表單的功能

第2部分中，探索使用網頁窗體的低/無程式代碼選項。 最好一開始看看是否可以避免寫下程序代碼。

+++檢視如何建立網頁窗體的詳細資訊

1. 使用開發人員帳戶存取 Acrobat Sign。

1. 選取 **首頁上的「發佈網頁表單** 」。

   ![Sign 首頁Acrobat螢幕擷圖](assets/embeddedesignature/embed_1.png)

1. 建立您的合約。

   ![如何建立網頁窗體的螢幕擷圖](assets/embeddedesignature/embed_2.png)

1. 將您的合約嵌入平面 HTML 頁面上。

1. 嘗試動態新增查詢參數。

   ![新增查詢參數的螢幕擷圖](assets/embeddedesignature/embed_3.png)

+++

## 第3部分：以表單傳送合約及合併數據

第 3 部分可動態建立合約。

+++檢視有關如何動態建立合約的詳細資訊

首先，您需要建立存取權。 使用 Acrobat Sign，您可以透過兩種方式透過 API 進行連線。 OAuth 令牌與整合密鑰。 除非您有在應用程式中使用 OAuth 的明確原因，否則您應該先探索整合密鑰。

1. 在「帳戶」索引標籤下方的&#x200B;**「API資訊**」選單&#x200B;**&#x200B;**&#x200B;中，選&#x200B;**取「Acrobat Sign」中的「整合密鑰**」。

   ![哪裡可以找到整合密鑰的螢幕擷圖](assets/embeddedesignature/embed_4.png)

既然您已經擁有訪問許可權並且可以與API互動，請看看您可以使用API做些什麼。

1. 流覽至「 [Acrobat 6 版方法](http://adobesign.com/public/docs/restapi/v6)API Sign REST。

   ![導覽Acrobat Sign REST API 6 版方法的螢幕擷圖](assets/embeddedesignature/embed_5.png)

1. 將字元當做「持有人」值使用。

   ![持有人值的螢幕擷圖](assets/embeddedesignature/embed_6.png)

若要傳送第一份合約，最好瞭解如何使用API。

1. 建立暫時性文件並傳送。

>[!NOTE]
>
>JSON 請求呼叫具有「模型」和「最小模型結構」選項。 這提供規格和最低裝載集。

![建立暫時性文件的螢幕擷圖](assets/embeddedesignature/embed_7.png)

第一次傳送合約后，您準備好加入邏輯。 建立一些輔助程式來減少重複性始終是個好主意。 以下是一些範例：

**驗證**

![驗證邏輯的螢幕擷圖](assets/embeddedesignature/embed_8.png)

**標頭/驗證**

![標題/驗證邏輯的螢幕擷圖](assets/embeddedesignature/embed_9.png)

**基本 URI**

![基本 URI 邏輯的螢幕擷圖](assets/embeddedesignature/embed_10.png)

了解暫時性檔在 Sign 生態系統的巨集大配置中所處的位置。暫時性 -> 合約
暫時性 -> 範本 ->合約
暫時性 -> Widget ->合約

本範例使用範本作為檔來源。 這通常是最佳途徑，除非您有充分的理由動態產生檔以供簽署 （例如舊有程式代碼或文件產生）。

程式代碼相當簡單;它會使用檔來源的資料庫檔 （範本）。 系統會動態指派第一位和第二位簽署者。 狀態 `IN_PROCESS` 表示檔會立即傳送。 此外， `mergeFieldInfo` 也可用來動態填滿欄位。

![可動態新增簽名的程式代碼螢幕擷圖](assets/embeddedesignature/embed_11.png)

+++

## 第4部分：嵌入簽署體驗、重新導向等

在許多情況下，您可能會希望允許觸發參與者立即簽署合約。 這對於面向客戶的應用程式和販賣亭很實用。

++檢視如何嵌入簽署體驗的詳細資訊

如果您不希望第一個傳送電子郵件觸發，管理行為的方法很簡單，就是修改API呼叫。

![不觸發傳送電子郵件的程式代碼螢幕擷圖](assets/embeddedesignature/embed_12.png)

以下說明如何控制簽署後重新導向：

![可控制簽署後重新導向的程式代碼螢幕擷圖](assets/embeddedesignature/embed_13.png)

更新合約建立程式後，最後一個步驟是產生簽署URL。 此呼叫也相當簡單，並產生簽署者可用來存取其部分簽署程式的URL。

![產生簽署者URL的程式代碼螢幕擷圖](assets/embeddedesignature/embed_14.png)

>[!NOTE]
>
>請注意，合約建立呼叫在技術上是異步的。 這表示可以進行「POST」合約呼叫，但合約尚未準備就緒。 最佳做法是建立重試迴圈。 使用重試或任何適合您環境的最佳做法。

![屏幕截圖顯示建立重試迴圈是最佳做法](assets/embeddedesignature/embed_15.png)

一切整合在一起，解決方案就相當簡單。 您正在製作合約，然後產生簽署URL讓簽署者點選並開始簽署指派。

+++

## 其他主題

* [JS 事件](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/events.md)
* Webhook 活動
   * [REST API](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/webhooks/createWebhook)
   * [Acrobat Sign v6 中的 Webhook](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/webhooks.md)
* [重新啟動要求電子郵件 （含事件）](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/updateAgreement)
* [以「重試」取代逾時](https://stackoverflow.com/questions/23267409/how-to-implement-retry-mechanism-into-python-requests-library)
* 自訂提醒
   * 透過初始建立

     ![導覽至 Power Automate 的螢幕擷圖](assets/embeddedesignature/embed_16.png)

   * 或在飛行中新增一個[&#128279;](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/createReminderOnParticipant)
