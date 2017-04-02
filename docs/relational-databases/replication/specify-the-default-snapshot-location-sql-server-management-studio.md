---
title: "指定預設快照集位置 (SQL Server Management Studio) | Microsoft Docs"
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
  - "快照集 [SQL Server 複寫], 預設位置"
  - "預設快照集位置"
ms.assetid: 27c5d9ad-a915-4c59-a8b7-82e3af61ac4d
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# 指定預設快照集位置 (SQL Server Management Studio)
  指定預設快照集位置上 **快照集資料夾** 頁面的 「 設定散發精靈 」。 如需使用此精靈的詳細資訊，請參閱 [設定發行與散發](../../relational-databases/replication/configure-publishing-and-distribution.md)。 如果您未設定為散發者的伺服器上建立發行集，指定預設快照集位置上 **快照集資料夾** 新的發行集精靈] 頁面。 如需使用此精靈的詳細資訊，請參閱 [建立發行集](../../relational-databases/replication/publish/create-a-publication.md)。  
  
 修改預設快照集位置上 **發行者** 頁面 **散發者屬性-\< 散發者>** 對話方塊。 如需詳細資訊，請參閱 [檢視和修改 「 散發者 」 和 「 發行者 」 屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)。 設定在每個發行集的快照集資料夾 **發行集屬性-\< 發行集>** 對話方塊。 如需詳細資訊，請參閱 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
### 若要修改預設快照集位置  
  
1.  在 **發行者** 頁面 **散發者屬性-\< 散發者>** 對話方塊方塊中，按一下 [內容] 按鈕 (**...**) 您想要變更預設快照集位置的 「 發行者 」。  
  
2.  在 **發行者屬性-\< 發行者>** ] 對話方塊中，輸入的值 **預設快照集資料夾** 屬性。  
  
    > [!NOTE]  
    >  快照集代理程式必須有您指定之目錄的寫入權限，而散發代理程式或合併代理程式則必須有讀取權限。 如果使用提取訂閱，您必須指定共用的目錄做為通用的命名慣例 (UNC) 路徑，例如 \\\computername\snapshot。 如需詳細資訊，請參閱 [保護快照集資料夾](../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## 另請參閱  
 [替代快照集資料夾位置](../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [使用快照集初始化訂閱](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  