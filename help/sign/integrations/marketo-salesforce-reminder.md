---
title: Send reminders using Adobe Sign for Salesforce and Marketo Configuration Guide
description: Learn how to send an email reminder from Marketo when an agreement remains unsigned after a period of time
role: Admin
product: adobe sign
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: 33aca2e0-2f27-4100-a16f-85ba652c17a3
source-git-commit: 089b6768cee4e3af8f1a349d5754d84aa3f4f69a
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 1%

---

# Send reminders using Adobe Sign for Salesforce and Marketo Configuration Guide

Learn how to send an email reminder from Marketo when an agreement remains unsigned after a period of time. This integration uses Adobe Sign, Adobe Sign for Salesforce, Marketo, and the Marketo and Salesforce Sync.

## 必要條件

1. Install the Marketo Salesforce Sync.

   [](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Install Adobe Sign for Salesforce.

   [](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Find the custom object

When the Marketo Salesforce Sync and Adobe Sign for Salesforce configurations are complete, several new options appear in the Marketo Admin Terminal.

![管理員](assets/adminTab.png)

![](assets/salesforceAdmin.png)

1. ********

   ![重新整理](assets/refreshSchema1.png)

1. ****

   ![停用](assets/disableGlobal.png)

1. ****

   ![](assets/refreshSchema2.png)

## Sync the custom object

On the right side, see Lead, Contact, and Account-based custom objects.

****

****

****

1. ******** Do this for any other custom objects you&#39;d like to sync.

   ![](assets/agreementObject.png)

1. ****

   ![](assets/customObjectSync1.png)

   ![](assets/customObjectSync2.png)

## Expose the custom object fields to triggers

1. ****

1. Check the &quot;Agreement Name&quot; field in the trigger column to expose it to your Campaign Action Triggers. ****

   ![](assets/editVisible1.png)

   ![](assets/editVisible2.png)

1. When finished enabling sync on the custom objects and exposing the trigger values, remember to reactivate the ync:

   ![](assets/enableGlobal.png)

## Create the program and token

1. ********

   ![](assets/newFolder.png)

1. ********

   ![](assets/newProgram1.png)

   ![](assets/newProgram2.png)

1. ********

   ![](assets/emailScript.png)

1. ****

   ![](assets/nameAndSave.png)

1. ******** Find and drag Agreement Name, Agreement Status, Date Signed, and Signing URL onto the canvas.

1. Write a Velocity script using these tokens to display the agreement URL of an agreement that goes unsigned for a week. Here is an example that compares the current date to Date Sent:

   ```
   #foreach($agreement in $echosign_dev1__SIGN_Agreement__cList)
       #if($agreement.echosign_dev1__Status__c == "Out for Signature")
           #set($todayCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$date.get('yyyy-MM-dd'))) )
           #set($dateSentCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$agreement.echosign_dev1__DateSent__c)) )
           #set($dateDiff = ($todayCalObj.getTimeInMillis() - $dateSentCalObj.getTimeInMillis()) / 86400000 )
   
           #if($dateDiff >= 7)
               #set($agreementName = $agreement.Name)
               #set($agreementURL = $agreement.echosign_dev1__Signing_URL__c.substring(8))
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

1. 按一下「**儲存**」。

## Create the reminder and add personalization

Examples of personalization include: the name of the signer, the name of the agreement, a link to the agreement, etc.

1. ********

   ![](assets/createNewEmail.png)

1. ********&#x200B;按一下「**建立**」。

   ![](assets/templatePicker.png)

1. ********

   ![](assets/reminderEmail.png)

1. Click on the message body to activate the Editor. ************

   ![](assets/insertToken.png)

1. Preview using a profile that has an agreement assigned to it. You should see a link to the URL with the Agreement Name as the label.

   ![](assets/emailLink.png)

## Set up the Smart Campaign Filter

1. ****

   ![](assets/smartCampaign1.png)

1. ****

   ![](assets/smartCampaign2.png)

1. ****

   ![](assets/hasAgreement.png)

1. ******** For each field added, define the values to filter by. ********

   ![合約狀態](assets/agreementStatus.png)

   >[!NOTE]
   >
   > ****

1. Confirm the campaign audience and see who will qualify in the Schedule tab.

   ![](assets/qualifiers.png)

## Set up the Smart Campaign Flow

****

1. ********

   ![](assets/sendEmail.png)

1. ************

   ![](assets/scheduleTab.png)

1. ****

   ![](assets/scheduleSettings.png)

>[!TIP]
>
>[](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1)
