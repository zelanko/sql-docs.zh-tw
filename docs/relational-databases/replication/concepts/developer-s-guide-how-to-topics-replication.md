---
title: "開發人員指南：使用說明主題 (複寫) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: c6c15ae6-da52-4638-93d3-61c7242e8a0b
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 288ed137e701d6cfb416d12b6ff2176c59ec0278
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="developer39s-guide-how-to-topics-replication"></a>開發人員指南：使用說明主題 (複寫)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  本主題提供有關如何以程式設計方式執行複寫相關工作的資訊連結。  
  
## <a name="securing-a-replication-topology"></a>保護複寫拓撲的安全性  
  
-   [檢視及修改複寫安全性設定](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
-   [管理發行集存取清單中的登入](../../../relational-databases/replication/security/manage-logins-in-the-publication-access-list.md)  
  
## <a name="configuring-modifying-and-disabling-publishing-and-distribution-replication"></a>設定、修改及停用發行與散發 (複寫)  
  
-   [設定發行和散發](../../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
-   [檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
-   [停用發行和散發](../../../relational-databases/replication/disable-publishing-and-distribution.md)  
  
## <a name="creating-modifying-and-deleting-publications-and-articles"></a>建立、修改及刪除發行集和發行項  
  
-   [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)  
  
-   [檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
-   [檢視和修改發行項屬性](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
-   [刪除發行集](../../../relational-databases/replication/publish/delete-a-publication.md)  
  
-   [刪除發行項](../../../relational-databases/replication/publish/delete-an-article.md)  
  
-   [從 Oracle 資料庫建立發行集](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)  
  
-   [設定訂閱的到期時間](../../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md)  
  
-   [指定結構描述選項](../../../relational-databases/replication/publish/specify-schema-options.md)  
  
-   [複寫結構描述變更](../../../relational-databases/replication/publish/replicate-schema-changes.md)  
  
-   [管理識別資料行](../../../relational-databases/replication/publish/manage-identity-columns.md)  
  
-   [設定合併式發行集的相容性層級](../../../relational-databases/replication/publish/set-the-compatibility-level-for-merge-publications.md)  
  
### <a name="snapshot-options"></a>快照集選項  
  
-   [設定快照集屬性 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
-   [透過 FTP 傳遞快照集](../../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)  
  
### <a name="filtering-data"></a>篩選資料  
  
-   [定義及修改資料行篩選](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)  
  
-   [定義及修改靜態資料列篩選](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)  
  
-   [針對合併發行項定義及修改參數化資料列篩選](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
-   [最佳化參數化資料列篩選](../../../relational-databases/replication/publish/optimize-parameterized-row-filters.md)  
  
-   [定義和修改合併發行項之間的聯結篩選](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)  
  
### <a name="transactional-replication-options"></a>異動複寫選項  
  
-   [設定對交易式發行項之資料變更的傳播方法](../../../relational-databases/replication/publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md)  
  
-   [啟用交易式發行集的更新訂閱](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
### <a name="merge-replication-options"></a>合併式複寫選項  
  
-   [定義合併資料表發行項之間的邏輯記錄關聯性](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)  
  
-   [指定合併資料表發行項的處理順序 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/publish/specify-the-processing-order-of-merge-table-articles.md)  
  
-   [將合併資料表發行項指定為僅限下載](../../../relational-databases/replication/publish/specify-that-a-merge-table-article-is-download-only.md)  
  
-   [指定不應該為合併發行項追蹤刪除 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/publish/specify-that-deletes-should-not-be-tracked-for-merge-articles.md)  
  
-   [指定合併發行項的衝突追蹤與解決層級](../../../relational-databases/replication/publish/specify-the-conflict-tracking-and-resolution-level-for-merge-articles.md)  
  
-   [指定合併發行項解析程式](../../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
-   [指定合併發行項的互動式衝突解決方法](../../../relational-databases/replication/publish/specify-interactive-conflict-resolution-for-merge-articles.md)  
  
## <a name="creating-modifying-and-deleting-subscriptions"></a>建立、修改與刪除訂閱  
  
-   [建立提取訂閱](../../../relational-databases/replication/create-a-pull-subscription.md)  
  
-   [檢視及修改提取訂閱屬性](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)  
  
-   [刪除提取訂閱](../../../relational-databases/replication/delete-a-pull-subscription.md)  
  
-   [建立發送訂閱](../../../relational-databases/replication/create-a-push-subscription.md)  
  
-   [檢視及修改發送訂閱屬性](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md)  
  
-   [刪除發送訂閱](../../../relational-databases/replication/delete-a-push-subscription.md)  
  
-   [指定同步處理排程](../../../relational-databases/replication/specify-synchronization-schedules.md)  
  
-   [建立交易式發行集的可更新訂閱](../../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md)
  
-   [為非 SQL Server 訂閱者建立訂閱](../../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)  
  
## <a name="synchronizing-subscriptions"></a>同步處理訂閱  
  
-   [建立和套用初始快照集](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)  
  
-   [使用參數化篩選建立合併式發行集的快照集](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [從備份初始化交易式訂閱 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/initialize-a-transactional-subscription-from-a-backup.md)  
  
-   [手動初始化訂閱](../../../relational-databases/replication/initialize-a-subscription-manually.md)  
  
-   [同步處理提取訂閱](../../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
-   [同步處理發送訂閱](../../../relational-databases/replication/synchronize-a-push-subscription.md)  
  
-   [重新初始化訂閱](../../../relational-databases/replication/reinitialize-a-subscription.md)  
  
-   [在同步處理期間執行指令碼 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)  
  
-   [為合併發行項實作商務邏輯處理常式](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
-   [偵錯商務邏輯處理常式 &#40;複寫程式設計&#41;](../../../relational-databases/replication/debug-a-business-logic-handler-replication-programming.md)  
  
-   [在同步處理期間控制觸發程序和條件約束的行為 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md)  
  
-   [針對合併發行項實作自訂衝突解析程式](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## <a name="administering-a-replication-topology"></a>管理複寫拓撲  
  
-   [處理複寫代理程式設定檔](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
-   [驗證訂閱者端的資料](../../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
-   [使用參數化篩選管理合併式發行集的資料分割](../../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [將資料大量載入合併式發行集中的資料表 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/bulk-load-data-into-tables-in-a-merge-publication.md)  
  
-   [清除合併中繼資料 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/administration/clean-up-merge-metadata-replication-transact-sql-programming.md)  
  
-   [執行合併發行項的虛擬更新 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/administration/perform-a-dummy-update-for-a-merge-article-replication-transact-sql-programming.md)  
  
-   [在散發資料庫中檢視複寫的命令和其他資訊 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md)  
  
-   [為異動複寫啟用協調備份 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md)  
  
-   [管理點對點拓撲 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)  
  
-   [停止複寫拓撲 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)  
  
-   [設定 Oracle 發行者的交易集作業 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)  
  
-   [升級複寫指令碼 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)  
  
## <a name="monitoring-a-replication-topology"></a>監視複寫拓撲  
  
-   [允許非管理員使用複寫監視器](../../../relational-databases/replication/monitor/allow-non-administrators-to-use-replication-monitor.md)  
  
-   [以程式設計方式監視複寫](../../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
-   [在散發資料庫中檢視複寫的命令和其他資訊 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md)  
  
-   [檢視合併式發行集的衝突資訊 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md)  
  
-   [針對異動複寫測量延遲及驗證連線](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
