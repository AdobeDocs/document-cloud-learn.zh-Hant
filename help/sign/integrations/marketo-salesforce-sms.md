---
title: 使用適用於 Salesforce 和 Marketo 的 Acrobat Sign 傳送通知
description: 瞭解如何傳送簡訊、電子郵件或推送通知，讓簽署者知道合約即將推出
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
jira: KT-7247
topic: Integrations
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: ac3334ec-b65f-4ce4-b323-884948f5e0a6
source-git-commit: 51d1a59999a7132cb6e47351cc39a93d9a38eaeb
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# 使用 Acrobat Sign 針對 [!DNL Salesforce] 和 [!DNL Marketo]

瞭解如何使用 Acrobat Sign、Acrobat Sign for Salesforce、Marketo 和 Marketo Salesforce 同步功能，傳送簡訊、電子郵件或推送通知，讓簽署者知道合約即將推出。 若要從 Marketo 傳送通知，您必須先購買或設定 Marketo SMS 管理功能。 此逐步解說使用 [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/)，但可以使用其他 Marketo SMS 解決方案。

## 必要條件

1. 安裝 Marketo Salesforce 同步。

   如需 Salesforce Sync 的資訊和最新增效模組，請參閱此處 [。](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. 安裝 Acrobat Sign for Salesforce。

   有關此增效模組的資訊請參閱 [這裡。](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## 尋找自定義物件

Marketo Salesforce 同步和 Acrobat Sign for Salesforce 設定完成後，Marketo Admin Terminal 中會出現幾個新選項。

![管理](assets/adminTab.png)

![物件同步](assets/salesforceAdmin.png)

1. 如果這是您第一次這麼做，請按兩下 **「同步結構** 」。 否則，請按下 **「重新整理結構」**。

   ![刷新](assets/refreshSchema1.png)

1. 如果全域同步正在執行，請按兩下「 **停用全域同步」以停用**。

   ![禁用](assets/disableGlobal.png)

1. 按兩下 **「重新整理結構」** 。

   ![重新整理 2](assets/refreshSchema2.png)

## 同步自定義物件

在右側，請參閱「商機」、「聯繫人」和「帳戶型自定義物件」。

**如果您想要在 Salesforce 中將銷售機會新增至合約時觸發，請為「商機」底下的物件啟用同步** 。

**如果您想要在 Salesforce 中將聯繫人新增至合約時觸發「連絡人」，請為「聯繫人」底下的物件啟用同步** 。

**如果您想要在 Salesforce 中將帳戶新增至合約時觸發「帳戶」底下的物件同步** 。

1. **針對所需父級 （「商機」、「聯繫人」或「帳戶」） 下方顯示的自定義物件啟用同步** 。

   ![自訂物件](assets/customObjects.png)

1. 下列資產會顯示如何 **啟用同步**。

   ![自訂同步 1](assets/customObjectSync1.png)

   ![自訂同步 2](assets/customObjectSync2.png)

1. 在啟用「自定義物件」上的同步後，請重新啟用同步。

   ![啟用全域](assets/enableGlobal.png)

## 建立程式

1. 在 Marketo 的「行銷活動」區段中，以滑鼠右鍵按兩下 **左列的「行銷活動** 」，選 **取「新增Campaign資料夾」，然後命名該檔案夾**。

   ![新檔案夾](assets/newFolder.png)

1. 在建立的檔案夾上按下滑鼠右鍵，選取 **「新增程式**」，然後命名。 將其他一切保留為預設值，然後按兩下「 **建立」**。

   ![新方案 1](assets/newProgram1.png)

   ![新方案 2](assets/newProgram2.png)

## 設定 Twilio SMS

請先確認您擁有有效 Twilio 帳戶，並購買所需的 SMS 功能。

設定 Marketo - Twilio SMS Webhook 需要您的帳戶提供三個 Twilio 參數。

- 帳戶 SID
- 帳戶令牌
- Twilio 電話號碼

從您的帳戶擷取這些參數，現在開啟您的 Marketo 實例。

1. **按下右上方的「管理員**」。

   ![管理](assets/adminTab.png)

1. 按兩下「 **Webhook」**，然後按一下「 **新增 Webhook」**。

   ![Webhook](assets/webhooks.png)

1. **輸入 Webhook 名稱**&#x200B;和&#x200B;**說明**。

1. 輸入下列URL，並務必使用您的 Twilio 認證取代 **[ACCOUNT_SID]** 和 **[AUTH_TOKEN]** 。

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. 選 **取「POST** 」做為您的「要求」類型。

1. 輸入下列&#x200B;**範本**，並務必將 MY_TWILIO_NUMBER ]**替換**[&#x200B;為 Twilio 電話號碼，YOUR_MESSAGE **[]**&#x200B;您選擇的訊息。

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. 將「要求令牌編碼」設為「表格/URL」。

1. 將回應類型設為 JSON，然後按兩下「儲存 **」**。

## 設定智慧型手機Campaign觸發程式

1. 在「行銷活動」區段中，在您建立的程式上按下滑鼠右鍵，然後選取「 **新增智慧型手機Campaign**」。

   ![智慧型Campaign 1](assets/smartCampaign1.png)

1. 命名，然後按兩下「 **建立」**。

   ![智慧型Campaign 2](assets/smartCampaign3.png)

   如果「自定義物件同步」的設定已正確完成，您應該會在 Salesforce 檔案夾下方看到下列可供使用的觸發。

1. 按兩下並拖曳「新增至合約」至智慧型清單。 新增觸發時您希望擁有的任何限制。

   ![新增至合約 2](assets/addedToAgreement2.png)

## 設定智慧型手機Campaign流程

1. 按兩下智慧型手機Campaign **中的「流程** 」索引標籤。 Search，將「呼叫 Webhook **」流程拖**&#x200B;曳到畫布上，然後選取您在上一個區段中建立的 Webhook。

   ![呼叫 Webhook](assets/callWebhook.png)

1. 現在已為新增至合約的潛在客戶設定SMS通知營銷活動。
