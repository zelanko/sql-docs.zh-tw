---
title: "不使用快照集初始化交易式訂閱 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactional replication, initializing
- replication [SQL Server], initializing
- initializing subscriptions [SQL Server replication], without snapshots
ms.assetid: 75c8c1f8-60bc-44a8-944b-d18d1f6bda11
caps.latest.revision: "37"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 471ff7f62145dd3e6593ab449545f5ddb49612eb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="initialize-a-transactional-subscription-without-a-snapshot"></a>不使用快照集初始化交易式訂閱
  依預設，會使用快照集來初始化交易式發行集的訂閱，此快照集由「快照集代理程式」產生並由「散發者代理程式」套用。 在某些狀況下，例如那些牽涉到大型初始資料集的狀況，最好使用其他方法初始化訂閱。 其他初始化「訂閱者」的方法包括：  
  
-   指定一個備份。 在「訂閱者」上還原備份，「散發代理程式」隨後會複製所有需要的複寫中繼資料與系統程序。 用備份進行初始化是將資料傳遞到「訂閱者」的最快方法且相當便利，因為如果最新的備份發生在為「使用備份進行初始化」啟用發行集之後，便可使用。  
  
-   透過其他機制將初始資料集複製到「訂閱者」，例如附加資料庫。 您必須確定「訂閱者」端的資料和結構描述正確，然後「散發代理程式」會複製需要的所有中繼資料和系統程序。  
  
## <a name="initializing-a-subscription-with-a-backup"></a>使用備份初始化訂閱  
 備份包含整個資料庫；因此當訂閱資料庫被初始化後，每個資料庫都包含發行集資料庫的完整副本：  
  
-   備份包含未指定為發行集之發行項的資料表。  
  
-   即使資料列或資料行篩選已在資料表中加以指定，此備份仍會包含所有資料。  
  
 在還原備份之後，管理員或應用程式有責任移除所有不想要的物件或資料。 在後續同步處理中，只有當資料變更套用至指定為發行項的資料表，且這些變更滿足您指定的所有篩選條件時，才會複寫資料變更。  
  
> [!NOTE]  
>  還原備份時，如果您想讓「訂閱者」自動進行同步處理，則必須確定備份來自「發行者」。 備份中的記錄序號 (LSN) 值 (用於設定啟動同步處理的位置) 對「發行者」是特定的。  
  
 **若要使用備份初始化訂閱**  
  
 若要使用備份初始化訂閱，在建立發行集時必須先啟用此選項，然後在建立訂閱時指定一些選項的值。 發行集可以透過「新增發行集精靈」或以程式設計方式進行啟用。 但是，訂閱選項所需的值只能以程式設計方式指定。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]：[為交易式發行集啟用使用備份的初始化 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/enable-initialization-with-backup-for-transactional-publications.md)  
  
-   複寫 Transact-SQL 程式設計：[從備份初始化交易式訂閱 &#40;複寫 Transact-SQL 程式設計&#41;](../../relational-databases/replication/initialize-a-transactional-subscription-from-a-backup.md)  
  
> [!NOTE]  
>  如果訂閱未使用快照集初始化，在發行者端執行 SQL Server 服務的帳戶必須具有散發者端快照集資料夾的寫入權限。 如需權限的資訊，請參閱＜ [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)＞。  
  
### <a name="ensuring-the-suitability-of-a-backup"></a>確定備份的適合性  
 如果備份後發生的所有交易均儲存在「散發者」端，則備份適用於初始化「訂閱者」。 如果備份不適合，則複寫會顯示一條錯誤訊息。  
  
 若要幫助確定備份適合使用，請遵循下列指導方針：  
  
-   使用可用的最新備份，如果最新備份早於最長散發保留期限，則在嘗試使用備份來初始化訂閱前建立一個新備份。 如需保留期限的詳細資訊，請參閱＜ [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)＞。  
  
-   依預設，散發清除作業會從散發資料庫中清除 72 小時前的交易。 清除是根據為發行集設定的保留期限來進行的。 與較舊的備份進行同步處理時，請考慮在您要還原備份之前暫時停用作業，並在訂閱成功建立後要重新啟用它。 這可防止交易從可能需要從備份成功進行同步處理的散發資料庫中移除。 如需執行清除作業的資訊，請參閱[執行複寫維護作業 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md)。  
  
 在某些情況下，您必須在設定使用備份進行了初始化的訂閱後，在還原的「訂閱者」資料庫中手動執行自訂。 一般而言，如果定義「發行集」的方式為「訂閱者」資料庫內容應不同於「發行者」資料庫內容，則要求在還原的「訂閱者」資料庫端進行手動修改。  
  
-   如果將還原資料庫中的索引檢視做為記錄式索引檢視發行項來發行，則必須將它們轉換成資料表。  
  
-   還原資料庫中的訂閱時間戳記資料行必須轉換為 **binary(8)** 資料行：將包含時間戳記資料行之資料表的內容複製到含相符結構描述的新資料表 (除非含有的是 **binary(8)** 資料行而非時間戳記資料行)，拖拽原始資料表，並將新資料表重新命名為原始資料表的名稱。  
  
## <a name="initializing-a-subscription-with-an-alternative-method"></a>使用替代方法初始化訂閱  
 使用可讓您將發行集資料庫結構描述與資料複製到「訂閱者」的任何方法，均有可能初始化訂閱，例如 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。 當您使用替代方法來初始化「訂閱者」時，複寫支援物件會複製到「訂閱者」。  
  
 與使用備份進行初始化不同，您或您的應用程式必須確定資料與結構描述在您新增訂閱時已正確進行了同步處理。 例如，若在複製資料和結構描述到訂閱者的時間，與加入訂閱的時間之間，發行者端有活動，此活動所導致的變更可能不會複寫到訂閱者。  
  
 若要使用替代方法初始化訂閱，請參閱＜ [Initialize a Subscription Manually](../../relational-databases/replication/initialize-a-subscription-manually.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [初始化訂閱](../../relational-databases/replication/initialize-a-subscription.md)  
  
  
