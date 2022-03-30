---
title: Send notifications using Adobe Sign for Salesforce and Marketo
description: Learn how to send a text message, email, or push notification to let the signer know an agreement is on its way
role: Admin
product: adobe sign
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: ac3334ec-b65f-4ce4-b323-884948f5e0a6
source-git-commit: 089b6768cee4e3af8f1a349d5754d84aa3f4f69a
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Send notifications using Adobe Sign for Salesforce and Marketo

Learn how to send a text message, email, or push notification to let the signer know an agreement is on its way using Adobe Sign, Adobe Sign for Salesforce, Marketo, and the Marketo Salesforce Sync. To send notifications from Marketo, you first need to purchase or configure a Marketo SMS management feature. [](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/)

## 必要條件

1. Install the Marketo Salesforce Sync.

   [](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Install Adobe Sign for Salesforce.

   [](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Find the custom object

Once the Marketo Salesforce Sync and Adobe Sign for Salesforce configurations are complete, several new options appear in the Marketo Admin Terminal.

![管理員](assets/adminTab.png)

![](assets/salesforceAdmin.png)

1. ********

   ![重新整理](assets/refreshSchema1.png)

1. ****

   ![停用](assets/disableGlobal.png)

1. ****

   ![](assets/refreshSchema2.png)

## Sync the custom objects

On the right side, see Lead, Contact, and Account-based custom objects.

****

****

****

1. ****

   ![自訂物件](assets/customObjects.png)

1. ****

   ![](assets/customObjectSync1.png)

   ![](assets/customObjectSync2.png)

1. When finished enabling sync on the Custom Objects, reactivate the sync.

   ![](assets/enableGlobal.png)

## Create the program

1. ********

   ![](assets/newFolder.png)

1. ********

   ![](assets/newProgram1.png)

   ![](assets/newProgram2.png)

## Set up Twilio SMS

First ensure you have an active Twilio account and purchased the SMS features you require.

Setting up the Marketo - Twilio SMS webhook requires three Twilio parameters from your account.

- Account SID
- Account Token
- Twilio Phone Number

Retrieve these parameters from your account, now open up your Marketo instance.

1. ****

   ![管理員](assets/adminTab.png)

1. ********

   ![Webhook](assets/webhooks.png)

1. ********

1. **[]****[]**

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. ****

1. ******[]****[]**

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Set the Request Token Encoding to Form/URL.

1. ****

## Set up the Smart Campaign Trigger

1. ****

   ![](assets/smartCampaign1.png)

1. ****

   ![](assets/smartCampaign3.png)

   If the configuration for the Custom Object Sync was done correctly, you should see the following triggers available for use under the Salesforce folder.

1. Click and drag Added to Agreement to the Smart List. Add any constraints you wish to have on the trigger.

   ![](assets/addedToAgreement2.png)

## Set up the Smart Campaign Flow

1. ********

   ![](assets/callWebhook.png)

1. Your SMS notice campaign for leads who are added to an agreement is now set up.

>[!TIP]
>
>[](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1)