---
title: 使用 Adobe Sign 針對 Microsoft Dynamics 365 和 Marketo 傳送通知
description: 瞭解如何傳送簡訊、電子郵件或推送通知，讓簽署者知道合約即將推出
role: Admin
product: adobe sign
solution: Adobe Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
source-git-commit: bcddb0ee106239f2786debaed908b2a2ec5ce792
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# 使用 Adobe Sign 針對 Microsoft Dynamics 365 和 Marketo 傳送通知

瞭解如何傳送簡訊、電子郵件或推送通知，讓簽署者知道合約正在使用 Adobe Sign、Adobe Sign for Microsoft Dynamic、Marketo 和 Marketo Microsoft Dynamics Sync。 若要從 Marketo 傳送通知，您必須先購買或設定 Marketo SMS 管理功能。 此逐步解說使用 [ Twilio ](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/) SMS，但可以使用其他 Marketo SMS 解決方案。

## 必要條件

1. 安裝 Marketo Microsoft Dynamics Sync。

   有關 Microsoft Dynamics Sync 的資訊和最新外掛程式，請參閱 [ 這裡。](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. 安裝適用于 Microsoft Dynamics 的 Adobe Sign。

   有關此增效模組的資訊請參閱 [ 這裡。](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## 尋找自訂物件

Marketo Microsoft Dynamics Sync 和 Adobe Sign for Dynamics 設定完成後，Marketo Admin Terminal 中就會出現兩個新選項。

![管理員](assets/adminTerminal.png)

* 按一下 **[!UICONTROL 「Dynamics 實體同步]** 」。

   同步自訂實體之前，必須停用同步。 **** 如果這是您第一次這麼做，請按一下「同步結構」。否則，請按一下 **[!UICONTROL 「重新整理結構]** 」。

   ![重新整理](assets/refreshSchema.png)

## 同步自訂物件

1. 在右側找到 [!UICONTROL  「商機 ] 」、「 [!UICONTROL  連絡人」 ] 和「 [!UICONTROL  帳戶 ] 」型自訂物件。

   * **[!UICONTROL 如果您想要在 Dynamics 中將銷售機會]** 新增至合約時觸發，請為「商機」底下的物件啟用同步。

   * **[!UICONTROL 如果您想要在 Dynamics 中將連絡人新增至合約時觸發「連絡人」，請為「連絡人」]** 底下的物件啟用同步。

   * ****&#x200B;如果您想要在 Dynamics 中將帳戶新增至合約時觸發「帳戶」底下的物件「同步」。

   * **在** 所需的父級 （商機、連絡人或帳戶） 下方，啟用合約物件的同步功能。

   ![自訂物件](assets/enableSyncDynamics.png)

1. 在新視窗中，選取您在「合約」下想要的屬性。

   啟用「 **[!UICONTROL 限制」和「觸發器」下方的方塊]** **** ，即可將其顯示在您的行銷活動中。

   ![自訂同步 1](assets/entitySync1.png)

   ![自訂同步 2](assets/entitySync2.png)

1. 在自訂物件上啟用同步後，重新開機同步。

   返回 [!UICONTROL  管理員終端機 ] ，然後按一下 **[!UICONTROL Microsoft]** Dynamics，然後按一下 **[!UICONTROL 「啟用同步]** 」。

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![啟用全域](assets/enableGlobalDynamics.png)

## 建立程式

1. 在 [!UICONTROL  「行銷活動」 ] 中，在 **[!UICONTROL 左側列的「行銷活動」上按一下]** 滑鼠右鍵，選取 **[!UICONTROL 「新增Campaign資料夾]** 」，然後將其命名。

   ![新檔案夾](assets/newFolder.png)

1. 在建立的檔案夾上按一下滑鼠右鍵，選取「 **[!UICONTROL 新增程式]** 」，然後命名。

   將其他一切保留為預設值，然後按一下「 **[!UICONTROL 建立]** 」。

   ![新方案 1](assets/newProgram1.png)

   ![新方案 2](assets/newProgram2.png)

## 設定 [!DNL Twilio] 簡訊

請先確認您擁有有效 [!DNL Twilio] 帳戶，並購買所需的 SMS 功能。

設定 Marketo - [!DNL Twilio] SMS Webhook 需要 [!DNL Twilio] 您的帳戶提供三個參數。

* 帳戶 SID
* 帳戶權杖
* Twilio 電話號碼

從您的帳戶擷取這些參數，現在請開啟您的 Marketo 實例。

1. 按一下 **** 右上方的「管理員」。

   ![管理員](assets/adminTab.png)

1. 按一下 **** 「Webhook」，然後按一下「 **[!UICONTROL 新增 Webhook」。]**

   ![Webhook](assets/webhooks.png)

1. 輸入 **[!UICONTROL Webhook 名稱]** 和 **[!UICONTROL 說明]** 。

1. 輸入下列URL，並務必更換 `ACCOUNT_SID` 憑 `AUTH_TOKEN` [!DNL Twilio] 證和認證。

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. 選 **[!UICONTROL 取]** 「POST」做為您的「要求」類型。

1. 輸入下列 **範本** ，並務必以 `MY_TWILIO_NUMBER` [!DNL Twilio] 電話號碼取代，並顯示 `YOUR_MESSAGE` 您選擇的訊息。

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. 將 **[!UICONTROL 「要求權杖編碼」設]** 為 *「表格* /URL」。

1. 將回應類型設為 *JSON，* 然後按一下「 **[!UICONTROL 儲存]** 」。

## 設定智慧型Campaign觸發程式

1. 在「行銷活動」區段中，在您建立的程式上按一下滑鼠右鍵，然後選取「 **[!UICONTROL 新增智慧型Campaign]** 。。

   ![智慧型Campaign 1](assets/smartCampaign1.png)

1. 命名，然後按一下「 **[!UICONTROL 建立]** 」。

   ![Smart Campaign 2](assets/smartCampaign3.png)

   您應該會在 Microsoft 檔案夾下看到幾個可用的觸發程式。

1. 按一下並拖曳 **** 「新增至合約」至 **[!UICONTROL 「智慧型清單]** 」，然後在觸發程式上新增任何限制。

   ![新增至合約](assets/addedToAgreementDynamics.png)

## 設定智慧型Campaign流程

1. 按一下智慧型 **** Campaign中的「流量 [!UICONTROL  」索引標籤 ] 。

   Search，將 **「呼叫 Webhook」流程拖曳** 到畫布上，然後選取您在上一個區段中建立的 Webhook。

   ![呼叫 Webhook](assets/callWebhook.png)

1. 現在已為新增至合約的潛在客戶設定 SMS 通知行銷活動。
>[!TIP]
>
>本教學課程包含在 Experience League [ 上免費提供 Microsoft Dynamics 和 Marketo Adobe Sign，可加速銷售週期 ](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) ！