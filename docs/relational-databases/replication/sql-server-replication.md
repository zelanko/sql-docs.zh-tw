---
title: SQL Server 複寫 | Microsoft Docs
description: 了解 SQL Server 中的複寫，此為在資料庫之間複製和散發資料及資料庫物件，以及在資料庫之間進行同步處理的技術。
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], about
- replication [SQL Server]
ms.assetid: 3a5f4592-3c61-4b4d-9ceb-39716aeeba41
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 898053b0114eb398c5b9650fa162779edb6af818
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479659"
---
# <a name="sql-server-replication"></a>SQL Server 複寫
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  複寫是指，將資料和資料庫物件從某個資料庫複製和散發到另一個資料庫，然後在兩個資料庫之間進行同步處理，以維護一致性的一組技術。 使用複寫，以透過區域網路、廣域網路、撥號連接、無線連接及網際網路，將資料散發到不同的位置，以及散發到遠端或行動使用者。  
  
 異動複寫一般用於需要高輸送量的伺服器對伺服器案例中，其中包括：提升延展性和可用性、資料倉儲和報表、整合多個站台的資料、整合異質資料，以及卸載批次處理。 合併式複寫主要是為了可能具有資料衝突的行動應用程式或分散式伺服器應用程式而設計。 常見的案例包括：與行動使用者交換資料、消費者銷售點 (POS) 應用程式，以及多個站台的資料整合。 快照式複寫用於提供交易式和合併式複寫的初始資料集；它也可以用於適合將資料完全重新整理時。 使用這三種複寫， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了強大且彈性的系統，可同步處理您企業中的資料。 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 和 [!INCLUDE[win8](../../includes/win8-md.md)]支援複寫至 SQLCE 3.5 和 SQLCE 4.0。  


## <a name="whats-new"></a>新功能 
- SQL Server 2017 尚未在 SQL Server 複寫中導入重大的新功能。 
- SQL Server 2016 尚未在 SQL Server 複寫中導入重大的新功能。 

如需回溯相容性資訊，請參閱[複寫回溯相容性](replication-backward-compatibility.md) 


 ## <a name="replication-security"></a>複寫安全性
  
-   [檢視及修改複寫安全性設定](security/view-and-modify-replication-security-settings.md)  
-   [管理發行集存取清單中的登入](security/manage-logins-in-the-publication-access-list.md)  
  
## <a name="publishing-and-distribution"></a>發行和散發  
  
-   [設定發行和散發](configure-publishing-and-distribution.md)   
-   [檢視和修改發行集屬性](publish/view-and-modify-publication-properties.md)   
-   [停用發行和散發](disable-publishing-and-distribution.md)  
  
## <a name="publications-and-articles"></a>發行集和發行項 
  
-   [建立發行集](publish/create-a-publication.md)    
-   [定義發行項](publish/define-an-article.md)   
-   [檢視和修改發行集屬性](publish/view-and-modify-publication-properties.md)   
-   [檢視和修改發行項屬性](publish/view-and-modify-article-properties.md)    
-   [刪除發行集](publish/delete-a-publication.md)   
-   [刪除發行項](publish/delete-an-article.md)    
-   [從 Oracle 資料庫建立發行集](publish/create-a-publication-from-an-oracle-database.md)   
-   [設定訂閱的到期時間](publish/set-the-expiration-period-for-subscriptions.md)  
-   [指定結構描述選項](publish/specify-schema-options.md)  
-   [複寫結構描述變更](publish/replicate-schema-changes.md)    
-   [管理識別資料行](publish/manage-identity-columns.md)   
-   [設定合併式發行集的相容性層級](publish/set-the-compatibility-level-for-merge-publications.md)  
  
### <a name="snapshot-options"></a>快照集選項  
  
-   [設定快照集屬性](publish/configure-snapshot-properties-replication-transact-sql-programming.md)    
-   [透過 FTP 傳遞快照集](publish/deliver-a-snapshot-through-ftp.md) 
  
### <a name="filter-data"></a>篩選資料  
  
-   [定義及修改資料行篩選](publish/define-and-modify-a-column-filter.md)    
-   [定義及修改靜態資料列篩選](publish/define-and-modify-a-static-row-filter.md)    
-   [針對合併發行項定義及修改參數化資料列篩選](publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)    
-   [最佳化參數化資料列篩選](publish/optimize-parameterized-row-filters.md)    
-   [定義和修改合併發行項之間的聯結篩選](publish/define-and-modify-a-join-filter-between-merge-articles.md)  
  
### <a name="transactional-replication-options"></a>異動複寫選項  
  
