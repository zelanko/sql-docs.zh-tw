---
title: "以程式設計方式監視複寫 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "sp_replmonitorhelppublisher"
  - "sp_replmonitorhelpmergesessiondetail"
  - "monitoring performance [SQL Server replication], publication status"
  - "sp_replmonitorhelpmergesession"
  - "sp_replmonitorhelppublicationthresholds"
  - "monitoring performance [SQL Server replication], subscription status"
  - "monitoring performance [SQL Server replication], Transact-SQL programming"
  - "sp_replmonitorsubscriptionpendingcmds"
  - "sp_replmonitorchangepublicationthreshold"
  - "transactional replication, monitoring"
  - "sp_replmonitorhelppublication"
  - "sp_replmonitorhelpsubscription"
  - "monitoring performance [SQL Server replication], thresholds and warnings"
  - "merge replication monitoring [SQL Server replication]"
  - "快照式複寫 [SQL Server], 監視"
ms.assetid: e8bf8850-8da5-4a4f-a399-64232b4e476d
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# 以程式設計方式監視複寫
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
  
#### 若要從散發者監視發行者、發行集和訂閱  
  
1.  在散發資料庫的散發者端，執行 [sp_replmonitorhelppublisher](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublisher-transact-sql.md)。 這會為所有使用此「散發者」的「發行者」傳回監視資訊。 若要將結果集限制為單一「發行者」，請指定 **@publisher**。  
  
2.  在散發資料庫的散發者端，執行 [sp_replmonitorhelppublication](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublication-transact-sql.md)。 這會為所有使用此「散發者」的發行集傳回監視資訊。 若要限制結果集到單一 「 發行者 」、 發行集或已發行的資料庫，請指定 **@publisher**, ，**@publication**, ，或 **@publisher_db**, 分別。  
  
3.  在散發資料庫的散發者端，執行 [sp_replmonitorhelpsubscription](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpsubscription-transact-sql.md)。 這會為所有使用此「散發者」的訂閱傳回監視資訊。 若要限制結果集至訂閱屬於單一 「 發行者 」，發行集或發行的資料庫指定 **@publisher**, ，**@publication**, ，或 **@publisher_db**, 分別。  
  
#### 若要監視在訂閱者端等候套用的交易式命令  
  
1.  在散發資料庫的散發者端，執行 [sp_replmonitorsubscriptionpendingcmds](../../../relational-databases/system-stored-procedures/sp-replmonitorsubscriptionpendingcmds-transact-sql.md)。 這會為所有使用此「散發者」的訂閱傳回所有暫止命令的監視資訊。 若要限制結果集，以暫止命令的訂閱屬於單一 「 發行者 」，「 訂閱者 」、 發行集或已發行的資料庫指定 **@publisher**, ，**@subscriber**, ，**@publication**, ，或 **@publisher_db**, 分別。  
  
#### 若要監視等候上傳或下載的合併變更  
  
1.  在發行集資料庫的發行者，執行 [sp_showpendingchanges](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md)。 這會傳回結果集，顯示正等候複寫至「訂閱者」之變更的相關資訊。 若要將結果集限制為屬於單一發行集或發行項的變更，請分別指定 **@publication** 或 **@article**。  
  
2.  在訂閱者 」 在訂閱資料庫上，執行 [sp_showpendingchanges](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md)。 這會傳回結果集，顯示正等候複寫至「發行者」之變更的相關資訊。 若要將結果集限制為屬於單一發行集或發行項的變更，請分別指定 **@publication** 或 **@article**。  
  
#### 若要監視合併代理程式的工作階段  
  
1.  在散發資料庫的散發者端，執行 [sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md)。 這會傳回監視資訊，包括 **Session_id**, ，使用此散發者的所有訂閱的所有合併代理程式工作階段。 您也可以取得 **Session_id** 藉由查詢 [MSmerge_sessions](../../../relational-databases/system-tables/msmerge-sessions-transact-sql.md) 系統資料表。  
  
