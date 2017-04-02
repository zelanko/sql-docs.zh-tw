---
title: "建立並套用快照集 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "快照集 [SQL Server 複寫], 套用"
  - "快照集 [SQL Server 複寫], 建立"
ms.assetid: 631f48bf-50c9-4015-b9d8-8f1ad92d1ee2
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# 建立並套用快照集
  快照集在發行集建立之後由「快照代理程式」產生。 它們可以：  
  
-   立即產生。 依預設，在「新增發行集精靈」中建立發行集後會立即產生合併式發行集的快照集。  
  
-   在排程時間產生。 指定的排程上 **快照集代理程式** 頁面的 「 新增發行集精靈 」，或使用預存程序或 Replication Management Objects (RMO)。  
  
-   手動。 在命令提示下或從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 執行「快照集代理程式」。 如需執行代理程式的詳細資訊，請參閱 [複寫代理程式可執行檔概念](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) 和 [啟動和停止複寫代理程式 & #40。SQL Server Management Studio & #41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)。  
  
 針對合併式複寫，每次執行快照集代理程式都會產生快照集。 對於異動複寫，產生快照集取決於發行集屬性的設定 **immediate_sync**。 若屬性設定為 TRUE (使用新增發行集精靈的預設)，每次執行快照集代理程式都會產生快照集，同時隨時可套用至訂閱者。 如果此屬性設定為 FALSE (預設值使用時 **sp_addpublication**)，因為最後一個快照集代理程式執行時，已加入新的訂閱時，才會產生快照集「 訂閱者 」 必須等到完成後才可以在同步處理快照集代理程式。  
  
 依預設，快照集產生後會儲存在「散發者」上的預設快照集資料夾中。 您也可以將快照集檔案儲存於抽取式媒體，例如卸除式磁碟機、CD-ROM 或預設快照集資料夾之外的位置。 此外，您可以壓縮檔案，使它們更易儲存和傳送，還可以在快照集套用至「訂閱者」端前後執行指令碼。 如需有關這些選項的詳細資訊，請參閱 [快照集選項](../../relational-databases/replication/snapshot-options.md)。  
  
 若快照集是專為使用參數化篩選的合併式發行集而產生，該快照集會使用兩部份處理建立而成。 首先建立結構描述快照集，其中包含複寫指令碼和已發行物件的結構描述，但不包含資料。 接下來每個訂閱皆以快照集初始化，該快照集中包含從結構描述快照集複製而來的指令碼和結構描述，以及屬於訂閱分割的資料。 如需相關資訊，請參閱 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)。  
  
 快照集在「發行者」端建立，並儲存於預設或替代的快照集位置之後，可以傳送「訂閱者」並進行套用。 初始同步處理期間，「散發代理程式」 (用於快照式或異動複寫) 或「合併代理程式」 (用於合併式複寫) 會傳送快照集，並將結構描述和資料檔套用至「訂閱者」端的訂閱資料庫。 依預設，如果您使用「新增訂閱精靈」，初始同步處理便會在建立訂閱之後立即進行。 這種行為會受到 **初始化時機** 選項 **初始化訂閱** 精靈頁面。 快照集在訂閱初始化之後產生時，不會套用至「訂閱者」，除非訂閱已標示為要重新初始化。 如需詳細資訊，請參閱 [重新初始化訂閱](../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
 「散發代理程式」或「合併代理程式」套用初始化快照集後，代理程式會傳播後續的更新以及其他資料修改。 快照集散發並套用至「訂閱者」後，只有等待初始快照集或新快照集的「訂閱者」會受影響。 該發行集的其他「訂閱者」(收到對已發行資料之插入、更新、刪除或其他修改的「訂閱者」) 均不受影響。  
  
 若要建立和套用初始快照集， [建立和套用初始快照集](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
 若要檢視或修改預設的快照資料夾位置，請參閱  
  
-   [!包含 [ssManStudioFull] (.../ Token/ssManStudioFull_md.md)]: [Specify the Default Snapshot Location &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)  
  
-   複寫程式設計和 RMO 程式設計︰ [設定發行與散發](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
## 另請參閱  
 [使用快照集初始化訂閱](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [保護快照集資料夾](../../relational-databases/replication/security/secure-the-snapshot-folder.md)   
 [sp_addpublication & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)  
  
  