---
title: 針對異動複寫測量延遲及驗證連接 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, performance
- tracer tokens [SQL Server replication]
- latency [SQL Server replication]
- transactional replication, tracer tokens
- monitoring performance [SQL Server replication], tracer tokens
ms.assetid: 4addd426-7523-4067-8d7d-ca6bae4c9e34
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 89149645524adedf01b8d9fb7c116cf0ab0f26c5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "62667813"
---
# <a name="measure-latency-and-validate-connections-for-transactional-replication"></a>針對異動複寫測量延遲及驗證連接
  本主題描述如何使用複寫監視器、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中測量延遲及驗證異動複寫的連接。 異動複寫具有追蹤 Token 功能，該功能會提供便利的方式來計算異動複寫拓撲中的延遲並驗證「發行者」、「散發者」及「訂閱者」之間的連接。 Token (即少量的資料) 會寫入發行集資料庫的交易記錄，會標示為典型的已複寫交易並且會透過系統傳送，它可允許計算：  
  
-   在發行者端認可交易和在散發者端之散發資料庫插入對應的命令之間，所經過的時間。  
  
-   在散發資料庫中插入命令和在訂閱者端認可對應的交易之間，所經過的時間。  
  
 根據以上計算，您可以回答許多問題，包括：  
  
-   哪些訂閱者在接收發行者的變更時，所花費的時間最長？  
  
-   預期會收到追蹤 Token 的訂閱者中，哪些沒有接收到 (如果有的話)？  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
-   **若要測量延遲及驗證連接，請使用：**  
  
     [SQL Server 複寫監視器](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects](#RMOProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
 追蹤 Token 在停止系統時也很有幫助，包括停止所有活動並確認所有節點已接收全部尚未處理的變更。 如需詳細資訊，請參閱[停止複寫拓撲 &#40;複寫 Transact-SQL 程式設計&#41;](../administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)。  
  
 若要使用追蹤 token，您必須使用的[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]特定版本：  
  
-   散發者必須為[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]或更新版本。  
  
-   「發行者」必須為 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本，或為「Oracle 發行者」。  
  
-   針對發送訂閱，如果訂閱者是[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 7.0 或更新版本，則會從發行者、散發者和訂閱者收集追蹤 token 統計資料。  
  
-   對於提取訂閱，則會從「訂閱者」收集追蹤 Token 統計資料，但只限於「訂閱者」為 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本的情況下。 如果訂閱者是[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 7.0 或[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)]，則只會從發行者和散發者收集統計資料。  
  
 以下為另外一些應注意的問題和限制：  
  
-   訂閱必須為作用狀態以便接收追蹤 Token。 如果訂閱已經過初始化，則其為作用狀態。  
  
-   重新初始化會移除相關訂閱的所有暫止追蹤 Token。  
  
-   「訂閱者」僅接收初始同步處理之後建立的追蹤 Token。  
  
-   追蹤 Token 不會透過重新發行「訂閱者」來轉送。  
  
-   在容錯移轉到次要複本之後，複寫監視器就無法調整 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 發行執行個體的名稱，而且會繼續在原始主要 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體名稱之下顯示複寫資訊。 在容錯移轉之後，便無法使用複寫監視器輸入追蹤 Token，但是可以在複寫監視器中看到在新的發行者端使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)]輸入的追蹤 Token。  
  
##  <a name="using-sql-server-replication-monitor"></a><a name="SSMSProcedure"></a>使用 SQL Server 複寫監視器  
 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](start-the-replication-monitor.md)。  
  
#### <a name="to-insert-a-tracer-token-and-view-information-on-the-token"></a>插入追蹤 Token 並檢視 Token 上的資訊  
  
1.  在左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  按一下 **[追蹤 Token]** 索引標籤。  
  
3.  按一下 **[插入追蹤]**。  
  
4.  在下列資料行中檢視追蹤 Token 的經過時間： **[發行者到散發者]**、 **[散發者到訂閱者]**、 **[延遲總計]**。 值為 [**暫**止] 表示 token 尚未到達指定的點。  
  
#### <a name="to-view-information-on-a-tracer-token-inserted-previously"></a>若要檢視先前插入之追蹤 Token 上的訊息  
  
1.  在左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  按一下 **[追蹤 Token]** 索引標籤。  
  
3.  從 **[插入的時間]** 下拉式清單中選取時間。  
  
4.  在下列資料行中檢視追蹤 Token 的經過時間： **[發行者到散發者]**、 **[散發者到訂閱者]**、 **[延遲總計]**。 值為 [**暫**止] 表示 token 尚未到達指定的點。  
  
    > [!NOTE]  
    >  追蹤 Token 資訊與其他記錄資料的保留時間週期相同，這會由散發資料庫的記錄保留期限控制。 如需變更散發資料庫屬性的詳細資訊，請參閱[檢視及修改散發者和發行者屬性](../view-and-modify-distributor-and-publisher-properties.md)。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-post-a-tracer-token-to-a-transactional-publication"></a>若要將追蹤 Token 公佈到交易式發行集  
  
