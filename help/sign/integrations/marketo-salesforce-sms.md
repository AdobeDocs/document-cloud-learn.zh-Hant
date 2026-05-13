---
title: 使用適用於Salesforce和Marketo的Acrobat Sign傳送通知
description: 瞭解如何傳送簡訊、電子郵件或推播通知，讓簽署者知道協定即將達成
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo Engage, Document Cloud
level: Intermediate
jira: KT-7247
topic: Integrations
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: ac3334ec-b65f-4ce4-b323-884948f5e0a6
TQID: https://experienceleague.adobe.com/ZtQuaoB6MhGUnNA2uZLM2pJxthD-XuhsN7yXI65tTVg
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615id: c1c5fb98-9105-44ed-9df1-9e04d062a784
feature_v2: id: a1028f9a-6dbc-4a4f-adf5-eb9f85a408a6id: b13bd2ad-8e65-49e5-9691-2a0d31067b35id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45
subfeature_v2: id: ea4e3ff5-e7b9-4b4c-a5a0-dc27cc3f4275
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
source-git-commit: d92345097c162b68b9d8405122534371c87c5f1a
workflow-type: tm+mt
source-wordcount: 678
ht-degree: 0%

---

# 使用Acrobat Sign傳送[!DNL Salesforce]和[!DNL Marketo]的通知

瞭解如何使用Acrobat Sign、適用於Salesforce的Acrobat Sign、Marketo和Marketo Salesforce Sync傳送簡訊、電子郵件或推播通知，讓簽署者知道即將達成協定。 若要從Marketo傳送通知，您必須先購買或設定Marketo簡訊管理功能。 此逐步解說使用[Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/)，但其他Marketo SMS解決方案可供使用。

## 必要條件

1. 安裝Marketo Salesforce Sync。

   [此處](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)提供Salesforce Sync的資訊和最新外掛程式。

1. 安裝適用於Salesforce的Acrobat Sign。

   [此處](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)提供此外掛程式的資訊。

## 尋找自訂物件

Marketo Salesforce同步和適用於Salesforce的Acrobat Sign設定完成後，Marketo管理終端機中會顯示數個新選項。

![管理員](assets/adminTab.png)

![物件同步](assets/salesforceAdmin.png)

1. 如果您是第一次，請按一下&#x200B;**同步結構描述**。 否則，請按一下&#x200B;**重新整理結構描述**。

   ![重新整理](assets/refreshSchema1.png)

1. 如果正在執行全域同步處理，請按一下[停用全域同步處理] **來停用。**

   ![停用](assets/disableGlobal.png)

1. 按一下&#x200B;**重新整理結構描述**。

   ![重新整理2](assets/refreshSchema2.png)

## 同步處理自訂物件

在右側，請參閱Lead、Contact和Account型自訂物件。

如果要在Salesforce中將潛在客戶新增至合約時觸發，請在Lead底下為物件&#x200B;**啟用Sync**。

如果要在Salesforce中將連絡人新增至合約時觸發，請在[連絡人]底下的物件&#x200B;**啟用[同步]**。

如果要在Salesforce中將帳號新增至合約時觸發，請為[帳號]下的物件&#x200B;**啟用[同步]**。

1. **啟用所需父項（潛在客戶、連絡人或帳戶）下顯示之自訂物件的同步**。

   ![自訂物件](assets/customObjects.png)

1. 下列資產顯示如何&#x200B;**啟用同步**。

   ![自訂同步處理1](assets/customObjectSync1.png)

   ![自訂同步處理2](assets/customObjectSync2.png)

1. 在自訂物件上啟用同步後，請重新啟用同步。

   ![啟用全域](assets/enableGlobal.png)

## 建立方案

1. 在Marketo的「行銷活動」區段中，以滑鼠右鍵按一下左側列上的&#x200B;**行銷活動**，選取&#x200B;**新增行銷活動資料夾**，然後為其命名。

   ![新資料夾](assets/newFolder.png)

1. 以滑鼠右鍵按一下建立的資料夾，選取&#x200B;**新程式**，然後為其命名。 保留其他專案為預設值，然後按一下[建立]。****

   ![新程式1](assets/newProgram1.png)

   ![新程式2](assets/newProgram2.png)

## 設定Twilio簡訊

首先，請確定您擁有有效的Twilio帳戶，並購買您需要的簡訊功能。

設定Marketo - Twilio SMS webhook需要來自您帳戶的三個Twilio引數。

- 帳戶SID
- 帳戶權杖
- Twilio電話號碼

從您的帳戶擷取這些引數，現在請開啟您的Marketo執行個體。

1. 按一下右上方的&#x200B;**管理員**。

   ![管理員](assets/adminTab.png)

1. 按一下&#x200B;**Webhook**，然後按&#x200B;**新Webhook**。

   ![Webhook](assets/webhooks.png)

1. 輸入&#x200B;**Webhook名稱**&#x200B;和&#x200B;**描述**。

1. 輸入下列URL，並確定以您的Twilio認證取代&#x200B;**[ACCOUNT_SID]**&#x200B;和&#x200B;**[AUTH_TOKEN]**。

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. 選取&#x200B;**POST**&#x200B;作為您的要求型別。

1. 輸入下列&#x200B;**範本**，並確定要將&#x200B;**[MY_TWILIO_NUMBER]**&#x200B;取代為您的Twilio電話號碼，並將&#x200B;**[YOUR_MESSAGE]**&#x200B;取代為您選擇的訊息。

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. 將請求權杖編碼設定為表單/URL。

1. 將回應型別設定為JSON，然後按一下&#x200B;**儲存**。

## 設定Smart Campaign觸發器

1. 在行銷活動區段中，以滑鼠右鍵按一下您建立的方案，然後選取&#x200B;**新增Smart Campaign**。

   ![智慧型行銷活動1](assets/smartCampaign1.png)

1. 將其命名，然後按一下[建立]。****

   ![智慧型行銷活動2](assets/smartCampaign3.png)

   如果「自訂物件同步」的設定正確完成，您應該會在Salesforce資料夾下看到下列可供使用的觸發器。

1. 按一下「加入至協定」，然後拖曳至「智慧清單」。 新增您想要在觸發程式上設定的任何限制。

   ![已新增至合約2](assets/addedToAgreement2.png)

## 設定Smart Campaign流程

1. 按一下Smart Campaign中的&#x200B;**流量**&#x200B;標籤。 搜尋&#x200B;**呼叫Webhook**&#x200B;流程並拖曳至畫布上，然後選取您在上一節中建立的webhook。

   ![呼叫Webhook](assets/callWebhook.png)

1. 您針對新增至協定的潛在客戶的SMS通知行銷活動現已設定。
