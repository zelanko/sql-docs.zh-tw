---
title: "發行集屬性、訂閱選項 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.newpubwizard.pubproperties.subscriptionoptions.f1
ms.assetid: 31abd605-b273-419d-86df-d0ecf539a507
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a2b1050183fa56189cb4985d3c19283d9e5d7b3c
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
# <a name="publication-properties-subscription-options"></a>發行集屬性，訂閱選項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **[發行集屬性]** 對話方塊的 **[訂閱選項]** 頁面，可以讓您檢視和設定訂閱相關聯的發行集層級屬性。 屬性會依下列類別目錄分組：  
  
-   套用至所有發行集的屬性。  
  
-   套用至快照式和交易式發行集的屬性 (包括允許更新訂閱的發行集)。  
  
-   套用至合併式發行集的屬性。  
  
> [!NOTE]  
>  部分屬性是唯讀的；此主題的屬性描述有討論原因。 部分屬性變更需要發行集的新快照集，且部分也需要重新初始化所有訂閱。 如需詳細資訊，請參閱[變更發行集與發行項屬性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
## <a name="options-for-all-publications"></a>所有發行集的選項  
  
### <a name="creation-and-synchronization"></a>建立與同步處理  
 **允許匿名訂閱**  
 決定是否允許匿名提取訂閱。 匿名訂閱支援 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEWEd2005](../../includes/ssewed2005-md.md)], [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssMobileEd2005](../../includes/ssmobileed2005-md.md)]版和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for Windows CE。 若要在快照式和交易式發行集使用此選項， **[快照集永遠可使用]** 選項就必須設定為 **[True]**。  
  
 **可附加訂閱資料庫**  
 決定是否可以附加訂閱資料庫的副本來建立訂閱 (快照式和交易式發行集的 **[快照集永遠可使用]** 選項必須設定為 **[True]** )。  
  
> [!IMPORTANT]  
>  未來的版本將不再提供可附加訂閱。 這項功能已被取代。  
  
 **允許提取訂閱**  
 決定是否允許訂閱者建立此發行集的提取訂閱。 如需詳細資訊，請參閱[訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)。  
  
### <a name="schema-replication"></a>結構描述複寫  
 **複寫結構描述變更**  
 僅限[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本。 決定是否複寫結構描述變更 (例如，加入資料行至資料表或變更資料行的資料類型) 至發行的物件。 如需詳細資訊，請參閱[對發行集資料庫進行結構描述變更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
## <a name="options-for-snapshot-and-transactional-publications"></a>快照式和交易式發行集的選項  
  
### <a name="creation-and-synchronization"></a>建立與同步處理  
 **獨立散發代理程式**  
 決定是否使用與此資料庫之其他發行集無關的代理程式。 此選項是唯讀的；針對使用新增發行集精靈所建立的發行集，預設為 **[True]** ，而且在發行集建立後就無法變更。 如需詳細資訊，請參閱[複寫代理程式管理](../../relational-databases/replication/agents/replication-agent-administration.md)。  
  
 **[快照集永遠可使用]**  
 決定是否每次執行快照集代理程式時都會建立快照集檔案 (需要 **[獨立散發代理程式]**)。 此選項是唯讀的；如果您在「新增發行集精靈」的 **[快照集代理程式]** 頁面上選取 **[立即建立快照集，並保留快照集為可使用狀態，以初始化訂閱]** (預設值)，此選項就會設定為 **[True]** 。 如需詳細資訊，請參閱[建立和套用快照集](../../relational-databases/replication/create-and-apply-the-snapshot.md)。  
  
 **允許從備份檔案初始化。**  
 僅限[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本。 決定是否允許使用備份檔案來初始化訂閱。 如需詳細資訊，請參閱 [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)中手動初始化訂閱。  
  
 **允許非 SQL Server 訂閱者**  
 僅限[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本。 決定發行集是否支援非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者。 將此選項設定為 **[True]** ，就會將其他發行集屬性設定為支援非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者。 如果訂閱已存在，此選項會是唯讀的；如果 **[允許立即更新訂閱]** 、 **[允許佇列更新訂閱]**或 **[允許點對點訂閱]**設定為 **[True]** ，則此選項無法設定為 **[True]**。 如需詳細資訊，請參閱 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)。  
  
### <a name="data-transformation"></a>資料轉換  
 **允許資料轉換**  
 決定在資料散發至訂閱者之前，是否使用 Data Transformation Services (DTS) 來轉換資料。 此選項是唯讀的；只有在使用預存程序建立發行集時，才能啟用資料轉換。  
  
> [!IMPORTANT]  
>  未來的版本將不再提供可轉換的訂閱。 這項功能已被取代。  
  
### <a name="peer-to-peer-replication"></a>點對點複寫  
 **[True]**  
 僅適用於 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本。 決定發行集是否支援點對點複寫。 將此選項設定為 **[True]** ，就會將其他發行集屬性設定為支援點對點複寫。 如果訂閱存在，這個選項就是唯讀的。 如果 [允許立即更新訂閱]  、[允許佇列更新訂閱]  或 [允許非 SQL Server 訂閱者] 設定為 [True]  ，此選項就無法設定為 [True] 。 如需相關資訊，請參閱 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 **允許點對點衝突偵測**  
 僅適用於 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本。 指定這個發行集是否啟用衝突偵測。 若要使用衝突偵測，所有節點都必須執行 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更新版本，而且您必須針對所有節點啟用偵測。 若要使用衝突偵測，您也必須指定 [對等建立者識別碼] 的值。如需詳細資訊，請參閱 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)。  
  
 **對等訂閱者識別碼**  
 僅適用於 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本。 針對點對點拓撲中的節點指定識別碼。 如果 **[允許點對點衝突偵測]** 設定為 **[True]**，這個識別碼就會用於衝突偵測。 請指定拓撲中從未使用過的非零正數識別碼。 如需已經使用的識別碼清單，請查詢 [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) 系統資料表。  
  
### <a name="updatable-subscriptions"></a>可更新的訂閱  
 **[允許佇列更新訂閱]**  
 決定訂閱者資料的變更是否可立即複寫至發行者。 此選項是唯讀的，只有在建立發行集時才能啟用更新訂閱。 如需詳細資訊，請參閱 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)。  
  
 **[允許點對點訂閱]**  
 決定訂閱者資料的變更是否可先排入佇列，稍後再複寫至發行者。 此選項是唯讀的，只有在建立發行集時才能啟用更新訂閱。 如需詳細資訊，請參閱 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)。  
  
 **集中報告衝突**  
 決定是否只在發行者端報告資料變更的衝突，或在發行者和訂閱者兩端都報告 (需要啟用 **[允許佇列更新訂閱]**選項)。 此選項是唯讀的；針對使用新增發行集精靈所建立的發行集，預設為 **[True]** ，而且在發行集建立後就無法變更。 **[True]** 值表示衝突只會在發行者端報告。 衝突只能在其報告處檢視。  
  
 **衝突解決原則**  
 指定當訂閱者的變更和發行者的變更發生衝突時，所要採取的動作 (需要啟用 **[允許佇列更新訂閱]**選項)。 如需詳細資訊，請參閱 [Queued Updating Conflict Detection and Resolution](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)。  
  
 **佇列類型**  
 決定是否使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 佇列或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing (MSMQ) 將訂閱者端的變更排入佇列，直到可以套用至發行者為止 (需要啟用 **[允許佇列更新訂閱]**選項)。 此選項只適用於 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]。更新版本一律會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表執行佇列。  
  
