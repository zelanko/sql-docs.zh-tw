---
title: "以程式設計方式監視複寫 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- sp_replmonitorhelppublisher
- sp_replmonitorhelpmergesessiondetail
- monitoring performance [SQL Server replication], publication status
- sp_replmonitorhelpmergesession
- sp_replmonitorhelppublicationthresholds
- monitoring performance [SQL Server replication], subscription status
- monitoring performance [SQL Server replication], Transact-SQL programming
- sp_replmonitorsubscriptionpendingcmds
- sp_replmonitorchangepublicationthreshold
- transactional replication, monitoring
- sp_replmonitorhelppublication
- sp_replmonitorhelpsubscription
- monitoring performance [SQL Server replication], thresholds and warnings
- merge replication monitoring [SQL Server replication]
- snapshot replication [SQL Server], monitoring
ms.assetid: e8bf8850-8da5-4a4f-a399-64232b4e476d
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b05b9c5af4ff9ed8626773fc6714c2c05f1605b2
ms.lasthandoff: 04/11/2017

---
# <a name="programmatically-monitor-replication"></a>以程式設計方式監視複寫
  「複寫監視器」是一個允許您監視複寫拓撲之全面健全狀況的圖形化工具。 您可以使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 複寫預存程序或 Replication Management Objects (RMO)，以程式設計的方式存取相同的監視資料。 這些物件可用來設計下列工作：  
  
-   監視「發行者」、發行集和訂閱的狀態。  
  
-   在一個或多個「訂閱者」端監視「合併代理程式」的工作階段。  
  
-   監視在一個或多個「訂閱者」端等候套用的交易式命令。  
  
-   定義臨界值標準，以決定發行集何時需要介入。  
  