-   [設定對交易式發行項之資料變更的傳播方法](publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md)    
-   [啟用交易式發行集的更新訂閱](publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
### <a name="merge-replication-options"></a>合併式複寫選項  
  
-   [定義合併資料表發行項之間的邏輯記錄關聯性](publish/define-a-logical-record-relationship-between-merge-table-articles.md)    
-   [指定合併式複寫屬性](merge/specify-merge-replication-properties.md)    
-   [指定合併發行項解析程式](publish/specify-a-merge-article-resolver.md)    

  
## <a name="manage-subscriptions"></a>管理訂閱  
  
-   [建立提取訂閱](create-a-pull-subscription.md)    
-   [檢視及修改提取訂閱屬性](view-and-modify-pull-subscription-properties.md)    
-   [刪除提取訂閱](delete-a-pull-subscription.md)    
-   [建立發送訂閱](create-a-push-subscription.md)   
-   [檢視及修改發送訂閱屬性](view-and-modify-push-subscription-properties.md)   
-   [刪除發送訂閱](delete-a-push-subscription.md)   
-   [指定同步處理排程](specify-synchronization-schedules.md)    
-   [建立交易式發行集的可更新訂閱](publish/create-an-updatable-subscription-to-a-transactional-publication.md)  
-   [為非 SQL Server 訂閱者建立訂閱](create-a-subscription-for-a-non-sql-server-subscriber.md)  
  
## <a name="synchronize-subscriptions"></a>同步處理訂閱  
  
-   [建立和套用初始快照集](create-and-apply-the-initial-snapshot.md)   
-   [使用參數化篩選建立合併式發行集的快照集](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)    
-   [從備份初始化交易式訂閱 &#40;複寫 Transact-SQL 程式設計&#41;](initialize-a-transactional-subscription-from-a-backup.md)    
-   [手動初始化訂閱](initialize-a-subscription-manually.md)    
-   [同步處理提取訂閱](synchronize-a-pull-subscription.md)    
-   [同步處理發送訂閱](synchronize-a-push-subscription.md)   
-   [重新初始化訂閱](reinitialize-a-subscription.md)    
-   [在同步處理期間執行指令碼 &#40;複寫 Transact-SQL 程式設計&#41;](execute-scripts-during-synchronization-replication-transact-sql-programming.md)    
-   [為合併發行項實作商務邏輯處理常式](implement-a-business-logic-handler-for-a-merge-article.md)  
-   [偵錯商務邏輯處理常式 &#40;複寫程式設計&#41;](debug-a-business-logic-handler-replication-programming.md)    
-   [在同步處理期間控制觸發程序和條件約束的行為 &#40;複寫 Transact-SQL 程式設計&#41;](control-behavior-of-triggers-and-constraints-in-synchronization.md)    
-   [為合併發行項實作自訂衝突解析程式](implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## <a name="administration"></a>系統管理 
  
-   [處理複寫代理程式設定檔](agents/work-with-replication-agent-profiles.md)   
-   [驗證訂閱者端的資料](validate-data-at-the-subscriber.md)    
-   [使用參數化篩選管理合併式發行集的資料分割](publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)    
-   [將資料大量載入合併式發行集中的資料表 &#40;複寫 Transact-SQL 程式設計&#41;](bulk-load-data-into-tables-in-a-merge-publication.md)    
-   [清除合併中繼資料 &#40;複寫 Transact-SQL 程式設計&#41;](administration/clean-up-merge-metadata-replication-transact-sql-programming.md)    
-   [執行合併發行項的虛擬更新 &#40;複寫 Transact-SQL 程式設計&#41;](administration/perform-a-dummy-update-for-a-merge-article-replication-transact-sql-programming.md)    
-   [在散發資料庫中檢視複寫的命令和其他資訊 &#40;複寫 Transact-SQL 程式設計&#41;](monitor/view-replicated-commands-and-information-in-distribution-database.md)    
-   [為異動複寫啟用協調備份 &#40;複寫 Transact-SQL 程式設計&#41;](administration/enable-coordinated-backups-for-transactional-replication.md)   
-   [管理點對點拓撲 &#40;複寫 Transact-SQL 程式設計&#41;](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)    
-   [停止複寫拓撲 &#40;複寫 Transact-SQL 程式設計&#41;](administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)    
-   [設定 Oracle 發行者的交易集作業 &#40;複寫 Transact-SQL 程式設計&#41;](administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
-   [升級複寫指令碼 &#40;複寫 Transact-SQL 程式設計&#41;](administration/upgrade-replication-scripts-replication-transact-sql-programming.md)  
  
## <a name="monitor"></a>監視
  
-   [允許非管理員使用複寫監視器](monitor/allow-non-administrators-to-use-replication-monitor.md)    
-   [以程式設計方式監視複寫](monitor/programmatically-monitor-replication.md)    
-   [在散發資料庫中檢視複寫的命令和其他資訊 &#40;複寫 Transact-SQL 程式設計&#41;](monitor/view-replicated-commands-and-information-in-distribution-database.md)    
-   [檢視合併式發行集的衝突資訊 &#40;複寫 Transact-SQL 程式設計&#41;](./view-and-resolve-data-conflicts-for-merge-publications.md) 
-   [針對異動複寫測量延遲及驗證連接](monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
