---
title: "指定替代快照集資料夾位置 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "快照集 [SQL Server 複寫], 替代資料夾位置"
  - "快照式複寫 [SQL Server], 替代資料夾位置"
  - "替代快照集資料夾 [SQL Server 複寫]"
ms.assetid: 9293f0eb-5531-47ec-b6e2-0392823ce5cc
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# 指定替代快照集資料夾位置 (SQL Server Management Studio)
  在 [指定替代快照集位置 **快照集** 頁面 **發行集屬性-\< 發行集>** 對話方塊。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。  
  
### 若要指定替代快照集位置  
  
1.  在 **快照** 頁面 **發行集屬性-\< 發行集>** ] 對話方塊中︰  
  
    1.  選取 **[將檔案放在下列資料夾中]**，然後按一下 **[瀏覽]** 以瀏覽至目錄，或者輸入應儲存快照集檔案之目錄的路徑。  
  
        > [!NOTE]  
        >  快照集代理程式必須有您指定之目錄的寫入權限，而散發代理程式或合併代理程式則必須有讀取權限。 如果使用提取訂閱，您必須指定共用的目錄做為通用的命名慣例 (UNC) 路徑，例如 \\\computername\snapshot。 如需詳細資訊，請參閱 [保護快照集資料夾](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
    2.  除非您需要將快照集檔案寫入兩個位置，否則請清除 **[將檔案放在預設資料夾]** 。  
  
     若要壓縮快照集檔案，請選取 **壓縮快照集檔案，在此位置**。 壓縮通常用於低頻寬連接和抽取式媒體上的替代快照集位置，例如 CD-ROM。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## 另請參閱  
 [替代快照集資料夾位置](../../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [設定快照集屬性和 #40。複寫 TRANSACT-SQL 程式設計 & #41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [指定預設快照集位置 & #40。SQL Server Management Studio & #41;](../../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)   
 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [使用快照集初始化訂閱](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  