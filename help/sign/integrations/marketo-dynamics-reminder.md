---
title: Send reminders using Adobe Sign for Microsoft Dynamics 365 and Marketo
description: Learn how to send an email reminder when an agreement remains unsigned after a period of time
role: Admin
product: adobe sign
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7250.jpg
exl-id: 5a97fade-18a3-448a-8504-efb9e38e9187
source-git-commit: 089b6768cee4e3af8f1a349d5754d84aa3f4f69a
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 2%

---

# Send reminders using Adobe Sign for Microsoft Dynamics 365 and Marketo

Learn how to send an email reminder when an agreement remains unsigned after a period of time. This integration uses Adobe Sign, Adobe Sign for Microsoft Dynamics, Marketo, and the Marketo Microsoft Dynamics Sync.

## 必要條件

1. Install the Marketo Microsoft Dynamics Sync.

   [](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. [](https://appsource.microsoft.com/zh-tw/product/dynamics-365/adobesign.f3b856fc-a427-4d47-ad4b-d5d1baba6f86)

   [](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Find the custom object

Once the Marketo Microsoft Dynamics Sync and Adobe Sign for Dynamics configurations are complete, two new options appear in the Marketo Admin Terminal.

![管理員](assets/adminTerminal.png)

1. ****

   Sync must be disabled before syncing custom entities. ********

   ![重新整理](assets/refreshSchema.png)

## Sync the custom object

1. 

   * ********

   * ********

   * ********

   * ********

   ![自訂物件](assets/enableSyncDynamics.png)

1. ********

   ![](assets/entitySync1.png)

   ![](assets/entitySync2.png)

1. Reactivate the sync after enabling sync on the custom objects.

   ********

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![](assets/enableGlobalDynamics.png)

## Create the program and token

1. ****

   ****

   ![](assets/newFolder.png)

1. ****

   ****

   ![](assets/newProgram1.png)

   ![](assets/newProgram2.png)

1. ********

   ![](assets/emailScript.png)

1. ****

   ![](assets/nameAndSave.png)

1. ********

   

1. Write a Velocity script using these tokens to display the agreement URL of an agreement that goes unsigned for a week. Here is an example that compares the current date to Sent On:

   ```
   #foreach($agreement in $adobe_agreementList)
       #if($agreement.adobe_esagreementstatus == "Out for Signature")
           #set($todayCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$date.get('yyyy-MM-dd'))) )
           #set($dateSentCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$agreement.adobe_datesent)) )
           #set($dateDiff = ($todayCalObj.getTimeInMillis() - $dateSentCalObj.getTimeInMillis()) / 86400000 )
   
           #if($dateDiff >= 7)
               #set($agreementName = $agreement.adobe_name)
               #set($agreementURL = $agreement.adobe_currentsignerurl.substring(8))
               #break
           #else
           #end
       #else
       #end
   #end
   
   #if(${agreementName})
       <a href="https://${agreementURL}">${agreementName}</a>
   #else
       Please contact us. 
   #end
   ```

1. 按一下「**[!UICONTROL 儲存]**」。

## Create the reminder and add personalization

Examples of personalization include: the name of the signer, the name of the agreement, a link to the agreement, etc.

1. ********

   ![](assets/createNewEmail.png)

1. ********

   ![](assets/templatePicker.png)

1. 按一下「**[!UICONTROL 建立]**」。

1. ********

   ![](assets/reminderEmail.png)

1. Click on the message body to activate the Editor.

   ************

   ![](assets/insertToken.png)

1. Preview using a profile that has an agreement assigned to it.

   You should see a link to the URL with the Agreement Name as the label.

   ![](assets/emailLink.png)

## Set up the Smart Campaign Filter

1. ****

   ![](assets/smartCampaign1.png)

1. ****

   ![](assets/smartCampaign2.png)

1. ****

   ![](assets/hasAgreementDynamics1.png)

   ****

1. ****

   For each field added, define the values to filter by. ************

   ![合約狀態](assets/hasAgreementDynaSentOn.png)

   >[!NOTE]
   >
   > ****

1. Confirm the campaign audience and see who will qualify in the Schedule tab.

   ![](assets/qualifiers.png)

## Set up the Smart Campaign Flow

****

1. ****

   ****

   ![](assets/sendEmail.png)

1. ************

   ![](assets/scheduleTab.png)

1. ****__ Choose a start day and time and end date for the campaign if necessary.

   ![](assets/scheduleSettings.png)

>[!TIP]
>
>[](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1)