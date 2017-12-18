---
title: "建立並套用快照集 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], applying
- snapshots [SQL Server replication], creating
ms.assetid: 631f48bf-50c9-4015-b9d8-8f1ad92d1ee2
caps.latest.revision: "38"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6729d35310c914b711b8054f7feccbe6bde465aa
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="create-and-apply-the-snapshot"></a>建立並套用快照集
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 快照集在發行集建立之後由「快照集代理程式」產生。 它們可以：  
  
-   立即產生。 依預設，在「新增發行集精靈」中建立發行集後會立即產生合併式發行集的快照集。  
  
-   在排程時間產生。 在「新增發行集精靈」的 **[快照集代理程式]** 頁面上指定排程，或在使用預存程序或 Replication Management Objects (RMO) 時指定排程。  
  
-   手動。 在命令提示下或從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]執行「快照集代理程式」。 如需執行代理程式的詳細資訊，請參閱[複寫代理程式可執行檔概念](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)和[啟動及停止複寫代理程式 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)。  
  
 針對合併式複寫，每次執行快照集代理程式都會產生快照集。 針對異動複寫，是否產生快照集是依照發行集屬性 **immediate_sync**的設定而定。 若屬性設定為 TRUE (使用新增發行集精靈的預設)，每次執行快照集代理程式都會產生快照集，同時隨時可套用至訂閱者。 若屬性設定為 FALSE (使用 **sp_addpublication**時的預設)，則只有在上次執行快照集代理程式後有加入新訂閱的情況下，才會產生快照集。訂閱者必須等待快照集代理程式完成，才能同步處理。  
  
 依預設，快照集產生後會儲存在「散發者」上的預設快照集資料夾中。 您也可以將快照集檔案儲存於抽取式媒體，例如卸除式磁碟機、CD-ROM 或預設快照集資料夾之外的位置。 此外，您可以壓縮檔案，使它們更易儲存和傳送，還可以在快照集套用至「訂閱者」端前後執行指令碼。 如需這些選項的詳細資訊，請參閱 [Snapshot Options](../../relational-databases/replication/snapshot-options.md)。  
  
 若快照集是專為使用參數化篩選的合併式發行集而產生，該快照集會使用兩部份處理建立而成。 首先建立結構描述快照集，其中包含複寫指令碼和已發行物件的結構描述，但不包含資料。 接下來每個訂閱皆以快照集初始化，該快照集中包含從結構描述快照集複製而來的指令碼和結構描述，以及屬於訂閱分割的資料。 如需詳細資訊，請參閱 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)。  
  
 快照集在「發行者」端建立，並儲存於預設或替代的快照集位置之後，可以傳送「訂閱者」並進行套用。 初始同步處理期間，「散發代理程式」 (用於快照式或異動複寫) 或「合併代理程式」 (用於合併式複寫) 會傳送快照集，並將結構描述和資料檔套用至「訂閱者」端的訂閱資料庫。 依預設，如果您使用「新增訂閱精靈」，初始同步處理便會在建立訂閱之後立即進行。 此行為由精靈 **[初始化訂閱]** 頁面上的 **[初始化時機]** 選項控制。 快照集在訂閱初始化之後產生時，不會套用至「訂閱者」，除非訂閱已標示為要重新初始化。 如需詳細資訊，請參閱 [重新初始化訂閱](../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
 「散發代理程式」或「合併代理程式」套用初始化快照集後，代理程式會傳播後續的更新以及其他資料修改。 快照集散發並套用至「訂閱者」後，只有等待初始快照集或新快照集的「訂閱者」會受影響。 該發行集的其他「訂閱者」(收到對已發行資料之插入、更新、刪除或其他修改的「訂閱者」) 均不受影響。  
  
 若要建立和套用初始快照集，請參閱＜ [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)＞。  
  
 若要檢視或修改預設的快照資料夾位置，請參閱  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]：[指定預設快照集位置 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)  
  
-   複寫程式設計和 RMO 程式設計： [Configure Publishing and Distribution](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用快照集初始化訂閱](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [保護快照集資料夾](../../relational-databases/replication/security/secure-the-snapshot-folder.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)  
  
  
