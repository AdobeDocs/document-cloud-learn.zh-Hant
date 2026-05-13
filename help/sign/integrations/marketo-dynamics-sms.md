---
title: 使用適用於Microsoft Dynamics 365和Marketo的Acrobat Sign傳送通知
description: 瞭解如何傳送簡訊、電子郵件或推播通知，讓簽署者知道協定即將達成
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo Engage, Document Cloud
level: Intermediate
topic: Integrations
topic-revisit: Integrations
jira: KT-7249
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
TQID: https://experienceleague.adobe.com/J-UO0MiY9BG6zt7UcwxYTupl00NBWNbjamrkoF-nKKE
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
  - id: c1c5fb98-9105-44ed-9df1-9e04d062a784
feature_v2:
  - id: a1028f9a-6dbc-4a4f-adf5-eb9f85a408a6
  - id: b13bd2ad-8e65-49e5-9691-2a0d31067b35
  - id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45
subfeature_v2:
  - id: d5c7388a-594e-4d15-9b39-98d6ce479e8b
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
source-git-commit: d92345097c162b68b9d8405122534371c87c5f1a
workflow-type: tm+mt
source-wordcount: 686
ht-degree: 0%

---

# 使用適用於Microsoft Dynamics 365和Marketo的Acrobat Sign傳送通知

瞭解如何使用Acrobat Sign、適用於Microsoft動態的Acrobat Sign、Marketo和Marketo Microsoft Dynamics Sync傳送簡訊、電子郵件或推播通知，讓簽署者知道即將達成協定。 若要從Marketo傳送通知，您必須先購買或設定Marketo簡訊管理功能。 此逐步解說使用[Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/)，但其他Marketo SMS解決方案可供使用。

## 必要條件

1. 安裝Marketo Microsoft Dynamics Sync。

   [此處](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)提供Microsoft Dynamics Sync的資訊和最新外掛程式。

1. 安裝適用於Microsoft Dynamics的Acrobat Sign。

   [此處](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)提供此外掛程式的資訊。

## 尋找自訂物件

Marketo Microsoft Dynamics同步和Acrobat Sign for Dynamics設定完成後，「Marketo管理終端機」中會出現兩個新選項。

![管理員](assets/adminTerminal.png)

* 按一下&#x200B;**[!UICONTROL Dynamics Entities Sync]**。

  同步處理自訂實體前，必須先停用同步。 如果您是第一次，請按一下&#x200B;**[!UICONTROL 同步結構描述]**。 否則，請按一下&#x200B;**[!UICONTROL 重新整理結構描述]**。

  ![重新整理](assets/refreshSchema.png)

## 同步處理自訂物件

1. 在右側，找到[!UICONTROL 銷售機會]、[!UICONTROL 連絡人]和[!UICONTROL 帳戶]型自訂物件。

   * 如果要在Dynamics中將潛在客戶新增至合約時觸發，請為Lead底下的物件&#x200B;**[!UICONTROL 啟用同步]**。

   * 如果要在Dynamics中將連絡人新增至合約時觸發，請為[連絡人]底下的物件&#x200B;**[!UICONTROL 啟用[同步]]**。

   * 如果要在Dynamics中將帳號新增至合約時觸發，請為[帳號]下的物件&#x200B;**[!UICONTROL 啟用Sync]**。

   * **為想要的父項（潛在客戶、連絡人或帳戶）下的合約物件啟用同步**。

   ![自訂物件](assets/enableSyncDynamics.png)

1. 在新視窗中，在「協定」下選取您想要的屬性。

   啟用&#x200B;**[!UICONTROL 條件約束]**&#x200B;和&#x200B;**[!UICONTROL 觸發器]**&#x200B;下的方塊，以公開給您的行銷活動。

   ![自訂同步處理1](assets/entitySync1.png)

   ![自訂同步處理2](assets/entitySync2.png)

1. 在自訂物件上啟用同步後，重新啟用同步。

   返回[!UICONTROL 管理終端機]，按一下&#x200B;**[!UICONTROL Microsoft Dynamics]**，然後按一下&#x200B;**[!UICONTROL 啟用同步]**。

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![啟用全域](assets/enableGlobalDynamics.png)

## 建立方案

1. 在[!UICONTROL 行銷活動]中，用滑鼠右鍵按一下左側列上的&#x200B;**[!UICONTROL 行銷活動]**，選取&#x200B;**[!UICONTROL 新行銷活動資料夾]**，然後將其命名。

   ![新資料夾](assets/newFolder.png)

1. 以滑鼠右鍵按一下建立的資料夾，選取&#x200B;**[!UICONTROL 新程式]**，然後為其命名。

   保留其他專案為預設值，然後按一下[建立]。**&#x200B;**

   ![新程式1](assets/newProgram1.png)

   ![新程式2](assets/newProgram2.png)

## 設定[!DNL Twilio]簡訊

請先確定您擁有有效的[!DNL Twilio]帳戶並購買您所需的SMS功能。

設定Marketo - [!DNL Twilio]簡訊webhook需要您帳戶中的三個[!DNL Twilio]引數。

* 帳戶SID
* 帳戶權杖
* Twilio電話號碼

從您的帳戶擷取這些引數，現在請開啟您的Marketo執行個體。

1. 按一下右上角的&#x200B;**[!UICONTROL 管理員]**。

   ![管理員](assets/adminTab.png)

1. 按一下&#x200B;**[!UICONTROL Webhook]**，然後按一下&#x200B;**[!UICONTROL 新增Webhook]**。

   ![Webhook](assets/webhooks.png)

1. 輸入&#x200B;**[!UICONTROL Webhook名稱]**&#x200B;和&#x200B;**[!UICONTROL 描述]**。

1. 輸入下列URL，並確定以您的[!DNL Twilio]認證取代`ACCOUNT_SID`和`AUTH_TOKEN`。

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. 選取&#x200B;**[!UICONTROL POST]**&#x200B;作為您的要求型別。

1. 輸入下列&#x200B;**範本**，並確定要將`MY_TWILIO_NUMBER`取代為[!DNL Twilio]電話號碼，將`YOUR_MESSAGE`取代為您選擇的訊息。

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. 將&#x200B;**[!UICONTROL 要求權杖編碼]**&#x200B;設定為&#x200B;*表單/URL*。

1. 將回應型別設定為&#x200B;*JSON*，然後按一下&#x200B;**[!UICONTROL 儲存]**。

## 設定Smart Campaign觸發器

1. 在行銷活動區段中，以滑鼠右鍵按一下您建立的方案，然後選取&#x200B;**[!UICONTROL 新增Smart Campaign]**。

   ![智慧型行銷活動1](assets/smartCampaign1.png)

1. 將其命名，然後按一下[建立]。**&#x200B;**

   ![智慧型行銷活動2](assets/smartCampaign3.png)

   您應該會在Microsoft資料夾下看到數個可供使用的觸發器。

1. 按一下並將&#x200B;**[!UICONTROL 新增至合約]**&#x200B;拖曳至&#x200B;**[!UICONTROL 智慧列示]**，然後新增您想要在觸發程式上擁有的任何限制。

   ![已新增至合約](assets/addedToAgreementDynamics.png)

## 設定Smart Campaign流程

1. 按一下[!UICONTROL 智慧行銷活動]中的&#x200B;**[!UICONTROL 流量]**&#x200B;索引標籤。

   搜尋&#x200B;**呼叫Webhook**&#x200B;流程並拖曳至畫布上，然後選取您在上一節中建立的webhook。

   ![呼叫Webhook](assets/callWebhook.png)

1. 您針對新增至協定的潛在客戶的SMS通知行銷活動現已設定。
