---
title: "發行集屬性，訂閱選項 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.pubproperties.subscriptionoptions.f1"
ms.assetid: 31abd605-b273-419d-86df-d0ecf539a507
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 發行集屬性，訂閱選項
  **[發行集屬性]** 對話方塊的 **[訂閱選項]** 頁面，可以讓您檢視和設定訂閱相關聯的發行集層級屬性。 屬性會依下列類別目錄分組：  
  
-   套用至所有發行集的屬性。  
  
-   套用至快照式和交易式發行集的屬性 (包括允許更新訂閱的發行集)。  
  
-   套用至合併式發行集的屬性。  
  
> [!NOTE]  
>  部分屬性是唯讀的；此主題的屬性描述有討論原因。 部分屬性變更需要發行集的新快照集，且部分也需要重新初始化所有訂閱。 如需詳細資訊，請參閱 [變更發行集與發行項屬性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
## 所有發行集的選項  
  
### 建立與同步處理  
 **允許匿名訂閱**  
 決定是否允許匿名提取訂閱。 匿名訂閱支援 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEWEd2005](../../includes/ssewed2005-md.md)], [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssMobileEd2005](../../includes/ssmobileed2005-md.md)]版和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for Windows CE。 若要在快照式和交易式發行集使用此選項， **[快照集永遠可使用]** 選項就必須設定為 **[True]**。  
  
 **可附加訂閱資料庫**  
 判斷是否可以藉由附加訂閱資料庫的複本建立訂閱 (需要的選項 **快照集永遠可使用** 設為 **True** 快照式和交易式發行集)。  
  
> [!IMPORTANT]  
>  未來的版本將不再提供可附加訂閱。 這項功能已被取代。  
  
 **允許提取訂閱**  
 決定是否允許訂閱者建立此發行集的提取訂閱。 如需詳細資訊，請參閱 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)。  
  
### 結構描述複寫  
 **複寫結構描述變更**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本。 決定是否複寫結構描述變更 (例如，加入資料行至資料表或變更資料行的資料類型) 至發行的物件。 如需詳細資訊，請參閱 [對發行集資料庫進行結構描述變更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
## 快照式和交易式發行集的選項  
  
### 建立與同步處理  
 **獨立散發代理程式**  
 決定是否使用與此資料庫之其他發行集無關的代理程式。 這個選項是唯讀的。設定為 **True** 依預設使用新的發行集精靈 」 建立發行集，且之後就無法變更發行集建立。 如需詳細資訊，請參閱 [複寫代理程式管理](../../relational-databases/replication/agents/replication-agent-administration.md)。  
  
 **快照集永遠可使用**  
 決定是否將快照集檔案，建立每次執行快照集代理程式 (需要 **獨立散發代理程式**)。 這個選項是唯讀的。設定為 **True** 如果您選取 **立即建立快照集，並保留快照集可用來初始化訂閱** 上 **快照集代理程式** 新發行集精靈 」 （預設值） 的頁面。 如需詳細資訊，請參閱 [建立並套用快照集](../../relational-databases/replication/create-and-apply-the-snapshot.md)。  
  
 **允許從備份檔案初始化。**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本。 決定是否允許使用備份檔案來初始化訂閱。 如需詳細資訊，請參閱 [初始化交易式訂閱不使用快照集](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)。  
  
 **允許非 SQL Server 訂閱者**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本。 決定發行集是否支援非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者。 這個選項設成 **True** 設定其他發行集屬性，以支援非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 「 訂閱者 」。 這個選項是唯讀如果訂閱存在。不能設 **True** 如果 **允許立即更新訂閱**, ，**允許佇列更新訂閱**, ，或 **允許對等訂閱** 設為 **True**。 如需詳細資訊，請參閱 [非 SQL Server 訂閱者](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)。  
  
### 資料轉換  
 **允許資料轉換**  
 決定在資料散發至訂閱者之前，是否使用 Data Transformation Services (DTS) 來轉換資料。 此選項是唯讀的；只有在使用預存程序建立發行集時，才能啟用資料轉換。  
  
> [!IMPORTANT]  
>  未來的版本將不再提供可轉換的訂閱。 這項功能已被取代。  
  
### 點對點複寫  
 **允許點對點訂閱**  
 僅適用於 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本。 決定發行集是否支援點對點複寫。 這個選項設成 **True** 設定其他發行集屬性，以支援端對端複寫。 如果訂閱存在，這個選項就是唯讀的。 這個選項不能設 **True** 如果 **允許立即更新訂閱** 或 **允許佇列更新訂閱**, ，或 **允許非 SQL Server 訂閱** 設為 **True**。 如需詳細資訊，請參閱 [端對端交易式複寫](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 **允許點對點衝突偵測**  
 僅適用於 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本。 指定這個發行集是否啟用衝突偵測。 若要使用衝突偵測，所有節點都必須執行 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更新版本，而且您必須針對所有節點啟用偵測。 若要使用衝突偵測，您也必須指定 [對等建立者識別碼] 的值。 如需詳細資訊，請參閱 [中端對端複寫的衝突偵測](../../relational-databases/replication/transactional/conflict-detection-in-peer-to-peer-replication.md)。  
  
 **對等訂閱者識別碼**  
 僅適用於 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本。 針對點對點拓撲中的節點指定識別碼。 此識別碼用於衝突偵測，如果 **允許對等衝突偵測** 設為 **True**。 請指定拓撲中從未使用過的非零正數識別碼。 已使用的識別碼清單，如查詢 [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) 系統資料表。  
  
### 可更新的訂閱  
 **允許立即更新訂閱**  
 決定訂閱者資料的變更是否可立即複寫至發行者。 此選項是唯讀的，只有在建立發行集時才能啟用更新訂閱。 如需詳細資訊，請參閱 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)。  
  
 **允許佇列更新訂閱**  
 決定訂閱者資料的變更是否可先排入佇列，稍後再複寫至發行者。 此選項是唯讀的，只有在建立發行集時才能啟用更新訂閱。 如需詳細資訊，請參閱 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)。  
  
 **集中報告衝突**  
 決定是否要報告資料變更衝突只能在 「 發行者 」 或 「 發行者 」 和 「 訂閱者 」 (要求選項 **允許佇列更新訂閱**)。 這個選項是唯讀的。設定為 **True** 依預設使用新的發行集精靈 」 建立發行集，且之後就無法變更發行集建立。 **[True]** 值表示衝突只會在發行者端報告。 衝突只能在其報告處檢視。  
  
 **衝突解決原則**  
 指定要與發行者變更發生衝突的訂閱者變更時所採取的動作 (要求選項 **允許佇列更新訂閱**)。 如需詳細資訊，請參閱 [Queued Updating Conflict Detection and Resolution](../../relational-databases/replication/transactional/queued-updating-conflict-detection-and-resolution.md)。  
  
 **佇列類型**  
 決定是否要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 佇列或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 訊息佇列 (MSMQ) 在訂閱者 」 可將它們套用到 「 發行者 」 之前的佇列變更 (需要選擇 **允許佇列更新訂閱**)。 此選項只適用於 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]。更新版本一律會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表執行佇列。  
  
