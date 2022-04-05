---
title: 使用適用于 Microsoft Dynamics 365 和 Marketo 的 Acrobat Sign 傳送提醒
description: 瞭解如何在合約一段時間後仍未簽署時傳送電子郵件提醒
role: Admin
product: adobe sign
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7250.jpg
exl-id: 5a97fade-18a3-448a-8504-efb9e38e9187
source-git-commit: e02b1250de94ec781e7984c6c146dbae993f5d31
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 2%

---

# 使用適用于 Microsoft Dynamics 365 和 Marketo 的 Acrobat Sign 傳送提醒

瞭解如何在合約一段時間後仍未簽署時傳送電子郵件提醒。 此整合使用 Acrobat Sign、Acrobat Sign for Microsoft Dynamics、Marketo 以及 Marketo Microsoft Dynamics Sync。

## 必要條件

1. 安裝 Marketo Microsoft Dynamics Sync。

   有關 Microsoft Dynamics Sync 的資訊和最新外掛程式，請參閱 [ 這裡。](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. 安裝 [ 適用于 Microsoft Dynamics ](https://appsource.microsoft.com/zh-tw/product/dynamics-365/adobesign.f3b856fc-a427-4d47-ad4b-d5d1baba6f86) 的 Acrobat Sign。

   有關此增效模組的資訊請參閱 [ 這裡。](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## 尋找自訂物件

Marketo Microsoft Dynamics Sync 和 Acrobat Sign for Dynamics 設定完成後，Marketo Admin Terminal 中會出現兩個新選項。

![管理員](assets/adminTerminal.png)

1. 按一下 **[!UICONTROL 「Dynamics 實體同步」]** 。

   同步自訂實體之前，必須停用同步。 如果這是您第一次這麼做，請按一下 **「同步結構** 」。 否則，請按一下 **「重新整理結構」** 。

   ![重新整理](assets/refreshSchema.png)

## 同步自訂物件

1. 在右側找到 [!UICONTROL  「商機 ] 」、 [!UICONTROL  「連絡人 ] 」和 [!UICONTROL  「帳戶 ] 」自訂物件。

   * **如果您想要在商 ] 機未在 Dynamics 中簽署合約時 [!UICONTROL  傳送提醒，請為「商機」底下****的物件啟用同步** 。

   * **如果您想要在連絡人尚未在 Dynamics 中簽署合約時 [!UICONTROL  傳送提醒，請為「聯繫 ]]** 人」底下 **[!UICONTROL 的物件啟用同步** 。

   * **如果您想要在帳戶尚未在 Dynamics 中簽署合約時 [!UICONTROL  傳送提醒，請為「帳戶 ] 」底下****的物件啟用同步** 。

   * **在所需的父級 （ [!UICONTROL  商機 ] 、 [!UICONTROL  連絡人 ] 或 [!UICONTROL  帳戶） 下方，啟用合約物件的同步** 功能 ] 。 ]****[!UICONTROL 

   ![自訂物件](assets/enableSyncDynamics.png)

1. 在新視窗中，根據「合約」選取您要的屬性，然後啟用「限制 **」和** 「觸發」 **下方** 的方塊，以將其公開至您的行銷活動。

   ![自訂同步 1](assets/entitySync1.png)

   ![自訂同步 2](assets/entitySync2.png)

1. 在自訂物件上啟用同步後，重新開機同步。

   返回管理員終端機，按一下 Microsoft Dynamics **，然後按一下** 「啟用同步」 **。**

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![啟用全域](assets/enableGlobalDynamics.png)

## 建立程式和權杖

1. 在 Marketo 的「行銷活動」區段中，以滑鼠右鍵按一下 **左列的「行銷活動** 」。

   選 **取「新增Campaign資料夾」，然後命名資料夾** 。

   ![新檔案夾](assets/newFolder.png)

1. 在建立的檔案夾上按一下滑鼠右鍵，選取 **「新增程式** 」，然後命名。

   將其他一切保留為預設值，然後按一下「 **建立」** 。

   ![新方案 1](assets/newProgram1.png)

   ![新方案 2](assets/newProgram2.png)

1. 按一下「 **我的權杖** 」，然後將「電子郵件腳本」 **拖** 曳到畫布上。

   ![電子郵件腳本](assets/emailScript.png)

1. 指定名稱，然後按一下「按一下 **以編輯」** 。

   ![命名和編輯](assets/nameAndSave.png)

1. 展開 **[!UICONTROL 右側的「自訂物件]** 」，然後展開「 **[!UICONTROL 合約]** 」物件。

   在畫布上尋找並拖 [!UICONTROL  曳「名稱 ] 」、「合約狀態」、「已傳送」和「目前簽署者 URL」。

1. 使用這些權杖撰寫速度腳本，以顯示一周未簽署的合約URL。 以下是將目前日期與「傳送開啟」相比較的範例：

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

個人化範例包括：簽署者的姓名、合約名稱、合約的連結等等。

1. 在您建立的程式上按一下滑鼠右鍵，然後按一下「 **[!UICONTROL 新增本機資產]** 」，然後選取 **[!UICONTROL 「電子郵件」]** 。

   ![新電子郵件](assets/createNewEmail.png)

1. 在新標籤中，輸入電子郵件的 **[!UICONTROL 「名稱]** 」和 **[!UICONTROL 「說明]** 」，然後從範本選擇器選取範本。

   ![範本選擇器](assets/templatePicker.png)

1. 按一下「**[!UICONTROL 建立]**」。

1. 設定「來自名稱 ]**」和**[!UICONTROL  「 **[!UICONTROL 寄件者位址」]** 。

   ![提醒電子郵件](assets/reminderEmail.png)

1. 按一下訊息內文以啟用編輯器。

   按一下「 **[!UICONTROL 插入權杖」]** 按鈕，尋找您建立的自訂合約URL權杖，然後按一下「 **[!UICONTROL 插入」]** 。 完成電子郵件自訂，然後按一下「儲存 **[!UICONTROL 」]** 。

   ![插入字元](assets/insertToken.png)

1. 使用已指派合約的設定檔預覽。

   您應該會看到「合約名稱」為標籤的URL連結。

   ![電子郵件連結](assets/emailLink.png)

## 設定智慧型Campaign濾鏡

1. 在您建立的程式上按一下滑鼠右鍵，然後按一下 **[!UICONTROL 「新增智慧型Campaign]** 」。

   ![智慧型Campaign 1](assets/smartCampaign1.png)

1. 指定您選擇的名稱，然後按一下「 **[!UICONTROL 建立」]** 。

   ![智慧型Campaign 2](assets/smartCampaign2.png)

1. Search用，然後按一下「合約已 ]**存取智慧型清單」，然後按一下並拖**[!UICONTROL  曳至「智慧型清單」。

   ![有合約](assets/hasAgreementDynamics1.png)

   您向觸發程式顯示的欄位應該可在「新增限制 ]**」中**[!UICONTROL  使用。

1. 選取 **[!UICONTROL 「合約狀態」]** 以及您要篩選的其他任何欄位。

   對於新增的每個欄位，定義要篩選的值。 在此情況下，它只會在合約狀態為「已傳出進行簽署 ***[!UICONTROL 」時觸發，且「傳送至」*]** 會在超過 1 周 *之前觸發&#x200B;**[!UICONTROL 。*]**

   ![合約狀態](assets/hasAgreementDynaSentOn.png)

   >[!NOTE]
   >
   > 如果您希望此行銷活動只針對特定合約執行，可在限制 （例如「名稱 **」）** 中新增唯一識別碼。

1. 確認行銷活動受眾，並查看誰符合「排程」標籤的資格。

   ![限定 符](assets/qualifiers.png)

## 設定智慧型Campaign流程

由於使用了行銷活動篩選 **器「到期前** 天數」，您可以針對行銷活動使用排程的重複性。

1. 按一下「智慧型 **[!UICONTROL Campaign中的 [!UICONTROL  「流量]** 」索引標籤 ] 。

   Search，將「傳送電子郵件 **」流程拖** 曳到畫布上，然後選取您在上一個區段中建立的提醒電子郵件。

   ![傳送電子郵件](assets/sendEmail.png)

1. 按一下智慧型 **[!UICONTROL Campaign中的「排]** 程」標籤。 確保行銷活動流程僅限於「智慧型Campaign設定」中 **每人只執行一** 次。 然後，按一下「 **排程重複」索引** 標籤。

   ![「排程」索引標籤](assets/scheduleTab.png)

1. 將「 **排程」** 設為「 _每日」_ 。 必要時選擇行銷活動的開始日期和時間及結束日期。

   ![排程設定](assets/scheduleSettings.png)

>[!TIP]
>
>本教學課程 [ 包含Acrobat適用于 Microsoft Dynamics 和 Marketo ](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) 的 Acrobat Sign 可在 Experience League 上免費取得，以加速銷售週期！