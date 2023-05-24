---
title: 適用于 Microsoft Power Platform 的 Acrobat Sign 的檔自動化
description: 瞭解如何啟用和使用適用于 Microsoft Power Apps 的 Acrobat Sign 和 Adobe PDF Tools 連接器。 建立無需任何程式碼即可快速且安全地自動化業務審批和簽名流程的工作流程
role: User, Developer
level: Intermediate
topic: Integrations
thumbnail: KT-7488.jpg
kt: 7488
exl-id: 4113bc3f-293c-44a8-94ab-e1dbac74caed
source-git-commit: e02b1250de94ec781e7984c6c146dbae993f5d31
workflow-type: tm+mt
source-wordcount: '2436'
ht-degree: 1%

---

# 使用適用于 Microsoft Power Platform 的 Acrobat Sign 進行檔自動化

瞭解如何啟用和使用適用于 Microsoft Power Apps 的 Acrobat Sign 和 Adobe PDF Tools 連接器。 建立工作流程，無需任何程式碼即可快速且安全地自動化業務審批和簽名流程。 這個實作教學課程有四個部分，概述下列連結：

<table style="table-layout:fixed">
<tr>
  <td>
    <a href="documentautomation.md#part1">
        <img alt="第 1 部分：使用 Acrobat Sign 將已簽署的合約儲存在 SharePoint 中" src="assets/documentautomation/AutomationPart1_thumb.jpg" />
    </a>
    <div>
    <a href="documentautomation.md#part1"><strong>第 1 部分：使用 Acrobat Sign 將已簽署的合約儲存在 SharePoint 中</strong></a>
    </div>
  </td>
  <td>
    <a href="documentautomation.md#part2">
        <img alt="第 2 部分：自動化核准流程，以使用 Acrobat Sign 取得電子簽名" src="assets/documentautomation/AutomationPart2_thumb.jpg" />
    </a>
    <div>
    <a href="documentautomation.md#part2"><strong>第 2 部分：自動化核准流程，以使用 Acrobat Sign 取得電子簽名</strong></a>
    </div>
  </td>
  <td>
   <a href="documentautomation.md#part3">
      <img alt="第 3 部分：配備Adobe PDF工具的自動化檔 OCR" src="assets/documentautomation/AutomationPart3_thumb.jpg" />
   </a>
    <div>
    <a href="documentautomation.md#part3"><strong>第 3 部分：配備Adobe PDF工具的自動化檔 OCR</strong></a>
    </div>
  </td>
  <td>
   <a href="documentautomation.md#part4">
      <img alt="第 4 部分：使用Adobe PDF工具自動化檔元件" src="assets/documentautomation/AutomationPart4_thumb.jpg" />
   </a>
    <div>
    <a href="documentautomation.md#part4"><strong>第 4 部分：使用Adobe PDF工具自動化檔元件</strong></a>
    </div>
  </td>
</tr>
</table>

## 必要條件

* Microsoft 365 和 Power Automate 的熟悉程度
* Acrobat Sign 知識
* 可存取 SharePoint 和 Power Automate 的 Microsoft 365 帳戶 （Acrobat Sign 基本版、Adobe PDF工具進階版）
* Acrobat適用于企業的 Sign 或 Acrobat Sign 開發人員帳戶

**練習 1 和 2**

* Acrobat可存取API的 Sign 帳戶。 開發人員帳戶或企業帳戶。
* 您具有編輯許可權的 Power Automate 可存取 SharePoint 網站。 建議您擁有完整的管理員存取權限。
* 簽名核准要求和簽署的範例檔。

**練習 3 和 4**

