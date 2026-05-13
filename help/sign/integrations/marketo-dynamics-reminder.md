---
title: 使用適用於Microsoft Dynamics 365和Marketo的Acrobat Sign傳送提醒
description: 瞭解當一段時間後仍未簽署協定時，如何傳送電子郵件提醒
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo Engage, Document Cloud
level: Intermediate
topic: Integrations
topic-revisit: Integrations
jira: KT-7250
thumbnail: KT-7250.jpg
exl-id: 5a97fade-18a3-448a-8504-efb9e38e9187
TQID: https://experienceleague.adobe.com/3F6HF0QuK6IkhjgKTGoEGpo16ZGIaY3rZiWUAOWbwTo
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615id: c1c5fb98-9105-44ed-9df1-9e04d062a784
feature_v2: id: a1028f9a-6dbc-4a4f-adf5-eb9f85a408a6id: b13bd2ad-8e65-49e5-9691-2a0d31067b35id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45id: ed6be6bb-75bb-4ea9-9a42-3bcaa65e1bcc
subfeature_v2: id: d5c7388a-594e-4d15-9b39-98d6ce479e8b
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: d92345097c162b68b9d8405122534371c87c5f1a
workflow-type: tm+mt
source-wordcount: 905
ht-degree: 1%

---

# 使用適用於Microsoft Dynamics 365和Marketo的Acrobat Sign傳送提醒

瞭解當一段時間後仍未簽署協定時，如何傳送電子郵件提醒。 此整合使用Acrobat Sign、適用於Microsoft Dynamics的Acrobat Sign、Marketo以及Marketo Microsoft Dynamics Sync。

## 必要條件

1. 安裝Marketo Microsoft Dynamics Sync。

   [此處](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)提供Microsoft Dynamics Sync的資訊和最新外掛程式。

