---
title: 使用 Acrobat Sign for Salesforce 和 Marketo 設定指南傳送提醒
description: 瞭解如何在合約一段時間后仍未簽署時，向 Marketo 傳送電子郵件提醒
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic: Integrations
jira: KT-7248
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: 33aca2e0-2f27-4100-a16f-85ba652c17a3
source-git-commit: 51d1a59999a7132cb6e47351cc39a93d9a38eaeb
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 0%

---

# 使用 Acrobat Sign for Salesforce 和 Marketo 設定指南傳送提醒

瞭解如何在合約一段時間后仍未簽署時，向 Marketo 傳送電子郵件提醒。 此整合使用 Acrobat Sign、Acrobat Sign for Salesforce、Marketo 以及 Marketo 和 Salesforce Sync。

## 必要條件

1. 安裝 Marketo Salesforce 同步。

   如需 Salesforce Sync 的資訊和最新增效模組，請參閱此處 [。](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. 安裝 Acrobat Sign for Salesforce。

   有關此增效模組的資訊請參閱 [這裡。](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## 尋找自定義物件

Marketo Salesforce 同步和 Acrobat Sign for Salesforce 設定完成後，Marketo Admin Terminal 中會出現幾個新選項。

![管理](assets/adminTab.png)

![物件同步](assets/salesforceAdmin.png)

1. 如果這是您第一次這麼做，請按兩下 **「同步結構** 」。 否則，請按下 **「重新整理結構」**。

   ![刷新](assets/refreshSchema1.png)

1. 如果全域同步正在執行，請按兩下「 **停用全域同步」以停用**。

   ![禁用](assets/disableGlobal.png)

1. 按兩下 **「重新整理結構」** 。

   ![重新整理 2](assets/refreshSchema2.png)

## 同步自定義物件

在右側，請參閱「商機」、「聯繫人」和「帳戶型自定義物件」。

**如果您想要在銷售主管尚未在 Salesforce 中簽署合約時傳送提醒，請為「商機」底下的物件啟用同步** 。

**如果您想要在聯繫人尚未在 Salesforce 中簽署合約時傳送提醒，請為「聯繫人」底下的物件啟用同步** 。

**如果您想要在帳戶尚未在 Salesforce 中簽署合約時傳送提醒，請為「帳戶」底下的物件啟用同步** 。

1. **為所需父級 （商機、連絡人或帳戶） 下方顯示的合約物件啟用同步**&#x200B;**&#x200B;**&#x200B;功能。針對其他想要同步的自定義物件執行此動作。

   ![合約物件](assets/agreementObject.png)

1. 下列資產會顯示如何 **啟用同步**。

   ![自訂同步 1](assets/customObjectSync1.png)

   ![自訂同步 2](assets/customObjectSync2.png)

## 顯示自訂物件欄位以觸發

1. 停用全域同步時，選取您為「同步」啟用的合約自定義物件，然後選取「 **編輯可見字段」**。

1. 檢查觸發欄中的「合約名稱」字段，將其顯示在Campaign動作觸發器」中。 檢查要篩選的其他任何欄位，然後按下「 **儲存」**。

   ![編輯可見欄位 1](assets/editVisible1.png)

   ![編輯可見欄位 2](assets/editVisible2.png)

1. 完成啟用自訂物件上的同步並顯示觸發器值時，請記得重新啟用 ync：

   ![啟用全域](assets/enableGlobal.png)

## 建立程式和令牌

1. 在 Marketo 的「行銷活動」區段中，以滑鼠右鍵按兩下 **左列的「行銷活動** 」，選 **取「新增Campaign資料夾」，然後命名該檔案夾**。

   ![新檔案夾](assets/newFolder.png)

1. 在建立的檔案夾上按下滑鼠右鍵，選取 **「新增程式**」，然後命名。 將其他一切保留為預設值，然後按兩下「 **建立」**。

   ![新方案 1](assets/newProgram1.png)

   ![新方案 2](assets/newProgram2.png)

1. 按兩下「**我的令牌**」，然後將「電子郵件腳本」**拖**&#x200B;曳到畫布上。

   ![電子郵件腳本](assets/emailScript.png)

1. 指定名稱，然後按兩下「按下 **以編輯」** 。

   ![命名和編輯](assets/nameAndSave.png)

1. 展開 **右側的「自定義物件** 」，然後展開「 **合約** 」物件。 尋找並拖曳「合約名稱」、「合約狀態」、「已簽署日期」和「簽署」URL到畫布上。

1. 使用這些令牌撰寫速度腳本，以顯示一周未簽署的合約URL。 以下是將目前日期與「已傳送日期」相比較的範例：

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

個人化範例包括：簽署者的姓名、合約名稱、合約的連結等等。

1. 在您建立的程式上按下滑鼠右鍵，然後按下「 **新增本機資產**」，然後選取 **「電子郵件」**。

   ![新電子郵件](assets/createNewEmail.png)

1. 在新索引標籤中，輸入 **電子郵件的「名稱** 」和 **「說明** 」，然後從範本選擇器中選取範本。 按一下&#x200B;**「建立」**。

   ![範本選擇器](assets/templatePicker.png)

1. 設定「來自名稱&#x200B;**」和**「**寄件者位址」**。

   ![提醒電子郵件](assets/reminderEmail.png)

1. 按兩下訊息內文以啟用編輯器。 按兩下「 **插入令牌」** 按鈕，尋找您建立的自訂合約URL令牌，然後按下「 **插入」**。 完成電子郵件自定義，然後按兩下「儲存 **」**。

   ![插入字元](assets/insertToken.png)

1. 使用已指派合約的配置檔預覽。 您應該會看到「合約名稱」為標籤的URL連結。

   ![電子郵件連結](assets/emailLink.png)

## 設定智慧型Campaign濾鏡

1. 在您建立的程式上按兩下滑鼠右鍵，然後按下 **「新增智慧型手機Campaign**」。

   ![智慧型Campaign 1](assets/smartCampaign1.png)

1. 指定您選擇的名稱，然後按兩下「 **建立」**。

   ![智慧型Campaign 2](assets/smartCampaign2.png)

1. Search，然後按兩下「合約已&#x200B;**存取智慧型手機清單」，然後按下並拖**&#x200B;曳至「智慧型清單」。

   ![有合約](assets/hasAgreement.png)

1. 您向觸發程序顯示的欄位現在應可在「新增限制&#x200B;**」中**&#x200B;使用。選取 **「合約狀態」** 以及您要篩選的其他任何欄位。 對於新增的每個欄位，定義要篩選的值。 在此情況下，它只會在合約狀態&#x200B;**為「已傳出進行簽署」，且**「傳送&#x200B;**日期」已超過 7 天時**&#x200B;才會觸發。

   ![合約狀態](assets/agreementStatus.png)

   >[!NOTE]
   >
   > d 如果希望此行銷活動僅針對特定合約執行，則限制的唯一標識碼 （例如 **「合約名稱**」）。

1. 確認營銷活動受眾，並查看誰符合「排程」卷標的資格。

   ![限定 符](assets/qualifiers.png)

## 設定智慧型手機Campaign流程

由於使用了行銷活動篩選器 **「未簽署** 天數」，因此您可以針對營銷活動使用排程的重複。

1. 按兩下智慧型手機Campaign **中的「流程** 」索引標籤。 Search，將「傳送電子郵件&#x200B;**」流程拖**&#x200B;曳到畫布上，然後選取您在上一個區段中建立的提醒電子郵件。

   ![傳送電子郵件](assets/sendEmail.png)

1. 按兩下智慧型手機Campaign **中的「排程** 」標籤。 確保營銷活動流程僅限於「智慧型Campaign設定」中 **每人只執行一**&#x200B;次。 然後，按一下「 **排程重複」索引** 標籤。

   ![「排程」索引標籤](assets/scheduleTab.png)

1. 將時程表&#x200B;**&#x200B;**&#x200B;設定為每日，視需要選擇活動開始日和時間，以及營銷活動的結束日期。

   ![排程設定](assets/scheduleSettings.png)

