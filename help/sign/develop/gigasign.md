---
title: 使用 GigaSign 收集大量檔
description: Gigasign 可讓您同時傳送、收集和追蹤檔以索取簽名給成千上萬的人
feature: Workflow
role: Developer
level: Intermediate
jira: KT-6626
topic-revisit: Integrations
thumbnail: 328113.jpg
exl-id: a59eab61-fe61-45c6-8137-f074e1f2b3ed
source-git-commit: 84aa3c18e0da0d4e5c83130c4e3303407ebf784a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 1%

---

# 使用 GigaSign 收集大量檔

Gigasign 可讓您同時傳送、收集和追蹤檔以索取簽名給成千上萬的人。 這是專為與您的員工和客戶進行大量通訊所設計，支援多達 2,500 位收件者，每個都可大量傳送。 GigaSign 使用 Acrobat Sign API 提供與 MegaSign 相同的功能，並包含對多位簽署者、收件者群組、收件者角色、合約名稱、Carbon 副本等的支援。

>[!VIDEO](https://video.tv.adobe.com/v/328113?quality=12&learn=on&hidetitle=true)

## 下載並安裝 GigaSign 應用程式

[下載 GigaSign Zip 檔案](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:d1a3f4f2-0f7b-466f-9785-81dff2217776)

[JAVA 1.8 下載連結 （僅需視需要） ](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html) {target="_blank"}

[IP 位址至白名單 （僅視需要）](https://helpx.adobe.com/tw/sign/system-requirements.html#IPs){target="_blank"}

## 基本設定指示

1. 登入您的 Acrobat Sign 帳戶。

1. 按一下 **[!UICONTROL 「群組]** 」或 **[!UICONTROL 「帳戶]** 」，無論您在頂端看到哪一個。

1. 在畫面左側的搜尋欄位中輸入「存取權杖」。

1. 按右側的「+」圖示。

1. 建立具有所需範圍的金鑰 （User_Read、Agreement_Read、Agreement_Write、Agreement_Send、Library_Read）。

1. 按兩下您建立的金鑰並複製完整文字 （該文字會從畫面向右移，因此請確定您已全部取得）。

1. 開啟 GigaSign。

1. **[!UICONTROL 按一下右上方的「設定」]** 圖示。

1. 在第一行貼上整合金鑰。

1. 在第二行輸入用來建立該金鑰的帳戶電子郵件地址。

1. 按一下「**[!UICONTROL 送出]**」。