-   監視追蹤 Token 的狀態。  
  
 **本主題內容：**  
  
 [Transact-SQL](#Tsql)  
  
 [Replication Management Objects (RMO)](#RMO)  
  
##  <a name="Tsql"></a> Transact-SQL  
  
#### <a name="to-monitor-publishers-publications-and-subscriptions-from-the-distributor"></a>若要從散發者監視發行者、發行集和訂閱  
  
1.  在散發資料庫的「散發者」端，執行 [sp_replmonitorhelppublisher](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublisher-transact-sql.md)。 這會為所有使用此「散發者」的「發行者」傳回監視資訊。 若要將結果集限制為單一「發行者」，請指定 **@publisher**。  
  
2.  在散發資料庫的「散發者」端，執行 [sp_replmonitorhelppublication](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublication-transact-sql.md)。 這會為所有使用此「散發者」的發行集傳回監視資訊。 若要將結果集限制為單一「發行者」、發行集或已發行資料庫，請分別指定 **@publisher**、 **@publication**或 **@publisher_db**。  
  
3.  在散發資料庫的「散發者」端，執行 [sp_replmonitorhelpsubscription](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpsubscription-transact-sql.md)。 這會為所有使用此「散發者」的訂閱傳回監視資訊。 若要將結果集限制為屬於單一「發行者」、發行集或已發行資料庫的訂閱，請分別指定 **@publisher**、 **@publication**或 **@publisher_db**。  
  
#### <a name="to-monitor-transactional-commands-waiting-to-be-applied-at-the-subscriber"></a>若要監視在訂閱者端等候套用的交易式命令  
  
1.  在散發資料庫的「散發者」端，執行 [sp_replmonitorsubscriptionpendingcmds](../../../relational-databases/system-stored-procedures/sp-replmonitorsubscriptionpendingcmds-transact-sql.md)。 這會為所有使用此「散發者」的訂閱傳回所有暫止命令的監視資訊。 若要將結果集限制為屬於單一「發行者」、「訂閱者」、發行集或已發行資料庫之訂閱的暫止命令，請分別指定 **@publisher**、 **@subscriber**、 **@publication**或 **@publisher_db**。  
  
#### <a name="to-monitor-merge-changes-waiting-to-be-uploaded-or-downloaded"></a>若要監視等候上傳或下載的合併變更  
  
1.  在發行集資料庫的「發行者」端，執行 [sp_showpendingchanges](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md)。 這會傳回結果集，顯示正等候複寫至「訂閱者」之變更的相關資訊。 若要將結果集限制為屬於單一發行集或發行項的變更，請分別指定 **@publication** 或 **@article**。  
  
2.  在訂閱資料庫的「訂閱者」端，執行 [sp_showpendingchanges](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md)。 這會傳回結果集，顯示正等候複寫至「發行者」之變更的相關資訊。 若要將結果集限制為屬於單一發行集或發行項的變更，請分別指定 **@publication** 或 **@article**。  
  
#### <a name="to-monitor-merge-agent-sessions"></a>若要監視合併代理程式的工作階段  
  
1.  在散發資料庫的「散發者」端，執行 [sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md)。 這會針對所有使用此「散發者」的訂閱，傳回有關「合併代理程式」工作階段的監視資訊，包括 **Session_id**。 您也可以藉由查詢 **MSmerge_sessions** 系統資料表來取得 [Session_id](../../../relational-databases/system-tables/msmerge-sessions-transact-sql.md) 。  
  
2.  在散發資料庫的「散發者」端，執行 [sp_replmonitorhelpmergesessiondetail](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md)。 針對 **Session_id** 指定步驟 1 的 **@session_id**。 這會顯示有關工作階段的詳細監視資訊。  
  
3.  針對每個感興趣的工作階段重複步驟 2。  
  
#### <a name="to-monitor-merge-agent-sessions-for-pull-subscriptions-from-the-subscriber"></a>若要從訂閱者監視提取訂閱的合併代理程式工作階段  
  
1.  在訂閱資料庫的「訂閱者」端，執行 [sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md)。 針對給定的訂閱指定 **@publisher**、 **@publication**，及 **@publisher_db**。 這會傳回此訂閱最後五個「合併代理程式」工作階段的監視資訊。 請注意結果集中感興趣之工作階段的 **Session_id** 值。  
  
2.  在訂閱資料庫的「訂閱者」端，執行 [sp_replmonitorhelpmergesessiondetail](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md)。 針對 **Session_id** 指定步驟 1 的 **@session_id**。 這會顯示有關工作階段的詳細監視資訊。  
  
3.  針對每個感興趣的工作階段重複步驟 2。  
  
#### <a name="to-view-and-modify-the-monitor-threshold-metrics-for-a-publication"></a>若要檢視和修改發行集的監視臨界值標準  
  
1.  在散發資料庫的「散發者」端，執行 [sp_replmonitorhelppublicationthresholds](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublicationthresholds-transact-sql.md)。 這會傳回為所有使用此「散發者」的發行集所設定的監視臨界值。 若要將結果集限制為監視屬於單一「發行者」或已發行資料庫之發行集的臨界值或監視單一發行集的臨界值，請分別指定 **@publisher**、 **@publisher_db**或 **@publication**。 請注意必須變更之任何臨界值的 **Metric_id** 值。 如需相關資訊，請參閱 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。  
  
2.  在散發資料庫的「散發者」端，執行 [sp_replmonitorchangepublicationthreshold](../../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md)。 視需要指定下列項目：  
  
    -   針對 **Metric_id** 指定在步驟 1 中取得的 **@metric_id**。  
  
    -   針對 **@value**。  
  
    -   針對 **@shouldalert** ，指定 **@shouldalert** 的值以在達到此臨界值時記錄警示，或者如果不需要警示，則指定 **0** 的值。  
  
    -   針對 **@shouldalert** ，指定 **@mode** 的值以啟用監視臨界值標準；或指定 **2** 的值加以停用。  
  
##  <a name="RMO"></a> Replication Management Objects (RMO)  
  
#### <a name="to-monitor-a-subscription-to-a-merge-publication-at-the-subscriber"></a>若要監視訂閱者端合併式發行集的訂閱  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與訂閱者的連線。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor> 類別的執行個體，並設定訂閱的 <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publisher%2A>、<xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publication%2A>、<xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.PublisherDB%2A>、<xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.SubscriberDB%2A> 屬性，以及將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為在步驟 1 中建立的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>。  
  
3.  呼叫下列其中一個方法，以傳回此訂閱的「合併代理程式」工作階段的相關資訊：  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A> - 傳回 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> 物件的陣列，內含最多達最後五個「合併代理程式」工作階段的資訊。 請注意感興趣之任何工作階段的 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> 值。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A> - 傳回 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> 物件的陣列，內含在經過的小時數期間 (如 *hours* 參數所指定) 所發生的「合併代理程式」工作階段的資訊 (最多達最後五個工作階段)。 請注意感興趣之任何工作階段的 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> 值。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummary%2A> - 傳回 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> 物件，內含最後一個「合併代理程式」工作階段的資訊。 請注意此工作階段的 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> 值。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummaryDataSet%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含最多達最後五個「合併代理程式」工作階段的資訊，而且一列顯示一個工作階段的資訊。 請記下感興趣之任何工作階段的 **Session_id** 資料行值。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummaryDataRow%2A> - 傳回 <xref:System.Data.Data資料列> 物件，內含最後一個「合併代理程式」工作階段的資訊。 請記下此工作階段的 **Session_id** 資料行值。  
  
4.  (選擇性) 呼叫 <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A> 來重新整理傳遞為 *mss*之 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> 物件的資料，或呼叫 <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A> 來重新整理傳遞為 *drRefresh* 之 <xref:System.Data.Data資料列> 物件中的資料。  
  
5.  使用步驟 3 中取得的工作階段識別碼，呼叫下列其中一個方法來傳回有關特定工作階段詳細資料的資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetails%2A> - 傳回所提供 *SessionId* 之 <xref:Microsoft.SqlServer.Replication.MergeSessionDetail> 物件的陣列。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetailsDataSet%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含所指定 *SessionId* 的資訊。  
  
#### <a name="to-monitor-replication-properties-for-all-publications-at-a-distributor"></a>若要監視在散發者端所有發行集的複寫屬性  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與散發者的連線。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.ReplicationMonitor> 類別的執行個體。  
  
3.  將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為在步驟 1 中建立的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。  
  
5.  執行下列其中一或多個方法，以針對使用此散發者的所有發行者傳回複寫資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumDistributionAgents%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含這個散發者端之所有散發代理程式的資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumErrorRecords%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含散發者端所儲存錯誤的資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumLogReaderAgents%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含散發者端之所有「記錄讀取器代理程式」的資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMergeAgents%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含散發者端之所有「合併代理程式」的資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMiscellaneousAgents%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含散發者端之所有其他複寫代理程式的資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含這個散發者端之所有發行者的資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers2%2A> - 傳回 <xref:System.Data.DataSet> 物件，以傳回使用這個散發者的發行者。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgents%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含散發者端之所有「佇列讀取器代理程式」的資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessionDetails%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含所指定「佇列讀取器代理程式」和工作階段的詳細資料。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessions%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含所指定「佇列讀取器代理程式」的工作階段資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumSnapshotAgents%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含散發者端之所有「快照集代理程式」的資訊。  
  
#### <a name="to-monitor-publication-properties-for-a-specific-publisher-at-the-distributor"></a>若要監視在散發者端特定發行者的發行集屬性  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與散發者的連線。  
  
2.  以下列其中一種方法取得 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 物件。  
  
    -   建立 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 類別的執行個體。 設定發行者的 <xref:Microsoft.SqlServer.Replication.PublisherMonitor.Name%2A> 屬性，並將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為在步驟 1 中建立的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>。 呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回 **false**，則表示「發行者」名稱定義不正確，或者該發行集不存在。  
  
    -   從藉由現有 <xref:Microsoft.SqlServer.Replication.ReplicationMonitor> 物件的 <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.PublisherMonitors%2A> 屬性進行存取的 <xref:Microsoft.SqlServer.Replication.PublisherMonitorCollection>。  
  
3.  執行下列其中一或多個方法，針對屬於此「發行者」的所有發行集傳回複寫資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessionDetails%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含所指定「散發代理程式」和工作階段的詳細資料。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessions%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含所指定「散發代理程式」的工作階段資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumErrorRecords%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含所指定錯誤的錯誤記錄資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessionDetails%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含所指定「記錄讀取器代理程式」和工作階段的詳細資料。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessions%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含所指定「記錄讀取器代理程式」的工作階段資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含所指定「合併代理程式」和工作階段的詳細資料。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails2%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含所指定「合併代理程式」和工作階段的其他詳細資料。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含所指定「合併代理程式」的工作階段資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions2%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含所指定「合併代理程式」的其他工作階段資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含這個散發者端之所有發行集的資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications2%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含這個散發者端之所有發行集的其他資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessionDetails%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含所指定「快照集代理程式」和工作階段的詳細資料。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessions%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含所指定「快照集代理程式」的工作階段資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSubscriptions%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含這個散發者端之所有發行集訂閱的資訊。  
  
#### <a name="to-monitor-properties-for-a-specific-publication-at-the-distributor"></a>若要監視散發者端特定發行集的屬性  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與散發者的連線。  
  
2.  以下列其中一種方法取得 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 物件。  
  
    -   建立 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 類別的執行個體。 設定發行集的 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>、<xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>、<xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A> 和 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> 屬性，並將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為在步驟 1 中建立的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>。 呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回 **false**，則表示發行集屬性定義不正確，或者該發行集不存在。  
  
    -   從藉由現有 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 物件的 <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> 屬性進行存取的 <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection>。  
  
3.  執行下列其中一或多個方法，傳回有關此發行集的詳細資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumErrorRecords%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含所指定錯誤的錯誤記錄。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumLogReaderAgent%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含這個發行集之「記錄讀取器代理程式」的資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含針對這個發行集所設定之監視警告閾值的資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumQueueReaderAgent%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含這個發行集所使用之「佇列讀取器代理程式」的資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSnapshotAgent%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含這個發行集之「快照集代理程式」的資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.EnumSubscriptions%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含這個發行集之訂閱的資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSubscriptions2%2A> - 根據所提供的 <xref:Microsoft.SqlServer.Replication.SubscriptionResultOption>，傳回 <xref:System.Data.DataSet> 物件，內含這個發行集之訂閱的其他資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokenHistory%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含所指定追蹤 Token 的延遲資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A> - 傳回 <xref:System.Data.DataSet> 物件，內含插入至這個發行集之所有追蹤 Token 的資訊。  
  
#### <a name="to-monitor-transactional-commands-that-are-waiting-to-be-applied-at-the-subscriber"></a>若要監視在訂閱者端等候套用的交易式命令  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與散發者的連線。  
  
2.  以下列其中一種方法取得 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 物件。  
  
    -   建立 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 類別的執行個體。 設定發行集的 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>、<xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>、<xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A> 和 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> 屬性，並將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為在步驟 1 中建立的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>。 呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回 **false**，則表示發行集屬性定義不正確，或者該發行集不存在。  
  
    -   從藉由現有 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 物件的 <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> 屬性進行存取的 <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection>。  
  
3.  執行 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.TransPendingCommandInfo%2A> 方法，以傳回 <xref:Microsoft.SqlServer.Replication.PendingCommandInfo> 物件。  
  
4.  使用此 <xref:Microsoft.SqlServer.Replication.PendingCommandInfo> 物件的屬性判斷暫止命令的估計數，以及完成傳遞這些命令所需的時間長度。  
  
#### <a name="to-set-the-monitor-warning-thresholds-for-a-publication"></a>若要設定發行集的監視器警告臨界值  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與散發者的連線。  
  
2.  以下列其中一種方法取得 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 物件。  
  
    -   建立 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 類別的執行個體。 設定發行集的 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>、<xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>、<xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A> 和 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> 屬性，並將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為在步驟 1 中建立的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>。 呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回 **false**，則表示發行集屬性定義不正確，或者該發行集不存在。  
  
    -   從藉由現有 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 物件的 <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> 屬性進行存取的 <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection>。  
  
3.  執行 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A> 方法。 請記下 <xref:Microsoft.SqlServer.Replication.MonitorThreshold> 物件之所傳回 <xref:System.Collections.ArrayList> 中的目前閾值設定。  
  
4.  執行 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.ChangeMonitorThreshold%2A> 方法。 傳遞下列參數：  
  
    -   *metricID* - <xref:System.Int32> 值，代表來自下列資料表的監視閾值度量：  
  
        |Value|說明|  
        |-----------|-----------------|  
        |@shouldalert|**expiration** - 監視交易式發行集的訂閱是否即將到期。|  
        |2|**latency** - 監視交易式發行集的訂閱效能。|  
        |4|**mergeexpiration** - 監視合併式發行集的訂閱是否即將到期。|  
        |5|**mergeslowrunduration** - 監視透過低頻寬 (撥號) 連接進行合併同步處理的持續時間。|  
        |6|**mergefastrunduration** - 監視透過高頻寬 (LAN) 連接進行合併同步處理的持續時間。|  
        |7|**mergefastrunspeed** - 監視透過高頻寬 (LAN) 連接進行合併同步處理的同步處理速率。|  
        |8|**mergeslowrunspeed** - 監視透過低頻寬 (撥號) 連接進行合併同步處理的同步處理速率。|  
  
    -   *enable* - <xref:System.Boolean> 值，表示是否已針對發行集啟用度量。  
  
    -   *thresholdValue* - 設定臨界值的整數值。  
  
    -   *shouldAlert* - 代表此臨界值是否應產生警示的整數。  
  
  