1. 安裝適用於Microsoft Dynamics](https://appsource.microsoft.com/zh-tw/product/dynamics-365/adobesign.f3b856fc-a427-4d47-ad4b-d5d1baba6f86)的[Acrobat Sign。

   [此處](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)提供此外掛程式的資訊。

## 尋找自訂物件

Marketo Microsoft Dynamics同步和Acrobat Sign for Dynamics設定完成後，「Marketo管理終端機」中會出現兩個新選項。

![管理員](assets/adminTerminal.png)

1. 按一下&#x200B;**[!UICONTROL Dynamics Entities Sync]**。

   同步處理自訂實體前，必須先停用同步。 如果您是第一次，請按一下&#x200B;**同步結構描述**。 否則，請按一下&#x200B;**重新整理結構描述**。

   ![重新整理](assets/refreshSchema.png)

## 同步處理自訂物件

1. 在右側，找到[!UICONTROL 銷售機會]、[!UICONTROL 連絡人]和[!UICONTROL 帳戶]型自訂物件。

   * 如果要在[!UICONTROL 銷售機會]尚未在Dynamics中簽署合約時傳送提醒，請為&#x200B;**[!UICONTROL 銷售機會]**&#x200B;下的物件&#x200B;**啟用同步**。

   * 如果要在[!UICONTROL 連絡人]尚未在Dynamics中簽署合約時傳送提醒，請&#x200B;**啟用**[!UICONTROL &#x200B;連絡人&#x200B;]**下物件的同步**。

   * 如果要在[!UICONTROL 帳戶]尚未在Dynamics中簽署合約時傳送提醒，請&#x200B;**啟用**[!UICONTROL &#x200B;帳戶&#x200B;]**下物件的同步**。

   * **為所需**[!UICONTROL &#x200B;父系&#x200B;]**（[!UICONTROL 潛在客戶]、[!UICONTROL 連絡人]或[!UICONTROL 帳戶]）下的合約物件啟用Sync**。

   ![自訂物件](assets/enableSyncDynamics.png)

1. 在新視窗中，在[合約]下選取您想要的屬性，然後啟用[限制] ****&#x200B;和[觸發] ****&#x200B;下的方塊，以公開您的行銷活動。

   ![自訂同步處理1](assets/entitySync1.png)

   ![自訂同步處理2](assets/entitySync2.png)

1. 在自訂物件上啟用同步後，重新啟用同步。

   返回[管理終端機]，按一下&#x200B;**Microsoft Dynamics**，然後按一下&#x200B;**[啟用同步處理]**。

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![啟用全域](assets/enableGlobalDynamics.png)

## 建立程式和Token

1. 在Marketo的「行銷活動」區段中，在左側列上的「**行銷活動**」上按一下滑鼠右鍵。

   選取&#x200B;**新行銷活動資料夾**，並指定其名稱。

   ![新資料夾](assets/newFolder.png)

1. 以滑鼠右鍵按一下建立的資料夾，選取&#x200B;**新程式**，然後為其命名。

   保留其他專案為預設值，然後按一下[建立]。****

   ![新程式1](assets/newProgram1.png)

   ![新程式2](assets/newProgram2.png)

1. 按一下&#x200B;**我的Token**，然後將&#x200B;**電子郵件指令碼**&#x200B;拖曳到畫布上。

   ![電子郵件指令碼](assets/emailScript.png)

1. 提供名稱，然後按一下&#x200B;**按一下以編輯**。

   ![名稱和編輯](assets/nameAndSave.png)

1. 展開右側的&#x200B;**[!UICONTROL 自訂物件]**，然後展開&#x200B;**[!UICONTROL 合約]**&#x200B;物件。

   尋找[!UICONTROL 名稱]、合約狀態、傳送日期，以及目前的簽署者URL並拖曳到畫布上。

1. 使用這些權杖撰寫Velocity指令碼，以顯示一週內未簽署的合約URL。 以下是比較目前日期與「傳送日期」的範例：

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

## 建立提醒並新增個人化

個人化的範例包括：簽署者名稱、協定名稱、協定連結等。

1. 用滑鼠右鍵按一下您建立的程式，然後按一下&#x200B;**[!UICONTROL 新增本機資產]**，然後選取&#x200B;**[!UICONTROL 電子郵件]**。

   ![新電子郵件](assets/createNewEmail.png)

1. 在新索引標籤中，輸入電子郵件的&#x200B;**[!UICONTROL 名稱]**&#x200B;和&#x200B;**[!UICONTROL 描述]**，並從範本選擇器中選取範本。

   ![範本選擇器](assets/templatePicker.png)

1. 按一下&#x200B;**[!UICONTROL 「建立」]**。

1. 設定&#x200B;**[!UICONTROL 寄件者名稱]**&#x200B;和&#x200B;**[!UICONTROL 寄件者地址]**。

   ![提醒電子郵件](assets/reminderEmail.png)

1. 按一下訊息本文以啟動編輯器。

   按一下&#x200B;**[!UICONTROL 插入權杖]**&#x200B;按鈕，尋找您建立的自訂合約URL權杖，然後按一下&#x200B;**[!UICONTROL 插入]**。 完成自訂您的電子郵件，然後按一下&#x200B;**[!UICONTROL 儲存]**。

   ![插入Token](assets/insertToken.png)

1. 使用已指派合約的設定檔預覽。

   您應該會看到連至URL的連結，其中的「合約名稱」為標籤。

   ![電子郵件連結](assets/emailLink.png)

## 設定智慧行銷活動篩選器

1. 以滑鼠右鍵按一下您建立的方案，然後按一下&#x200B;**[!UICONTROL 新增Smart Campaign]**。

   ![智慧型行銷活動1](assets/smartCampaign1.png)

1. 為您選擇的名稱命名，然後按一下[建立]。****

   ![智慧型行銷活動2](assets/smartCampaign2.png)

1. 搜尋，然後按一下並將&#x200B;**[!UICONTROL 具有合約]**&#x200B;拖曳到智慧列示。

   ![有合約](assets/hasAgreementDynamics1.png)

   您公開給觸發器的欄位應該可以在&#x200B;**[!UICONTROL 新增限制]**&#x200B;中使用。

1. 選取「**[!UICONTROL 合約狀態]**」以及您想要作為篩選依據的任何其他欄位。

   對於每個新增的欄位，定義要作為篩選依據的值。 在此情況下，只有當&#x200B;**[!UICONTROL 合約狀態]**&#x200B;為&#x200B;*簽章結束*，且&#x200B;**[!UICONTROL 傳送日期]**&#x200B;為&#x200B;*且早於1週*&#x200B;時，才會觸發。

   ![合約狀態](assets/hasAgreementDynaSentOn.png)

   >[!NOTE]
   >
   > 如果您希望此行銷活動只針對特定合約執行，請將唯一識別碼新增至條件約束，例如&#x200B;**Name**。

1. 確認行銷活動對象，並在「排程」標籤中檢視誰符合資格。

   ![限定詞](assets/qualifiers.png)

## 設定Smart Campaign流程

由於已使用行銷活動篩選&#x200B;**到期前的天數**，因此您可以使用已排程的週期進行行銷活動。

1. 按一下[!UICONTROL 智慧行銷活動]中的&#x200B;**[!UICONTROL 流量]**&#x200B;索引標籤。

   搜尋&#x200B;**傳送電子郵件**&#x200B;流程，並將其拖曳至畫布上，並選取您在上一節建立的提醒電子郵件。

   ![傳送電子郵件](assets/sendEmail.png)

1. 按一下Smart Campaign中的&#x200B;**[!UICONTROL 排程]**&#x200B;索引標籤。 請確定&#x200B;**智慧行銷活動設定**&#x200B;中的行銷活動流程限製為每人執行一次。 然後，按一下&#x200B;**排程週期**&#x200B;索引標籤。

   ![排程標籤](assets/scheduleTab.png)

1. 將&#x200B;**排程**&#x200B;設定為&#x200B;_每日_。 視需要選擇行銷活動的開始日期、時間與結束日期。

   ![排程設定](assets/scheduleSettings.png)