1.  (選擇性) 在發行集資料庫的發行者上，執行 [sp_helppublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)。 請確認發行集存在且狀態為使用中。  
  
2.  (選擇性) 在發行集資料庫的發行者上，執行 [sp_helpsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql)。 請確認訂閱存在且狀態為使用中。  
  
3.  在發行集資料庫的發行者上，執行 [sp_posttracertoken &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql)，並指定 **@publication**。 請注意**@tracer_token_id**輸出參數的值。  
  
#### <a name="to-determine-latency-and-validate-connections-for-a-transactional-publication"></a>若要針對異動複寫判斷延遲並驗證連接  
  
1.  使用上一個程序將追蹤 Token 公佈到發行集。  
  
2.  在發行集資料庫的發行者上，執行 [sp_helptracertokens &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql)，並指定 **@publication**。 如此會傳回公佈到發行集的所有追蹤 Token 清單。 請注意結果集中所要的 **tracer_id** 。  
  
3.  在發行集資料庫的發行者上，執行 [sp_helptracertokenhistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql)，並指定 **@publication**，而且針對 **@tracer_id** 指定步驟 2 的追追蹤 Token 識別碼。 這麼做會傳回所選取追蹤 Token 的延遲資訊。  
  
#### <a name="to-remove-tracer-tokens"></a>若要移除追蹤 Token  
  
1.  在發行集資料庫的發行者上，執行 [sp_helptracertokens &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql)，並指定 **@publication**。 如此會傳回公佈到發行集的所有追蹤 Token 清單。 請注意結果集中要刪除之追蹤 Token 的 **tracer_id** 。  
  
2.  在發行集資料庫的發行者上，執行 [sp_deletetracertokenhistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql)，並指定 **@publication**，而且針對 **@tracer_id** 指定步驟 2 的要刪除的追蹤識別碼。  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> 範例 &#40;Transact-SQL&#41;  
 這麼做會公佈追蹤 Token 記錄，並使用傳回的公佈追蹤 Token 識別碼檢視延遲資訊。  
  
 [!code-sql[HowTo#sp_tracertokens](../../../snippets/tsql/SQL15/replication/howto/tsql/createtracertokens.sql#sp_tracertokens)]  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
  
#### <a name="to-post-a-tracer-token-to-a-transactional-publication"></a>若要將追蹤 Token 公佈到交易式發行集  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.TransPublication> 類別的執行個體。  
  
3.  設定發行集的 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 屬性，並將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為在步驟 1 中建立的連接。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回 `false`，則表示步驟 3 中的發行集屬性定義不正確，或者該發行集不存在。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.TransPublication.PostTracerToken%2A> 方法。 此方法會將追蹤 Token 插入至發行集的交易記錄。  
  
#### <a name="to-determine-latency-and-validate-connections-for-a-transactional-publication"></a>若要針對異動複寫判斷延遲並驗證連接  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與散發者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 類別的執行個體。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A>、 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>、 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>和 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A> 屬性，並將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為在步驟 1 中建立的連接。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回 `false`，則表示步驟 3 中的發行集監視器屬性定義不正確，或者該發行集不存在。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A> 方法。 將傳回的 <xref:System.Collections.ArrayList> 物件轉換為 <xref:Microsoft.SqlServer.Replication.TracerToken> 物件的陣列。  
  
6.  呼叫 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokenHistory%2A> 方法。 針對步驟 5 的追蹤 Token 傳遞 <xref:Microsoft.SqlServer.Replication.TracerToken.TracerTokenId%2A> 的值。 這麼做會以 <xref:System.Data.DataSet> 物件傳回所選取追蹤 Token 的延遲資訊。 如果傳回所有的追蹤 Token，則「發行者」和「散發者」之間的連接以及「散發者」和「訂閱者」之間的連接兩者都存在，且複寫拓撲可以運作。  
  
#### <a name="to-remove-tracer-tokens"></a>若要移除追蹤 Token  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與散發者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 類別的執行個體。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A>、 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>、 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>和 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A> 屬性，並將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為在步驟 1 中建立的連接。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回 `false`，則表示步驟 3 中的發行集監視器屬性定義不正確，或者該發行集不存在。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A> 方法。 將傳回的 <xref:System.Collections.ArrayList> 物件轉換為 <xref:Microsoft.SqlServer.Replication.TracerToken> 物件的陣列。  
  
6.  呼叫 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.CleanUpTracerTokenHistory%2A> 方法。 傳遞其中一個值：  
  
    -   步驟 5 追蹤 Token 的 <xref:Microsoft.SqlServer.Replication.TracerToken.TracerTokenId%2A> 。 這麼做會刪除所選取 Token 的資訊。  
  
    -   <xref:System.DateTime> 物件。 這麼做會刪除所有早於指定日期和時間的 Token 資訊。  
  
###  <a name="PShellExample"></a>  
