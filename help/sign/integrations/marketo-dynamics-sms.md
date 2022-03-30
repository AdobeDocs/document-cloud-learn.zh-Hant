---
title: Send notifications using Adobe Sign for Microsoft Dynamics 365 and Marketo
description: Learn how to send a text message, email, or push notification to let the signer know an agreement is on its way
role: Admin
product: adobe sign
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
source-git-commit: 089b6768cee4e3af8f1a349d5754d84aa3f4f69a
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Send notifications using Adobe Sign for Microsoft Dynamics 365 and Marketo

Learn how to send a text message, email, or push notification to let the signer know an agreement is on its way using Adobe Sign, Adobe Sign for Microsoft Dynamic, Marketo, and the Marketo Microsoft Dynamics Sync. To send notifications from Marketo, you first need to purchase or configure a Marketo SMS management feature. [](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/)

## 必要條件

1. Install the Marketo Microsoft Dynamics Sync.

   [](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Install Adobe Sign for Microsoft Dynamics.

   [](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Find the custom object

Once the Marketo Microsoft Dynamics Sync and Adobe Sign for Dynamics configurations are complete, two new options appear in the Marketo Admin Terminal.

![管理員](assets/adminTerminal.png)

* ****

   Sync must be disabled before syncing custom entities. ********

   ![重新整理](assets/refreshSchema.png)

## Sync the custom object

1. 

   * ****

   * ****

   * ****

   * ****

   ![自訂物件](assets/enableSyncDynamics.png)

1. In the new window, select the properties you want under Agreement.

   ********

   ![](assets/entitySync1.png)

   ![](assets/entitySync2.png)

1. Reactivate the sync after enabling sync on the custom objects.

   ********

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![](assets/enableGlobalDynamics.png)

## Create the program

1. ********

   ![](assets/newFolder.png)

1. ****

   ****

   ![](assets/newProgram1.png)

   ![](assets/newProgram2.png)

## [!DNL Twilio]

[!DNL Twilio]

[!DNL Twilio][!DNL Twilio]

* Account SID
* Account Token
* Twilio Phone Number

Retrieve these parameters from your account, now open your Marketo instance.

1. ****

   ![管理員](assets/adminTab.png)

1. ********

   ![Webhook](assets/webhooks.png)

1. ********

1. `ACCOUNT_SID``AUTH_TOKEN`[!DNL Twilio]

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. ****

1. ****`MY_TWILIO_NUMBER`[!DNL Twilio]`YOUR_MESSAGE`

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. ******

1. ******

## Set up the Smart Campaign Trigger

1. ****

   ![](assets/smartCampaign1.png)

1. ****

   ![](assets/smartCampaign3.png)

   You should see several triggers available for use under the Microsoft folder.

1. ********

   ![](assets/addedToAgreementDynamics.png)

## Set up the Smart Campaign Flow

1. ****

   ****

   ![](assets/callWebhook.png)

1. Your SMS notice campaign for leads who are added to an agreement is now set up.
>[!TIP]
>
>[](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1)