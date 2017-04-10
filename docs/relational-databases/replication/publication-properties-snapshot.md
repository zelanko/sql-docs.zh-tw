---
title: "發行集屬性，快照集 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.pubproperties.snapshotformat.f1"
ms.assetid: 8e9133b1-fc37-4a85-8a7c-d5eaf172fbef
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# 發行集屬性，快照集
  **[發行集屬性]** 對話方塊的 **[快照集]** 頁面，可以讓您設定快照集格式、快照集資料夾位置以及在快照集的應用程式之前和之後執行的指令碼。 快照集資料夾必須指定為共用，而且會讀取和寫入檔案到資料夾的代理程式需要有足夠的權限。 如需有關適當地設定資料夾的詳細資訊，請參閱 [保護快照集資料夾](../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
> [!NOTE]  
>  發行集需要有新的快照集才能進行變更。 如需詳細資訊，請參閱 [變更發行集與發行項屬性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
## 選項  
 **快照集格式**  
 為快照集格式選取原生模式或字元模式。  
  
-   選取 **原生 SQL Server-所有訂閱者必須是執行 SQL Server 伺服器** 若所有的訂閱者的執行個體 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)]。 原生快照集格式可以提供最佳的效能。  
  
-   選取 **字元-如果發行者或訂閱者沒有執行 SQL Server 則需要** 如果任何 「 訂閱者 」 執行 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 或為非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 「 訂閱者 」。  
  
 **快照集檔案的位置**  
 選取儲存快照集檔案的位置。 這些檔案可以儲存在預設位置；也可以儲存在取代預設位置的替代位置，或除了預設位置以外的替代位置。 儲存在替代位置的檔案可以壓縮。  
  
-   選取 **[將檔案放在預設資料夾]** ，以使用發行者的預設快照集資料夾。 快照集資料夾位置是唯讀，在此對話方塊中，因為它只在 「 發行者 」 的變更 **散發者屬性** 對話方塊。 如需詳細資訊，請參閱 [指定預設快照集位置 & #40。SQL Server Management Studio & #41;](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)。  
  
-   選取 **[將檔案放在下列資料夾中]** ，以指定取代預設位置的替代位置，或除了預設位置以外的替代位置。 在文字方塊中輸入路徑，或按一下 **[瀏覽]** 並瀏覽到適當位置。 選取 **[壓縮此資料夾中的快照集檔案]** ，以壓縮在替代快照集位置中的檔案。 替代位置可以位於其他伺服器、網路磁碟機或抽取式媒體 (例如 CD-ROM 或抽取式磁碟) 上。 如需相關資訊，請參閱 [Alternate Snapshot Folder Locations](../../relational-databases/replication/alternate-snapshot-folder-locations.md) 及 [Compressed Snapshots](../../relational-databases/replication/compressed-snapshots.md)。  
  
 **執行其他指令碼**  
 指定在訂閱者端套用快照集之前和之後要執行的指令碼。 如果 **[快照集格式]** 是 **[字元]**，則無法指定指令碼。  
  
 指令碼是選擇性的，但可提供便於執行命令以及在訂閱者端套用管理變更的方式。 如需有關如何執行指令碼的詳細資訊，請參閱 [執行指令碼之前和之後套用快照集](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)。  
  
-   在 **[套用快照集之前執行此指令碼]** 文字方塊中輸入路徑，或按一下 **[瀏覽]** 以指定指令碼的位置。  
  
-   在 **[套用快照集之後執行此指令碼]** 文字方塊中輸入路徑，或按一下 **[瀏覽]** 以指定指令碼的位置。  
  
## 另請參閱  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [檢視及修改發行集屬性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [建立和套用初始快照集](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [使用快照集初始化訂閱](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  