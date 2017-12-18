---
title: "變更資料擷取和其他 SQL Server 功能 | Microsoft Docs"
ms.custom: 
ms.date: 05/03/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: track-changes
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: change data capture [SQL Server], other SQL Server features and
ms.assetid: 7dfcb362-1904-4578-8274-da16681a960e
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 016d7eb7afb4b95c6a6635d24235d85025ccc4e2
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="change-data-capture-and-other-sql-server-features"></a>異動資料擷取和其他 SQL Server 功能
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] 本主題描述下列功能如何與異動資料擷取互動：  
  
-   [Change tracking](#ChangeTracking)  
  
-   [資料庫鏡像](#DatabaseMirroring)  
  
-   [異動複寫](#TransReplication)  
  
-   [還原或附加啟用變更資料擷取的資料庫](#RestoreOrAttach)  
  
##  <a name="ChangeTracking"></a> Change Tracking  
 您可以在同一個資料庫上啟用變更資料擷取和 [變更追蹤](../../relational-databases/track-changes/about-change-tracking-sql-server.md) 。 不需要進行任何特殊考量。 如需詳細資訊，請參閱[使用變更追蹤 &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-tracking-sql-server.md)。  
  
##  <a name="DatabaseMirroring"></a> 資料庫鏡像  
 啟用變更資料擷取的資料庫可以進行鏡像。 若要確保擷取和清除會在容錯移轉之後自動進行，請遵循下列步驟：  
  
1.  請確定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 是在新的主體伺服器執行個體上執行。  
  
2.  在新的主體資料庫上建立擷取作業和清除作業 (之前的鏡像資料庫)。 若要建立這些作業，請使用 [sp_cdc_add_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md) 預存程序。  
  
 若要檢視清除或擷取作業的目前組態，請在新的主體伺服器執行個體上使用 [sys.sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md) 預存程序。 對於指定的資料庫而言，擷取作業會命名為 cdc.*database_name*_capture，而清除作業會命名為 cdc.*database_name*_cleanup，其中 *database_name* 是資料庫的名稱。  
  
 若要變更作業的組態，請使用 [sys.sp_cdc_change_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md) 預存程序。  
  
 如需資料庫鏡像的相關資訊，請參閱[資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)。  
  
##  <a name="TransReplication"></a> Transactional Replication  
 雖然變更資料擷取和異動複寫可以同時存在同一個資料庫中，但是同時啟用這兩項功能時，系統會以不同的方式處理變更資料表的擴展。 變更資料擷取和異動複寫一定會使用相同的程序 [sp_replcmds](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)，從交易記錄中讀取變更。 單獨啟用變更資料擷取時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業就會呼叫 **sp_replcmds**。 在同一個資料庫上同時啟用這兩項功能時，記錄讀取器代理程式就會呼叫 **sp_replcmds**。 這個代理程式會同時擴展變更資料表和散發資料庫資料表。 如需詳細資訊，請參閱 [Replication Log Reader Agent](../../relational-databases/replication/agents/replication-log-reader-agent.md)。  
  
 假設您在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫上啟用了變更資料擷取，而且有兩份資料表啟用了擷取。 為了擴展變更資料表，擷取作業會呼叫 **sp_replcmds**。 資料庫啟用了異動複寫，而且建立了發行集。 此時，會針對資料庫建立記錄讀取器代理程式，並且刪除擷取作業。 記錄讀取器代理程式會繼續掃描記錄，從變更資料表所認可的最後一個記錄序號開始。 如此可確保變更資料表中的資料保持一致。 如果這個資料庫停用了異動複寫，系統就會移除記錄讀取器代理程式並且重新建立擷取作業。  
  
> [!NOTE]  
>  當記錄讀取器代理程式同時用於變更資料擷取和異動複寫時，複寫的變更會先寫入散發資料庫。 然後，擷取的變更才會寫入變更資料表。 這兩項作業會一起認可。 如果寫入散發資料庫時發生延遲，系統會建立對應的延遲，然後變更才會出現在變更資料表中。  
  
 啟用變更資料擷取時，異動複寫的 **proc exec** 選項無法使用。  
  
##  <a name="RestoreOrAttach"></a> 還原或附加啟用變更資料擷取的資料庫  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用下列邏輯來判斷在還原或附加資料庫之後，變更資料擷取是否會維持啟用狀態：  
  
-   如果資料庫還原至具有相同資料庫名稱的相同伺服器，變更資料擷取就會維持啟用狀態。  
  
-   如果資料庫還原至其他伺服器，預設會停用變更資料擷取並且刪除所有相關的中繼資料。  
  
     若要保留變更資料擷取，請在還原資料庫時使用 **KEEP_CDC** 選項。 如需有關這個選項的詳細資訊，請參閱＜ [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)＞。  
  
-   如果資料庫卸離並附加至相同伺服器或其他伺服器，變更資料擷取就會維持啟用狀態。  
  
-   如果您使用 **KEEP_CDC** 選項，將資料庫附加或還原至 Enterprise 以外的任何版本，此作業就會遭封鎖，因為變更資料擷取需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise。 此時會顯示錯誤訊息 934：  
  
     `SQL Server cannot load database '%.*ls' because Change Data Capture is enabled. The currently installed edition of SQL Server does not support Change Data Capture. Either restore database without KEEP_CDC option, or upgrade the instance to one that supports Change Data Capture.`  
  
 您可以使用 [sys.sp_cdc_disable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md) ，從還原或附加的資料庫中移除變更資料擷取。  
  
## <a name="change-data-capture-and-always-on"></a>變更資料擷取和 AlwaysON  
 當您使用 AlwaysON 時，應該在次要複寫上完成變更列舉以減少主要複寫的磁碟負載。  
  
## <a name="see-also"></a>另請參閱  
 [管理和監視異動資料擷取 &#40;SQL Server&#41;](../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