## <a name="options-for-merge-publications"></a>合併式發行集的選項  
  
### <a name="conflict-reporting"></a>衝突報告  
 **集中報告衝突**  
 決定是否只在發行者端報告資料變更的衝突，或在發行者和訂閱者兩端都報告。 此選項是唯讀的；針對使用新增發行集精靈所建立的發行集，預設為 **[True]** ，而且在發行集建立後就無法變更。 **[True]** 值表示衝突只會在發行者端報告。 衝突只能在其報告處檢視。 如需詳細資訊，請參閱＜ [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)＞的「檢視衝突」一節。  
  
### <a name="filtering"></a>篩選  
 **允許參數化篩選**  
 會依據發行集是否使用參數化篩選來設定。 此選項一律會是唯讀的。 如需詳細資訊，請參閱 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)。  
  
 **驗證訂閱者**  
 決定要使用哪些功能來驗證訂閱者的資料分割是否正確。 請以逗號分隔多個值。 如需詳細資訊，請參閱[驗證合併訂閱者的資料分割資訊](../../relational-databases/replication/validate-partition-information-for-a-merge-subscriber.md)。  
  
 **預先計算資料分割**  
 僅限[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本。 決定是否事先計算哪些資料列屬於哪些資料分割，來最佳化同步處理。 如果發行集符合預先計算資料分割的準則，此設定就會預設為 **[True]** 。 如需詳細資訊，請參閱[使用預先計算的資料分割最佳化參數化篩選效能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。  
  
 **最佳化同步處理**  
 決定是否在每一個訂閱者端儲存其他中繼資料，來最佳化合併處理。 預先計算的資料分割已取代此最佳化方式；只有在 **[預先計算資料分割]** 設定為 **[False]** 時， **[最佳化同步處理]**選項才適用。 如需詳細資訊，請參閱 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)。  
  
### <a name="merge-processes"></a>合併處理  
 **限制並行處理**  
 決定是否限制可同時執行的合併代理程式數目。 如果發行集有許多可能會同時進行同步處理的發送訂閱時，通常就會使用此選項。  
  
 **並行處理最大數**  
 可同時執行的合併代理程式最大數目 (需要 **[限制並行處理]**)。 如果正在同步處理的代理程式數目超過最大值，代理程式會排入佇列，直到數目降到最大值以下為止。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [檢視及修改發行集屬性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
