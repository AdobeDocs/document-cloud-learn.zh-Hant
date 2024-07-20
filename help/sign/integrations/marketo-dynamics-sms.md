---
title: 使用 Acrobat Sign 針對 Microsoft Dynamics 365 和 Marketo 傳送通知
description: 瞭解如何傳送簡訊、電子郵件或推送通知，讓簽署者知道合約即將推出
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic: Integrations
topic-revisit: Integrations
jira: KT-7249
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
source-git-commit: 452299b2b786beab9df7a5019da4f3840d9cdec9
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 0%

---

# 使用 Acrobat Sign 針對 Microsoft Dynamics 365 和 Marketo 傳送通知

瞭解如何使用 Acrobat Sign、Acrobat Sign for Microsoft Dynamic、Marketo 和 Marketo Microsoft Dynamics Sync，傳送簡訊、電子郵件或推送通知，讓簽署者知道合約進行中。 若要從 Marketo 傳送通知，您必須先購買或設定 Marketo SMS 管理功能。 此逐步解說使用 [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/)，但可以使用其他 Marketo SMS 解決方案。

## 必要條件

1. 安裝 Marketo Microsoft Dynamics Sync。

   有關 Microsoft Dynamics Sync 的資訊和最新外掛程式，請參閱 [這裡。](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. 安裝 Microsoft Dynamics Acrobat Sign。

   有關此增效模組的資訊請參閱 [這裡。](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## 尋找自定義物件

Marketo Microsoft Dynamics Sync 和 Acrobat Sign for Dynamics 設定完成後，Marketo Admin Terminal 中會出現兩個新選項。

![管理](assets/adminTerminal.png)

* 按兩下 **[!UICONTROL 「Dynamics 實體同步」]** 。

  同步自定義實體之前，必須停用同步。 如果這是您第一次這麼做，請按兩下 **[!UICONTROL 「同步結構]** 」。 否則，請按下 **[!UICONTROL 「重新整理結構」]**。

  ![刷新](assets/refreshSchema.png)

## 同步自定義物件

1. 在右側找到 [!UICONTROL 「商機]」、 [!UICONTROL 「聯繫人]」和 [!UICONTROL 「帳戶]」自定義物件。

   * **[!UICONTROL 如果您想要在 Dynamics 中將銷售機會新增至合約時觸發，請為「商機」底下的物件啟用同步]** 。

   * **[!UICONTROL 如果您想要在 Dynamics 中將聯繫人新增至合約時觸發「連絡人」，請為「聯繫人」底下的物件啟用同步]** 。

   * **[!UICONTROL 如果您想要在 Dynamics 中將帳戶新增至合約時觸發「帳戶」底下的物件「同步]** 」。

   * **在所需的父級 （商機、聯繫人或帳戶） 下方，啟用合約物件的同步** 功能。

   ![自訂物件](assets/enableSyncDynamics.png)

1. 在新視窗中，選取您在「合約」下想要的屬性。

   啟用「限制&#x200B;]**」和**[!UICONTROL 「觸發器&#x200B;]**」下方**[!UICONTROL &#x200B;的方塊，即可將其顯示在您的營銷活動中。

   ![自訂同步 1](assets/entitySync1.png)

   ![自訂同步 2](assets/entitySync2.png)

1. 在自定義物件上啟用同步後，重新啟動同步。

   返回 [!UICONTROL 「管理員終端機]」，然後按兩下 **[!UICONTROL 「Microsoft Dynamics]**」，然後按兩下 **[!UICONTROL 「啟用同步」]**。

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![啟用全域](assets/enableGlobalDynamics.png)

## 建立程式

1. 在[!UICONTROL 「行銷活動」]中，在左列的「營銷活動&#x200B;]**」上按下滑鼠右鍵**[!UICONTROL ，選&#x200B;**[!UICONTROL 取「新增Campaign資料夾]**」，然後將其命名。

   ![新檔案夾](assets/newFolder.png)

1. 在建立的檔案夾上按下滑鼠右鍵，選取 **[!UICONTROL 「新增程式]**」，然後命名。

   將其他一切保留為預設值，然後按兩下「 **[!UICONTROL 建立」]**。

   ![新方案 1](assets/newProgram1.png)

   ![新方案 2](assets/newProgram2.png)

## [!DNL Twilio]設定簡訊

請先確認您擁有有效 [!DNL Twilio] 帳戶，並購買所需的SMS功能。

設定 Marketo - [!DNL Twilio] SMS Webhook 需要您的帳戶提供三個 [!DNL Twilio] 參數。

* 帳戶 SID
* 帳戶令牌
* Twilio 電話號碼

從您的帳戶擷取這些參數，現在請開啟您的 Marketo 實例。

1. 按下 **[!UICONTROL 右上方的「管理員]** 」。

   ![管理](assets/adminTab.png)

1. 按兩下 **[!UICONTROL 「Webhook」]**，然後按一下 **[!UICONTROL 「新增 Webhook」]**。

   ![Webhook](assets/webhooks.png)

1. **[!UICONTROL 輸入 Webhook 名稱]**&#x200B;和&#x200B;**[!UICONTROL 說明]**。

1. 輸入下列URL，並務必更換`ACCOUNT_SID`憑證和`AUTH_TOKEN`[!DNL Twilio]認證。

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. 選 **[!UICONTROL 取「POST]** 」做為您的「要求」類型。

1. 輸入下列 **範本** ，並務必以 `MY_TWILIO_NUMBER` 電話號碼 [!DNL Twilio] 取代，並 `YOUR_MESSAGE` 顯示您選擇的訊息。

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. 將「 **[!UICONTROL 要求令牌編碼]** 」設為 *「表格/URL」*。

1. 將回應類型設為 *JSON，* 然後按兩下「儲存 **[!UICONTROL 」]**。

## 設定智慧型手機Campaign觸發程式

1. 在「行銷活動」區段中，在您建立的程式上按下滑鼠右鍵，然後選取「 **[!UICONTROL 新增智慧型手機Campaign]**」。

   ![智慧型Campaign 1](assets/smartCampaign1.png)

1. 命名，然後按兩下「 **[!UICONTROL 建立」]**。

   ![智慧型Campaign 2](assets/smartCampaign3.png)

   您應該會在「Microsoft」資料夾下看到幾個可用的觸發器。

1. 按兩下並拖 **[!UICONTROL 曳「新增至合約]** 」至 **[!UICONTROL 「智慧型清單]**」，然後在觸發程式中新增任何限制。

   ![新增至合約](assets/addedToAgreementDynamics.png)

## 設定智慧型手機Campaign流程

1. 按兩下「智慧型Campaign中的[!UICONTROL 「流量&#x200B;]**」索引標籤]。**[!UICONTROL 

   Search，將「呼叫 Webhook **」流程拖**&#x200B;曳到畫布上，然後選取您在上一個區段中建立的 Webhook。

   ![呼叫 Webhook](assets/callWebhook.png)

1. 現在已為新增至合約的潛在客戶設定SMS通知營銷活動。
>[!TIP]
>
>本教學課程包含 Acrobat適用於 Microsoft Dynamics 和 Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) 的 Acrobat Sign Experience League上免費提供，是本課程[的一部分，可加速銷售週期！