## 合併式發行集的選項  
  
### 衝突報告  
 **集中報告衝突**  
 決定是否只在發行者端報告資料變更的衝突，或在發行者和訂閱者兩端都報告。 這個選項是唯讀的。設定為 **True** 依預設使用新的發行集精靈 」 建立發行集，且之後就無法變更發行集建立。 **[True]** 值表示衝突只會在發行者端報告。 衝突只能在其報告處檢視。 如需詳細資訊，請參閱＜ [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)＞的「檢視衝突」一節。  
  
### 篩選  
 **允許參數化篩選**  
 會依據發行集是否使用參數化篩選來設定。 此選項一律會是唯讀的。 如需詳細資訊，請參閱 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
 **驗證訂閱者**  
 決定要使用哪些功能來驗證訂閱者的資料分割是否正確。 請以逗號分隔多個值。 如需詳細資訊，請參閱 [驗證合併訂閱者的資料分割資訊](../../relational-databases/replication/validate-partition-information-for-a-merge-subscriber.md)。  
  
 **預先計算資料分割**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本。 決定是否事先計算哪些資料列屬於哪些資料分割，來最佳化同步處理。 如果發行集符合預先計算資料分割的準則，此設定就會預設為 **[True]** 。 如需詳細資訊，請參閱 [最佳化 Parameterized Filter Performance with Precomputed Partitions](../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md)。  
  
 **最佳化同步處理**  
 決定是否在每一個訂閱者端儲存其他中繼資料，來最佳化合併處理。 預先計算的資料分割已取代此最佳化方式；只有在 **[預先計算資料分割]** 設定為 **[False]** 時， **[最佳化同步處理]**選項才適用。 如需詳細資訊，請參閱 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
### 合併處理  
 **限制並行處理**  
 決定是否限制可同時執行的合併代理程式數目。 如果發行集有許多可能會同時進行同步處理的發送訂閱時，通常就會使用此選項。  
  
 **並行處理最大數**  
 可以同時執行的合併代理程式的數目上限 (需要 **限制並行處理**)。 如果正在同步處理的代理程式數目超過最大值，代理程式會排入佇列，直到數目降到最大值以下為止。  
  
## 另請參閱  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [檢視及修改發行集屬性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  