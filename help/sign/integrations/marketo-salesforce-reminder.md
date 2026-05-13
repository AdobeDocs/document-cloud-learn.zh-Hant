---
title: 使用適用於Salesforce的Acrobat Sign和Marketo設定指南傳送提醒
description: 瞭解當一段時間後仍未簽署協定時，如何從Marketo傳送電子郵件提醒
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo Engage, Document Cloud
level: Intermediate
topic: Integrations
jira: KT-7248
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: 33aca2e0-2f27-4100-a16f-85ba652c17a3
TQID: https://experienceleague.adobe.com/LfZGcDB7-D6cUdqzCbbsUQuJWSk2k-MkBjIt1w--vgU
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
  - id: c1c5fb98-9105-44ed-9df1-9e04d062a784
feature_v2:
  - id: a1028f9a-6dbc-4a4f-adf5-eb9f85a408a6
  - id: b13bd2ad-8e65-49e5-9691-2a0d31067b35
  - id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45
  - id: ed6be6bb-75bb-4ea9-9a42-3bcaa65e1bcc
subfeature_v2:
  - id: d5c7388a-594e-4d15-9b39-98d6ce479e8b
  - id: ea4e3ff5-e7b9-4b4c-a5a0-dc27cc3f4275
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: d92345097c162b68b9d8405122534371c87c5f1a
workflow-type: tm+mt
source-wordcount: 949
ht-degree: 0%

---

# 使用適用於Salesforce的Acrobat Sign和Marketo設定指南傳送提醒

瞭解當一段時間後仍未簽署協定時，如何從Marketo傳送電子郵件提醒。 此整合使用Acrobat Sign、適用於Salesforce的Acrobat Sign、Marketo，以及Marketo和Salesforce Sync。

## 必要條件

1. 安裝Marketo Salesforce Sync。

   [此處](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html?lang=zh-Hant)提供Salesforce Sync的資訊和最新外掛程式。

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

如果您想要在Lead尚未在Salesforce中簽署合約時傳送提醒，請為Lead底下的物件&#x200B;**啟用Sync**。

**如果您要在連絡人尚未在Salesforce中簽署合約時傳送提醒，請為連絡人底下的物件**&#x200B;啟用同步處理。

如果要在帳戶尚未在Salesforce中簽署合約時傳送提醒，請為[帳戶]下的物件&#x200B;**啟用Sync**。

1. **為顯示在所需父項（潛在客戶、連絡人或帳戶）下的**&#x200B;合約&#x200B;**物件啟用同步**。 針對您想要同步的任何其他自訂物件執行此動作。

   ![合約物件](assets/agreementObject.png)

1. 下列資產顯示如何&#x200B;**啟用同步**。

   ![自訂同步處理1](assets/customObjectSync1.png)

   ![自訂同步處理2](assets/customObjectSync2.png)

## 向觸發器公開自訂物件欄位

1. 停用全域同步時，請選取您啟用同步處理的協定自訂物件，然後&#x200B;**編輯可見欄位**。

1. 勾選觸發程式欄位中的「合約名稱」欄位，將其公開給您的Campaign動作觸發程式。 勾選您要依據的其他欄位，然後&#x200B;**儲存**。

   ![編輯可見欄位1](assets/editVisible1.png)

   ![編輯可見欄位2](assets/editVisible2.png)

1. 在自訂物件上啟用同步並公開觸發程式值後，請記得重新啟用ync：

   ![啟用全域](assets/enableGlobal.png)

## 建立程式和Token

1. 在Marketo的「行銷活動」區段中，以滑鼠右鍵按一下左側列上的&#x200B;**行銷活動**，選取&#x200B;**新增行銷活動資料夾**，然後為其命名。

   ![新資料夾](assets/newFolder.png)

1. 以滑鼠右鍵按一下建立的資料夾，選取&#x200B;**新程式**，然後為其命名。 保留其他專案為預設值，然後按一下[建立]。**&#x200B;**

   ![新程式1](assets/newProgram1.png)

   ![新程式2](assets/newProgram2.png)

1. 按一下&#x200B;**我的Token**，然後將&#x200B;**電子郵件指令碼**&#x200B;拖曳到畫布上。

   ![電子郵件指令碼](assets/emailScript.png)

