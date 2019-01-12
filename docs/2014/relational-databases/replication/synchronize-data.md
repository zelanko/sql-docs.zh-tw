---
title: 同步處理資料 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- synchronization [SQL Server replication], about synchronization
- merge replication synchronization [SQL Server replication]
- scripts [SQL Server replication], synchronization and
- synchronization [SQL Server replication]
- snapshot replication [SQL Server], synchronization
- transactional replication, synchronization
- subscriptions [SQL Server replication], synchronizing
- on demand script execution
- replication [SQL Server], synchronization
- scripts [SQL Server replication]
ms.assetid: 724802f7-7d69-46d3-a330-bd8aa7f53114
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 15f4d85d117b5af09b0f67ef788364be6adad810
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54128558"
---
# <a name="synchronize-data"></a>同步處理資料
  同步資料是指在「訂閱者」端套用初始快照集後，在「發行者」與「訂閱者」之間傳播資料和結構描述變更的處理。 同步處理將會：  
  
-   連續發生，一般出現在異動複寫中。  
  
-   視需要發生，一般出現在合併式複寫中。  
  
-   在排程時間發生，一般出現在快照式複寫中。  
  
 同步處理訂閱時，根據使用的複寫類型將發生不同的處理：  
  
-   快照式複寫。 同步處理意味著「散發代理程式」在「訂閱者」端重新套用快照集，以使訂閱資料庫中的結構描述和資料與發行集資料庫保持一致。  
  
     如果在「發行者」端對資料或結構描述作了修改，則必須生成新的快照集，以將修改傳播到「訂閱者」端。  
  
-   異動複寫。 同步處理意味著「散發代理程式」將更新、插入、刪除和其他更改從散發資料庫傳送到「訂閱者」端。  
  
-   合併式複寫。 同步處理意味著「合併代理程式」將更改從「訂閱者」端上傳到「發行者」端，然後再將更改從「發行者」端下載到「訂閱者」端。 當有衝突時會進行偵測並解決。 資料會被聚合，最終「發行者」端和所有「訂閱者」端都將得到相同的資料值。 如果偵測到並解決了衝突，則將變更一些使用者認可的工作，以根據您定義的原則來解決衝突。  
  
 每次發生同步處理時，快照式發行集都會在「訂閱者」端重新整理整個結構描述，因此所有結構描述變更都將套用至「訂閱者」。 異動複寫與合併式複寫還支援最常見的結構描述變更。 如需詳細資訊，請參閱[對發行集資料庫進行結構描述變更](publish/make-schema-changes-on-publication-databases.md)。  
  
 若要同步處理發送訂閱，請參閱＜ [Synchronize a Push Subscription](synchronize-a-push-subscription.md)＞。  
  
 若要同步處理提取訂閱，請參閱＜ [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md)＞。  
  
 若要設定同步處理排程，請參閱＜ [Specify Synchronization Schedules](specify-synchronization-schedules.md)＞。  
  
 **若要檢視並解決同步處理衝突**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:[檢視並解決合併式發行集的資料衝突 &#40;SQL Server Management Studio&#41;](view-and-resolve-data-conflicts-for-merge-publications.md)  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:[檢視交易式發行集的資料衝突 &#40;SQL Server Management Studio&#41;](view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
## <a name="executing-code-during-synchronization"></a>在同步處理期間執行程式碼  
 複寫支援兩種同步處理時的程式碼執行方法  
  
-   異動複寫與合併式複寫支援視需要的指令碼執行。 視需要的指令碼執行可用於指定要在同步處理期間執行的 SQL 指令碼。 指令碼將複製到「訂閱者」端，並在開始同步處理時使用 **sqlcmd** 來執行。 指令碼套用至「訂閱者」後，便不具有對已複寫變更的存取權。 如需詳細資訊，請參閱[在同步處理期間執行指令碼 &#40;複寫 Transact-SQL 程式設計&#41;](execute-scripts-during-synchronization-replication-transact-sql-programming.md)。  
  
-   合併式複寫支援商務邏輯處理常式。 您可以使用商務邏輯處理常式架構來撰寫受管理的程式碼組件，該組件將在合併同步處理期間中被呼叫。 組件包括可對應至幾種同步處理條件的商務邏輯：資料變更、衝突和錯誤。 如需詳細資訊，請參閱[在合併同步處理期間執行商務邏輯](merge/execute-business-logic-during-merge-synchronization.md)。  
  
## <a name="see-also"></a>另請參閱  
 [偵測及解決合併式複寫衝突](merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