2.  在散發資料庫的散發者端，執行 [sp_replmonitorhelpmergesessiondetail](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md)。 指定 **Session_id** 步驟 1 中的值 **@session_id**。 這會顯示有關工作階段的詳細監視資訊。  
  
3.  針對每個感興趣的工作階段重複步驟 2。  
  
#### 若要從訂閱者監視提取訂閱的合併代理程式工作階段  
  
1.  在訂閱資料庫上的 「 訂閱者 」 執行 [sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md)。 針對給定的訂閱，指定 **@publisher**, ，**@publication**, ，以及發行集資料庫的名稱 **@publisher_db**。 這會傳回此訂閱最後五個「合併代理程式」工作階段的監視資訊。 記下的值 **Session_id** 在結果中的工作階段設定。  
  
2.  在訂閱資料庫上的 「 訂閱者 」 執行 [sp_replmonitorhelpmergesessiondetail](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md)。 指定 **Session_id** 步驟 1 中的值 **@session_id**。 這會顯示有關工作階段的詳細監視資訊。  
  
3.  針對每個感興趣的工作階段重複步驟 2。  
  
#### 若要檢視和修改發行集的監視臨界值標準  
  
1.  在散發資料庫的散發者端，執行 [sp_replmonitorhelppublicationthresholds](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublicationthresholds-transact-sql.md)。 這會傳回為所有使用此「散發者」的發行集所設定的監視臨界值。 若要限制結果集，以監視屬於單一 「 發行者 」 或已發行的資料庫或單一發行集的發行集的臨界值，指定 **@publisher**, ，**@publisher_db**, ，或 **@publication**, 分別。 記下的值 **Metric_id** 之必須變更任何臨界值。 如需詳細資訊，請參閱 [設定臨界值和複寫監視器 」 中的警告](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。  
  
2.  在散發資料庫的散發者端，執行 [sp_replmonitorchangepublicationthreshold](../../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md)。 視需要指定下列項目：  
  
    -    **Metric_id** 為步驟 1 中取得的值 **@metric_id**。  
  
    -   針對 **@value**指定監視臨界值標準的新值。  
  
    -   針對 **@shouldalert** ，指定 **1** 的值以在達到此臨界值時記錄警示，或者如果不需要警示，則指定 **0** 的值。  
  
    -   針對 **@mode** ，指定 **1** 的值以啟用監視臨界值標準；或指定 **2** 的值加以停用。  
  
##  <a name="RMO"></a> Replication Management Objects (RMO)  
  
#### 若要監視訂閱者端合併式發行集的訂閱  
  
1.  建立連接到訂閱者使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor> 類別，並設定 <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publisher%2A>, ，<xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publication%2A>, ，<xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.PublisherDB%2A>, ，<xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.SubscriberDB%2A> 訂用帳戶，並設定屬性 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 1 中建立。  
  
3.  呼叫下列其中一個方法，以傳回此訂閱的「合併代理程式」工作階段的相關資訊：  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A> -傳回的陣列 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> 物件上多達最後五個合併代理程式工作階段資訊。 請注意 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> 感興趣的任何工作階段的值。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A> -傳回的陣列 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> 物件做為在經過的小時數期間發生的合併代理程式工作階段的相關資訊 *小時* （多達最後五個工作階段中） 的參數。 請注意 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> 感興趣的任何工作階段的值。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummary%2A> -傳回 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> 最後的合併代理程式工作階段的相關資訊的物件。 請注意 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> 此工作階段的值。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummaryDataSet%2A> -傳回 <xref:System.Data.DataSet> 多達最後五個合併代理程式工作階段，每個資料列的其中一個物件的資訊上。 記下的值 **Session_id** 感興趣的任何工作階段的資料行。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummaryDataRow%2A> -傳回 <xref:System.Data.DataRow> 最後的合併代理程式工作階段的相關資訊的物件。 記下的值 **Session_id** 此工作階段的資料行。  
  
4.  （選擇性）呼叫 <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A> 若要重新整理的資料 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> 物件傳遞為 *mss，* 或呼叫 <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A> 中的資料重新整理 <xref:System.Data.DataRow> 物件傳遞為 *drRefresh*。  
  
5.  使用步驟 3 中取得的工作階段識別碼，呼叫下列其中一個方法來傳回有關特定工作階段詳細資料的資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetails%2A> -傳回的陣列 <xref:Microsoft.SqlServer.Replication.MergeSessionDetail> 所提供的物件 *SessionId*。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetailsDataSet%2A> -傳回 <xref:System.Data.DataSet> 物件的指定資訊 *SessionId*。  
  
#### 若要監視在散發者端所有發行集的複寫屬性  
  
1.  建立連接到散發者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.ReplicationMonitor> 類別。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 1 中建立。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。  
  
5.  執行下列其中一或多個方法，以針對使用此散發者的所有發行者傳回複寫資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumDistributionAgents%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含這個散發者端的所有散發代理程式的相關資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumErrorRecords%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含儲存在 「 散發者 」 的錯誤的相關資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumLogReaderAgents%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含所有的記錄讀取器代理程式在散發者的相關資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMergeAgents%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含所有的合併代理程式，在散發者的相關資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMiscellaneousAgents%2A> -傳回 <xref:System.Data.DataSet> 包含散發者端的所有其他複寫代理程式的相關資訊的物件。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含這個散發者端的所有發行者的相關資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers2%2A> -傳回 <xref:System.Data.DataSet> 傳回發行者使用此散發者的物件。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgents%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含所有的佇列讀取器代理程式在散發者的相關資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessionDetails%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含有關所指定的佇列讀取器代理程式和工作階段的詳細資料。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessions%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含指定的佇列讀取器代理程式的工作階段資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumSnapshotAgents%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含所有的快照集代理程式在散發者的相關資訊。  
  
#### 若要監視在散發者端特定發行者的發行集屬性  
  
1.  建立連接到散發者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  取得 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 中下列其中一種物件。  
  
    -   建立的執行個體 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 類別。 設定 <xref:Microsoft.SqlServer.Replication.PublisherMonitor.Name%2A> 發行者，並設定屬性 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 1 中建立。 呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。 如果此方法傳回 **false**，則表示「發行者」名稱定義不正確，或者該發行集不存在。  
  
    -   從 <xref:Microsoft.SqlServer.Replication.PublisherMonitorCollection> 藉由存取 <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.PublisherMonitors%2A> 屬性的現有 <xref:Microsoft.SqlServer.Replication.ReplicationMonitor> 物件。  
  
3.  執行下列其中一或多個方法，針對屬於此「發行者」的所有發行集傳回複寫資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessionDetails%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含有關所指定的散發代理程式和工作階段的詳細資料。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessions%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含有關指定散發代理程式工作階段資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumErrorRecords%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含有關所指定錯誤的錯誤記錄資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessionDetails%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含指定的記錄讀取器代理程式和工作階段的詳細資料。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessions%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含指定的記錄讀取器代理程式工作階段資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含有關所指定的合併代理程式和工作階段的詳細資料。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails2%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含有關指定之合併代理程式和工作階段的其他詳細資料。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含指定的合併代理程式的工作階段資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions2%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含指定的合併代理程式的其他工作階段資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含這個散發者端的所有發行集的資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications2%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含這個散發者端的所有發行集的其他資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessionDetails%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含有關指定之快照集代理程式和工作階段的詳細資料。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessions%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含指定之快照集代理程式工作階段資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSubscriptions%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含這個散發者端的發行集的所有訂閱的相關資訊。  
  
#### 若要監視散發者端特定發行集的屬性  
  
1.  建立連接到散發者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  取得 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 中下列其中一種物件。  
  
    -   建立的執行個體 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 類別。 設定 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, ，<xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, ，<xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> 發行集，並設定屬性 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 1 中建立。 呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。 如果此方法傳回 **false**，則表示發行集屬性定義不正確，或者該發行集不存在。  
  
    -   從 <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> 藉由存取 <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> 屬性的現有 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 物件。  
  
3.  執行下列其中一或多個方法，傳回有關此發行集的詳細資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumErrorRecords%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含有關所指定錯誤的錯誤記錄。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumLogReaderAgent%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含這個發行集的記錄讀取器代理程式的相關資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A> -傳回 <xref:System.Data.DataSet> 物件包含監視警告臨界值的相關資訊，設定此發行集。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumQueueReaderAgent%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含這個發行集所使用的佇列讀取器代理程式的相關資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSnapshotAgent%2A> -傳回 <xref:System.Data.DataSet> 物件，包含這個發行集快照集代理程式的相關資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.EnumSubscriptions%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含此發行集訂閱的相關資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSubscriptions2%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含訂閱此發行集的詳細資訊，根據所提供 <xref:Microsoft.SqlServer.Replication.SubscriptionResultOption>。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokenHistory%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含指定之的追蹤 token 的延遲資訊。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A> -傳回 <xref:System.Data.DataSet> 物件，其中包含所有追蹤 token 插入至此發行集的相關資訊。  
  
#### 若要監視在訂閱者端等候套用的交易式命令  
  
1.  建立連接到散發者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  取得 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 中下列其中一種物件。  
  
    -   建立的執行個體 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 類別。 設定 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, ，<xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, ，<xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> 發行集，並設定屬性 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 1 中建立。 呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。 如果此方法傳回 **false**，則表示發行集屬性定義不正確，或者該發行集不存在。  
  
    -   從 <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> 藉由存取 <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> 屬性的現有 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 物件。  
  
3.  執行 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.TransPendingCommandInfo%2A> 方法，傳回 <xref:Microsoft.SqlServer.Replication.PendingCommandInfo> 物件。  
  
4.  使用這個屬性 <xref:Microsoft.SqlServer.Replication.PendingCommandInfo> 物件，以判斷估計的暫止命令數目，以及完成傳遞這些命令時，它所需的時間長度。  
  
#### 若要設定發行集的監視器警告臨界值  
  
1.  建立連接到散發者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  取得 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 中下列其中一種物件。  
  
    -   建立的執行個體 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 類別。 設定 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, ，<xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, ，<xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> 發行集，並設定屬性 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 1 中建立。 呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。 如果此方法傳回 **false**，則表示發行集屬性定義不正確，或者該發行集不存在。  
  
    -   從 <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> 藉由存取 <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> 屬性的現有 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 物件。  
  
3.  執行 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A> 方法。 請注意目前臨界值設定在傳回 <xref:System.Collections.ArrayList> 的 <xref:Microsoft.SqlServer.Replication.MonitorThreshold> 物件。  
  
4.  執行 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.ChangeMonitorThreshold%2A> 方法。 傳遞下列參數：  
  
    -   *metricID* - <xref:System.Int32> 代表下表中的監視臨界值標準的值︰  
  
        |值|描述|  
        |-----------|-----------------|  
        |1|**到期** -監視交易式發行集的訂閱是否即將到期。|  
        |2|**延遲** -監視交易式發行集的訂閱效能。|  
        |4|**mergeexpiration** -監視合併式發行集的訂閱是否即將到期。|  
        |5|**mergeslowrunduration** -監視透過低頻寬 （撥號） 連接進行合併同步處理的持續時間。|  
        |6|**mergefastrunduration** -監視透過高頻寬 (LAN) 連接進行合併同步處理的持續時間。|  
        |7|**mergefastrunspeed** -監視透過高頻寬 (LAN) 連接進行合併同步處理的同步處理速率。|  
        |8|**mergeslowrunspeed** -監視透過低頻寬 （撥號） 連接進行合併同步處理的同步處理速率。|  
  
    -   *啟用* - <xref:System.Boolean> 值，指出是否啟用發行集的度量。  
  
    -   *thresholdValue* -設定的臨界值的整數值。  
  
    -   *shouldAlert* -整數，表示此臨界值是否應產生警示。  
  
  