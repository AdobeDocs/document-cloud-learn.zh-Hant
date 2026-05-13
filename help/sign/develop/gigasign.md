---
title: 使用GigaSign收集大量檔案
description: Gigasign可讓您同時傳送、收集及追蹤數千人要簽名的檔案
feature: Workflow
role: Developer
level: Intermediate
jira: KT-6626
topic-revisit: Integrations
thumbnail: 328113.jpg
exl-id: a59eab61-fe61-45c6-8137-f074e1f2b3ed
TQID: https://experienceleague.adobe.com/62xUXPGJ-H5XyknrYgKSEErD-mW0zIZc-qxQJvzXgCM
product_v2:
  - id: b12c730b-5ddb-4a2d-ba42-da774988b909
  - id: c1c5fb98-9105-44ed-9df1-9e04d062a784
  - id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
  - id: f002a92a-b99f-47a4-90c8-65e0e415bc7a
feature_v2:
  - id: a1028f9a-6dbc-4a4f-adf5-eb9f85a408a6
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: d92345097c162b68b9d8405122534371c87c5f1a
workflow-type: tm+mt
source-wordcount: 331
ht-degree: 2%

---

# 使用GigaSign收集大量檔案

Gigasign可讓您同時傳送、收集及追蹤數千人要簽名的檔案。 專為與員工和客戶進行大量通訊而設計，每次大量傳送時可支援最多2,500位收件者。 GigaSign使用Acrobat Sign API以提供與MegaSign相同的功能，並包含對多個簽署者、收件者群組、收件者角色、合約名稱、副本等的支援。

>[!IMPORTANT]
>
>GigaSign不再更新至最新版的Java或Acrobat Sign，僅提供有限支援。 正在將GigaSign的功能新增至產品中的[大量傳送](https://experienceleague.adobe.com/docs/document-cloud-learn/sign-learning-hub/admin-set-up/getting-started-admin/megasign.html?lang=zh-Hant？)功能。 對於未明確要求使用GigaSign的所有使用案例，請使用大量傳送。

>[!VIDEO](https://video.tv.adobe.com/v/3453521?captions=chi_hant&quality=12&learn=on&hidetitle=true)

## 下載並安裝GigaSign應用程式

[下載GigaSign Zip檔案](https://acrobat.adobe.com/id/urn:aaid:sc:US:001cf62d-1cab-46c7-aa96-661ac8680206)

[Java 1.8下載連結（僅限需要時）](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html){target="_blank"} 

[白名單的IP位址（僅在需要時提供）](https://helpx.adobe.com/tw/sign/system-requirements.html#IPs){target="_blank"}

## 基本設定指示

1. 登入您的Acrobat Sign帳戶。

1. 按一下頂端顯示的&#x200B;**[!UICONTROL 群組]**&#x200B;或&#x200B;**[!UICONTROL 帳戶]**。

1. 在畫面左側的搜尋欄位中輸入「存取權杖」。

1. 按右側的「+」圖示。

1. 建立包含所需範圍(User_Read、Agreement_Read、Agreement_Write、Agreement_Send、Library_Read)的金鑰。

1. 連按兩下您建立的金鑰並複製全文（它會從畫面右側移出，因此請確定您已全部取得）。

1. 開啟GigaSign。

1. 按一下右上角的&#x200B;**[!UICONTROL 設定]**&#x200B;圖示。

1. 在第一行貼上整合索引鍵。

1. 在第二行中輸入用來建立該金鑰的帳戶的電子郵件地址。

1. 按一下「**[!UICONTROL 送出]**」。