在此下載材料 [](https://github.com/benvanderberg/adobe-sign-pdftools-powerautomate-tutorial)

## 第 1 部分：使用 Acrobat Sign 將已簽署的合約儲存在 SharePoint 中 {#part1}

第一部分中，您將使用 Power Automate Flow 範本來設定自動化工作流程，將所有已簽署的合約儲存至 SharePoint 網站。

1. 流覽至「Power Automate」。
1. Search Acrobat簽署。

   ![導覽至 Power Automate 的螢幕擷圖](assets/documentautomation/automation_1.png)

1. 選擇 **「儲存Acrobat簽署已完成的合約至 SharePoint 資料庫** 。

   ![將Acrobat簽署完成的合約儲存至 SharePoint 資料庫動作的螢幕擷圖](assets/documentautomation/automation_2.png)

1. 檢閱畫面並設定任何需要的連線。 啟用 Acrobat Sign 連線。
1. 按一下藍色 `+` 元件。

   ![Acrobat Sign 和 SharePoint 流量連線的螢幕擷圖](assets/documentautomation/automation_3.png)

1. 輸入您的 Acrobat Sign 帳戶電子郵件，然後按一下新視窗中的密碼欄位。

   ![Acrobat登入畫面螢幕擷取](assets/documentautomation/automation_4.png)

   稍候片刻，等待Adobe檢查您的帳戶。

   >[!NOTE]
   >
   >如果您使用的是Adobe ID或公司 SSO，這項檢查會將您路由至適當的登入。

1. 完成登入。
1. 按一下 **「繼續** 」以前往「流程」編輯畫面。
1. 為觸發程式命名。

   ![觸發器命名螢幕擷取畫面](assets/documentautomation/automation_5.png)

1. 設定您的 SharePoint 設定。

   ![設定 SharePoint 設定的螢幕擷圖](assets/documentautomation/automation_6.png)

   **網站位址：** 您的 SharePoint 網站
   **檔案夾路徑：** 您要使用的共用文件路徑
   **檔案名：** 接受預設值
   **檔案內容：** 接受預設值

1. 儲存流程.

   ![儲存圖示的螢幕擷圖](assets/documentautomation/automation_7.png)

1. 使用藍色後箭頭導覽至流程概觀畫面。 您將第 2 部分測試此流程。

   ![流程概觀畫面的螢幕擷圖](assets/documentautomation/automation_8.png)

接下來，您會測試此流程。

## 第 2 部分：自動化核准流程，以使用 Acrobat Sign 取得電子簽名 {#part2}

在第二部分中，我們以更強大的「流程」建立第一個部分，並測試兩個「流程」，以瞭解它們的實際運作。

1. 從 Power Automate 介面選 **取左側的範本** 。

   ![選取範本的螢幕擷圖](assets/documentautomation/automation_9.png)

1. Search進行「管理者核准」。
1. 針對選取的檔案選 **取「要求管理員核准」** 。

   ![選取所選檔案要求管理員核准的螢幕擷圖](assets/documentautomation/automation_10.png)

   檢閱連線並新增任何您缺少的連線。

   >[!NOTE]
   >
   >如果這是您核准後進行的第一個流程，系統會在流程執行時完全設定。

1. 按一下 **「繼續** 」以前往流程編輯畫面。

   此流程具有許多預先設定的步驟，包括錯誤檢查和巢狀條件式步驟。

1. **設定選取的檔案** ，如下所示：
   **網站位址：** 您的 SharePoint 網站
   **資料庫名稱：** 您的檔存放庫
1. 請按照下列方法新增輸入：
   **類型** ：電子郵件
   **名稱** ：簽署者電子郵件

   ![設定流程的螢幕擷圖](assets/documentautomation/automation_11.png)

1. 設定「 **取得檔案內容」：** 如下所示：
   **網站位址：** 您的 SharePoint 網站
   **資料庫名稱：** 您的檔存放庫

1. 向下捲動並尋找「 **如果有的話」** 。

   ![「如果是」設定的螢幕擷圖](assets/documentautomation/automation_12.png)

1. 按一下 **「如果是** 」方塊 （不是最底部的） 中的 **「新增動作** 」，以新增要傳送以供簽署的步驟。

   ![在「如果是」方塊中新增動作的螢幕擷圖](assets/documentautomation/automation_13.png)

1. **Search SharePoint 取得檔案內容** ，然後選擇「 **取得檔案內容」** 。

   ![搜尋方塊的螢幕擷圖](assets/documentautomation/automation_14.png)

1. 設定「 **取得檔案內容** 」，如下所示：

   ![取得檔案內容設定的螢幕擷圖](assets/documentautomation/automation_15.png)

   **網站位址：** 您的 SharePoint 網站。
   **檔案識別碼：** Search為「識別碼」，然後從 **「取得檔案內容」步驟中選擇「識別碼」** 。
1. Search「Adobe」，然後選擇 **「Acrobat簽署** 」以新增其他動作。

   ![搜尋選單的螢幕擷圖](assets/documentautomation/automation_16.png)

1. 在「Acrobat Sign 的搜尋方塊中輸入「上傳」，然後選取「 **上傳檔」並取得檔 ID** 。
1. Search「動態變數 **名稱」** ，以取得在觸發程式中選取的專案/檔的名稱，位於「檔案名」 **下方** 。
1. 按一下 **「檔案內容」下方變數助理中的「** 運算式 **」** 。

   ![上傳檔和取得檔 ID 畫面的螢幕擷圖](assets/documentautomation/automation_17.png)

1. 新增單一縮寫符號，然後按一下返回「 **動態內容** 」，刪除縮寫符號，選 **取「檔案內容** 」，然後按一下「 **確定」** 。

   確定沒有額外的省略號，而且看起來就像下列範例一樣。

   ![動態內容畫面應呈現什麼樣貌的螢幕擷圖](assets/documentautomation/automation_18.png)

1. Search在「Acrobat Sign」搜尋區域中進行「建立」，以新增另一個「簽署」Acrobat動作。
1. 從已上傳的檔中選取「 **建立和合約」，並傳送以供簽署** 。

   ![搜尋建立的螢幕擷圖](assets/documentautomation/automation_19.png)

1. 設定所需資訊：
從「合約名稱」 **的動態變數助理中** 選擇 **「名稱」** 。從「檔 ID」的動態變數助理中 **選擇** 「檔 ID **」** 。從「參與者電子郵件 **」的動態變數助理中** 選擇 **「簽署者電子郵件」** 。依參與者順序輸入「1」 **** 。從「參與者角色」下拉式清單中 **選擇** 「簽署者 **」** 。

   ![所需資訊的螢幕擷圖](assets/documentautomation/automation_20.png)

1. **儲存** 流程。

### 測試流程

前往 SharePoint 網站的檔存放庫進行測試。

1. 選取檔，然後選擇 **您剛建立的** 「自動」 **和「流程** 」。

   ![選取「自動」選單和流程的螢幕擷圖](assets/documentautomation/automation_21.png)

1. 啟動流程以驗證連線 （僅限流量第一次執行）。
1. 在「訊息」中輸入給核准者的 **漂亮訊息** 。
1. 在「簽署者電子郵件」中 **輸入檔簽署者的電子郵件** 。
1. 按一下「 **執行流程」** 。

為開始流程的使用者設定的核准者會收到核准要求。 您可以透過電子郵件或透過 Power Automate 動作專案功能表核准。核准後，請簽署檔。 視您的使用者而定，如果使用者已登入 Sign，您可能需要在私人瀏覽器視窗中開啟簽署視窗。

![在私人瀏覽器視窗中開啟的螢幕擷圖](assets/documentautomation/automation_22.png)

完成簽署，然後在 SharePoint 檔案夾中回顧。

![SharePoint 檔案夾的螢幕擷圖](assets/documentautomation/automation_23.png)

## 第 3 部分：配備Adobe PDF工具的自動化檔 OCR {#part3}

第三部分中，您將瞭解如何在 PDF 中匯入至 Microsoft SharePoint 時自動執行 OCR。 這可解決掃描的 PDF 檔在 SharePoint 中無法搜尋的問題。

![瀏覽器中 PDF 檔的螢幕擷圖](assets/documentautomation/automation_24.png)

### 在 SharePoint 中設定資料夾

前往您要儲存檔的 Microsoft SharePoint。

1. 按一下 **「+New** 」，建立名為「處理過的合約」的新資料夾。
1. 按一下 **「+New** 」，建立名為「舊合約」的新檔案夾。

   ![新檔案夾的螢幕擷圖](assets/documentautomation/automation_25.png)

這些資料夾現在會參考您 Power Automate 流程的一部分。

### 從範本建立流程

1. 登入 HTTPs://flow.microsoft.com。
1. 按一下 **側邊欄中的「範本** 」。

   ![選取範本的螢幕擷圖](assets/documentautomation/automation_26.png)

1. 選取 **「在 SharePoint 中將新增的檔案轉換為可搜尋文字的 PDF」** 。
1. 按一下「 **工具Adobe PDF旁的 +** 符號。

   ![選取 + 元件的螢幕擷圖](assets/documentautomation/automation_27.png)

1. 在新索引標籤中流覽至「HTTPs://www.adobe.com/go/powerautomate_getstarted」。
1. 按一下「**開始使用**」。

   ![開始使用按鈕螢幕擷圖](assets/documentautomation/automation_28.png)

1. 使用您的 Adobe ID 登入。

   ![「登入」畫面的螢幕擷圖](assets/documentautomation/automation_29.png)

1. 輸入「認證名稱」和「認證說明」，然後按一下「 **建立認證」** 。

   ![「建立認證」畫面的螢幕擷圖](assets/documentautomation/automation_30.png)

   開啟憑證時保持視窗狀態。 您需要將它們輸入 Microsoft Power Automate。

   ![保持開啟瀏覽器索引標籤的螢幕擷圖](assets/documentautomation/automation_31.png)

1. 輸入憑證，然後按一下 **Microsoft Power Automate 中的「建立」** 。

   ![輸入 PDF 工具認證的螢幕擷圖](assets/documentautomation/automation_32.png)

1. 按一下「**繼續**」。

   ![按一下「繼續」的位置螢幕擷圖](assets/documentautomation/automation_33.png)

   現在您可以查看工作流程的視圖，並且需要為您的環境進行設定。

1. 選取「網站位址」欄位，然後在名為「 **在檔案夾** 中建立檔案時」的觸發器下選擇您正在使用的 SharePoint 網站。

   ![在檔案夾觸發器中建立檔案時的選取螢幕擷圖](assets/documentautomation/automation_34.png)

1. 按一下資料夾圖示，導覽至位於「資料夾 ID」下方的「舊合約」資料夾。

   ![選取「舊合約」檔案夾的螢幕擷圖](assets/documentautomation/automation_35.png)

1. **編輯流程底部的「建立檔案** 」動作：

   將網站位址 **變更** 為您的網站位址。在「檔案夾路徑」中指定「已處理合約」資料夾的位置。

1. **按一下** 右上角的「儲存」。
1. 按一下「 **測試」** 。
1. 手動選 **取** 。
1. 按一下「 **測試」** 。

   ![測試流程的螢幕擷圖](assets/documentautomation/automation_36.png)

### 嘗試新的流程

1. 流覽至 SharePoint 中的「舊合約」資料夾。
1. 在您下載的練習檔案中流覽至「E03/舊合約」。
1. 將 ReleaseFormXX.pdf 檔案複製到 SharePoint 中的「舊合約」資料夾。

   ![複製檔案的螢幕擷圖](assets/documentautomation/automation_37.png)

現在，如果您導覽至「已處理的合約」資料夾，您可以在工作流程完成幾分鐘後看到可使用的 PDF。 如果您開啟 PDF，您會看到該文字可供選取。此外，SharePoint 會為檔建立索引，讓您從 SharePoint 的搜尋列搜尋檔內容。

## 第 4 部分：使用Adobe PDF工具自動化檔元件 {#part4}

第四部分中，您將瞭解如何根據從 Microsoft SharePoint 選取和啟動流程時提供的資訊，將許多檔合併在一起。 在此情況下，流程將會：

* 詢問資訊，以選擇要包含在客戶套件中的內容。
* 會根據所提供的資訊，將許多檔合併在一起。 這些檔包括封面和選擇性白皮書。
* 合併的檔會儲存至 SharePoint。

### 將練習檔案匯入 SharePoint

1. 在「練習」檔案中開啟 E04 檔案夾。
1. 將「提案」、「範本」和「產生的檔」資料夾匯入 SharePoint。

   ![讀入檔案夾的螢幕擷圖](assets/documentautomation/automation_38.png)

這些檔案夾將作為參考。 您特別會針對您的提案使用「提案.docx」檔案。

在「範本」資料夾中，有一個包含不同城市封面頁面設計的封面檔案夾。 還有一個「白皮書」資料夾，其中包含選用的其他白皮書（如果選取的話）。

### 將流程匯入 Microsoft Power Automate

1. 登入 Microsoft Power Automate （HTTPs://flow.microsoft.com）。
1. 按一下「 **我的流程」** 。

   ![選取「我的流程」的位置螢幕擷圖](assets/documentautomation/automation_39.png)

1. 按一下&#x200B;**「讀入」**。

   ![讀入畫面螢幕擷圖](assets/documentautomation/automation_40.png)

1. 按一下 **「上傳** 」，然後在 E04/Flows/中選擇 GenerateProposal_20210311231623.zip 檔案夾。

   ![選取檔案夾的螢幕擷圖](assets/documentautomation/automation_41.png)

1. 按一下&#x200B;**「讀入」**。

1. 按一下「傳送提案給客戶」旁的 **「動作」** 下方的扳手圖示。

   ![扳手圖示的螢幕擷圖](assets/documentautomation/automation_42.png)

1. 在「設定」下，選 **取「以新** 手建立」。
1. 在「資源名稱」下方設定流程名稱。
1. 按一下「**儲存**」。

   對其他相關資源重複此操作，然後選取您的連線。

   ![儲存檔案的螢幕擷圖](assets/documentautomation/automation_43.png)

1. **建立所有連線後，按一下** 「讀入」。

### 為選取的檔案設定

在建立流程後，請執行下列動作：

1. 按一下&#x200B;**「編輯」**。

   ![選取編輯位置的螢幕擷圖](assets/documentautomation/automation_44.png)

1. 選取所選檔案的觸發 **程式** 。

   在「網站位址」中新增 SharePoint 網站。在資料庫中新增資料庫。

   ![已完成觸發程式的螢幕擷圖](assets/documentautomation/automation_45.png)

### 設定範本FolderPath

1. 按一下範本FolderPath 變數。
1. 設定「範本」檔案夾位於您匯入的 SharePoint 網站內的路徑。

### 設定封面 取得檔案內容

1. 按一下 **「封面** 」動作，展開「範圍」。
1. 展開 **封面：取得檔案內容** 。

   將網站位址設定至 SharePoint 網站。

   ![展開封面的螢幕擷圖](assets/documentautomation/automation_46.png)



### 設定選取的檔案

1. 展開「選取的 **檔案範圍」** 動作。

   在「取得檔案內容」下 **方，分別將「網站位址」和「資料庫名稱」變更為您的 SharePoint 網站和資料庫** 。在「取得檔案內容 **」下** 方，將「網站位址」變更為您的 SharePoint 網站。

   ![展開的「選取的檔案」動作的螢幕擷圖](assets/documentautomation/automation_47.png)

### 設定白皮書

1. 按一下 **「白皮書」** 動作。
1. 展開 **條件：新增白皮書** 。

   ![展開新增白皮書條件的螢幕擷圖](assets/documentautomation/automation_48.png)

1. 展開 **白皮書 1：使用路徑** 取得檔案內容。將網站位址編輯到您指定的 SharePoint 網站。

針對 **條件重複相同的步驟：新增白皮書 2** 。

### 設定「建立檔案」

1. 展開 **「建立檔案」** 。

   將「網站位址」和「資料夾路徑」編輯至 SharePoint 網站，以及「產生的檔」資料夾所在的路徑。

1. 按一下「**儲存**」。

### 測試您的流程

1. 流覽至 SharePoint 中的「提案」資料夾。
1. 選取「Recommendations.docx」資料夾。

   ![選取提案資料夾的螢幕擷圖](assets/documentautomation/automation_49.png)

1. 在「自動」選 **單下，** 選取您的流程。

   ![選取「自動」選單的螢幕擷圖](assets/documentautomation/automation_50.png)

1. 按一下 **「繼續** 」以開始流程。

   ![選取「繼續」按鈕的螢幕擷圖](assets/documentautomation/automation_51.png)

1. 選擇您的封面和想要附加的白皮書。
1. 按一下「 **執行流程」** 。

   ![「執行流程」按鈕的螢幕擷圖](assets/documentautomation/automation_52.png)

導覽至「產生檔」資料夾。 您現在應該會看到產生的 PDF 檔案。

![使用新 PDF 檔案的 SharePoint 目錄螢幕擷圖](assets/documentautomation/automation_53.png)

### 在流程中加入「保護」和其他動作

現在您已成功建立流程，您將會編輯流程，以密碼加密 PDF 檔。 這也會逐步說明如何運用其他動作。

1. 導覽回您的流程結束。
1. **按一下合併 PDF** 和 **建立檔案** 之間的 **+** 符號。

   ![選取 + 元件位置的螢幕擷圖](assets/documentautomation/automation_54.png)

1. 選取 **「新增動作」** 。
1. 「Adobe PDF工具」的Search。

   ![搜尋 Adobe PDF 的螢幕擷圖](assets/documentautomation/automation_55.png)

1. 選取 **「保護 PDF 不受檢視」** 。
1. 使用「動態內容」，在「合併 PDF」中將「檔案名」欄位設為 **PDF** 檔案名。

   ![動態內容的螢幕擷圖](assets/documentautomation/automation_56.png)

   觸發時，啟動表單中有一個「密碼」欄位。 我們可以在這裡使用。

1. **Search使用動態內容的「密碼」欄位** ，然後將其放置在「密碼」欄位中。

   ![搜尋密碼的螢幕擷圖](assets/documentautomation/automation_57.png)

1. 使用「動態內容」在 **「檔案內容」欄位中，將其設為「合併 PDF 檔案內容」中的 PDF** 檔案內容。
1. 變更「 **建立檔案」** ，從「保護 PDF」取得檔案內容，而非「合併 PDF」。
1. 展開 **「建立檔案」** 。
1. 清除「檔案內容」欄位。
1. 使用動態內容置入 **「保護 PDF 免于** 檢視 **」的 PDF 檔案內容** 。

### 測試您的流程

1. 流覽至 SharePoint 中的「提案」資料夾。
1. 選取「Recommendations.docx」。

   ![選取「提案」檔案夾的螢幕擷圖](assets/documentautomation/automation_58.png)

1. 選取 **「自動」** 以選擇您的流程。

   ![從選單中選取「自動」的螢幕擷圖](assets/documentautomation/automation_59.png)

1. 按一下 **「繼續** 」以開始流程。

   ![選取「繼續」的螢幕擷圖](assets/documentautomation/automation_60.png)

1. 選擇要附加的封面和白皮書。
1. 將「密碼」欄位設定為您要設定的「密碼」。
1. 按一下「 **執行流程」** 。

   ![選定檔案的螢幕擷圖和「執行流程」按鈕](assets/documentautomation/automation_61.png)

1. 導覽至「產生檔」資料夾。您應該會看到產生的 PDF 檔案。 開啟 PDF 檔案，系統會提示您輸入 PDF 密碼。

   ![SharePoint 目錄中產生的 PDF 螢幕擷圖](assets/documentautomation/automation_62.png)