1. 提供名稱，然後按一下&#x200B;**按一下以編輯**。

   ![名稱和編輯](assets/nameAndSave.png)

1. 展開右側的&#x200B;**自訂物件**，然後展開&#x200B;**合約**&#x200B;物件。 尋找並拖曳合約名稱、合約狀態、簽署日期和簽署URL至畫布。

1. 使用這些權杖撰寫Velocity指令碼，以顯示一週內未簽署的合約URL。 以下是比較目前日期與「傳送日期」的範例：

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

## 建立提醒並新增個人化

個人化的範例包括：簽署者名稱、協定名稱、協定連結等。

1. 用滑鼠右鍵按一下您建立的程式，然後按一下&#x200B;**新增本機資產**，然後選取&#x200B;**電子郵件**。

   ![新電子郵件](assets/createNewEmail.png)

1. 在新索引標籤中，輸入電子郵件的&#x200B;**名稱**&#x200B;和&#x200B;**描述**，並從範本選擇器中選取範本。 按一下&#x200B;**「建立」**。

   ![範本選擇器](assets/templatePicker.png)

1. 設定&#x200B;**寄件者名稱**&#x200B;和&#x200B;**寄件者地址**。

   ![提醒電子郵件](assets/reminderEmail.png)

1. 按一下訊息本文以啟動編輯器。 按一下&#x200B;**插入權杖**&#x200B;按鈕，尋找您建立的自訂合約URL權杖，然後按一下&#x200B;**插入**。 完成自訂您的電子郵件，然後按一下&#x200B;**儲存**。

   ![插入Token](assets/insertToken.png)

1. 使用已指派合約的設定檔預覽。 您應該會看到連至URL的連結，其中的「合約名稱」為標籤。

   ![電子郵件連結](assets/emailLink.png)

## 設定智慧行銷活動篩選器

1. 以滑鼠右鍵按一下您建立的方案，然後按一下&#x200B;**新增Smart Campaign**。

   ![智慧型行銷活動1](assets/smartCampaign1.png)

1. 為您選擇的名稱命名，然後按一下[建立]。**&#x200B;**

   ![智慧型行銷活動2](assets/smartCampaign2.png)

1. 搜尋，然後按一下並將&#x200B;**具有合約**&#x200B;拖曳到智慧列示。

   ![有合約](assets/hasAgreement.png)

1. 您公開給觸發器的欄位現在應該可以在&#x200B;**新增限制**&#x200B;中使用。 選取「**合約狀態**」以及您想要作為篩選依據的任何其他欄位。 對於每個新增的欄位，定義要作為篩選依據的值。 在此情況下，只有當&#x200B;**合約狀態**&#x200B;為簽名過期，且&#x200B;**傳送日期**&#x200B;在過去7天之前時，才會觸發此事件。

   ![合約狀態](assets/agreementStatus.png)

   >[!NOTE]
   >
   > 如果您希望此行銷活動只針對特定合約執行，請為條件約束（例如&#x200B;**合約名稱**）指定唯一的識別碼。

1. 確認行銷活動對象，並在「排程」標籤中檢視誰符合資格。

   ![限定詞](assets/qualifiers.png)

## 設定Smart Campaign流程

由於已使用未簽署的行銷活動篩選器&#x200B;**天**，因此您可以在此行銷活動中使用排程的週期。

1. 按一下Smart Campaign中的&#x200B;**流量**&#x200B;標籤。 搜尋&#x200B;**傳送電子郵件**&#x200B;流程，並將其拖曳至畫布上，並選取您在上一節建立的提醒電子郵件。

   ![傳送電子郵件](assets/sendEmail.png)

1. 按一下Smart Campaign中的&#x200B;**排程**&#x200B;索引標籤。 請確定&#x200B;**智慧行銷活動設定**&#x200B;中的行銷活動流程限製為每人執行一次。 然後，按一下&#x200B;**排程週期**&#x200B;索引標籤。

   ![排程標籤](assets/scheduleTab.png)

1. 將&#x200B;**排程**&#x200B;設定為「每日」，視需要選擇行銷活動的開始日期與時間，以及結束日期。

   ![排程設定](assets/scheduleSettings.png)

