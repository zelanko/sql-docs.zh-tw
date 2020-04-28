---
title: 工作負載管理
description: 分析平臺系統中的工作負載管理。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: d14714cb23a9f6b0d6cc63ddca5049cb6741017c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74399438"
---
# <a name="workload-management-in-analytics-platform-system"></a>分析平臺系統中的工作負載管理

SQL Server PDW 的工作負載管理功能可讓使用者和系統管理員將要求指派給預先設定的記憶體和並行處理。 使用工作負載管理可讓要求擁有適當的資源，而不需要永遠 starvation 任何要求，以改善工作負載的效能（不論是一致或混合的）。  
  
例如，使用 SQL Server PDW 中的工作負載管理技巧，您可以：  
  
-   將大量資源配置給載入作業。  
  
-   指定更多資源來建立資料行存放區索引。  
  
-   針對執行緩慢的雜湊聯結進行疑難排解，以查看它是否需要更多記憶體，然後提供更多記憶體。  
  
## <a name="workload-management-basics"></a><a name="Basics"></a>工作負載管理基本概念  
  
### <a name="key-terms"></a>主要詞彙：  
工作負載管理  
*工作負載管理*是瞭解及調整系統資源使用率的能力，以便達到並行要求的最佳效能。  
  
資源類別  
在 SQL Server PDW 中，*資源類別*是一種內建的伺服器角色，具有預先指派的記憶體和並行限制。 SQL Server PDW 會根據提交要求之登入的資源類別伺服器角色成員資格，將資源配置給要求。  
  
在計算節點上，資源類別的執行會使用 SQL Server 中的 Resource Governor 功能。 如需 Resource Governor 的詳細資訊，請參閱 MSDN 上的[Resource Governor](../relational-databases/resource-governor/resource-governor.md) 。  
  
### <a name="understand-current-resource-utilization"></a>瞭解目前的資源使用率  
若要瞭解目前正在執行之要求的系統資源使用量，請使用 [SQL Server PDW 動態管理] 視圖。 例如，您可以使用 Dmv 來瞭解緩慢執行的大型雜湊聯結是否可以因擁有更多記憶體而受益。  
  
<!-- MISSING LINKS
For examples, see [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md).  
-->
  
### <a name="adjust-resource-allocations"></a>調整資源配置  
若要調整資源使用率，請變更提交要求之登入的資源類別成員資格。 資源類別伺服器角色的名稱為**mediumrc**、 **largerc**和**xlargerc**。 它們分別代表中型、大型和超大型資源配置。  
  
例如，若要將大量系統資源配置給要求，請將提交要求的登入新增至**largerc**伺服器角色。 下列 ALTER SERVER ROLE 語句會將登入 Anna 新增至 largerc 伺服器角色。  
  
```sql  
ALTER SERVER ROLE largerc ADD MEMBER Anna;  
```  
  
## <a name="resource-class-descriptions"></a><a name="RC"></a>資源類別描述  
下表描述資源類別及其系統資源配置。  
  
|資源類別|要求重要性|最大記憶體使用量 *|平行存取插槽數（最大值 = 32）|描述|  
|------------------|----------------------|--------------------------|---------------------------------------|---------------|  
|default|中|400 MB|1|根據預設，每個登入都允許少量的記憶體和並行處理資源來處理其要求。<br /><br />當登入新增至資源類別時，新的類別會優先使用。 從所有資源類別中卸載登入時，登入會還原回預設資源配置。|  
|MediumRC|中|1200 MB|3|可能需要中型資源類別的要求範例：<br /><br />CTAS 具有大型雜湊聯結的作業。<br /><br />選取需要更多記憶體的作業，以避免快取至磁片。<br /><br />將資料載入叢集資料行存放區索引。<br /><br />針對具有10-15 資料行的小型資料表，建立、重建和重新組織叢集資料行存放區索引。|  
|Largerc|高|2.8 GB|7|可能需要大型資源類別的要求範例：<br /><br />非常大型的 CTAS 作業，具有大量的雜湊聯結或包含大型的匯總，例如大型 ORDER BY 或 GROUP BY 子句。<br /><br />針對雜湊聯結之類的作業，或 ORDER BY 或 GROUP BY 子句之類的匯總，選取需要海量儲存體的作業<br /><br />將資料載入叢集資料行存放區索引。<br /><br />針對具有10-15 資料行的小型資料表，建立、重建和重新組織叢集資料行存放區索引。|  
|xlargerc|高|8.4 GB|22|超大型資源類別適用于在執行時間需要額外耗用大量資源的要求。|  
  
<sup>*</sup>最大記憶體使用量是近似值。  
  
### <a name="request-importance"></a>要求重要性  
要求重要性會對應到在計算節點上執行 SQL Server 的 CPU 時間量，以提供給要求。  優先順序較高的要求會接收更多的 CPU 時間。  
  
### <a name="maximum-memory-usage"></a>最大記憶體使用量  
最大記憶體使用量是要求可在每個處理空間內使用的可用記憶體數量上限。 例如，mediumrc 要求在每個散發內最多可以使用 1200 MB 來處理。 確保資料不會扭曲，以避免有幾個散發執行大部分的工作，仍然很重要。  
  
### <a name="concurrency-slots"></a>平行存取插槽  
配置1、3、7和22平行存取插槽的目標，是要讓大型和小型進程同時執行，而不會在執行大型進程時封鎖小型進程。  例如，SQL Server PDW 可以配置最多32個平行存取插槽來執行1個額外的大型要求（22個位置）、1個大型要求（7個位置）和1個中型要求（3個位置）。  
  
將最多32個平行存取插槽配置給並行要求的範例：  
  
-   28個插槽 = 4 大  
  
-   30插槽 = 10 中型  
  
-   32插槽 = 32 預設值  
  
-   32插槽 = 1 個超大型 + 1 大型 + 1 中型  
  
-   32插槽 = 2 大型 + 4 中型 + 6 預設值  
  
假設有6個大型要求提交至 SQL Server PDW，然後提交10個預設要求。 SQL Server PDW 會依照下列連續處理要求：  
  
-   配置28個平行存取插槽，以便在記憶體可供使用時開始處理4個大型要求，並在佇列中保留2個大型要求。  
  
-   配置4個平行存取插槽以開始處理4個預設要求，並在等候佇列中保留6個預設要求。  
  
當要求完成且並行位置可供使用時，SQL Server PDW 會根據可用的資源和優先順序來配置剩餘的要求。 例如，當開啟7個平行存取插槽時，等待大型要求的優先順序會高於等待中型要求的7個位置。  如果開啟6個位置，SQL Server PDW 會配置6個預設大小的要求。 不過，記憶體和平行存取插槽必須全部都可以使用，SQL Server PDW 才允許執行要求。  
  
在每個資源類別中，要求會以先進先出（FIFO）循序執行。  
  
## <a name="general-remarks"></a><a name="GeneralRemarks"></a>一般備註  
如果登入是一個以上資源類別的成員，則會優先使用具有大部分資源的類別。  
  
在資源類別中加入或卸載登入時，此變更會立即針對所有未來的要求生效;目前正在執行或等待中的要求不會受到影響。 登入不需要中斷連線再重新連線，即可進行變更。  
  
針對每個登入，資源類別設定會套用至個別的語句和作業，而不會套用至會話。  
  
在 SQL Server PDW 執行語句之前，它會嘗試取得要求所需的平行存取插槽。 如果它無法取得足夠的平行存取插槽，SQL Server PDW 會將要求移至等待執行的狀態。 所有已配置給要求的資源系統都會傳回給系統。  
  
大部分的 SQL 語句一律需要預設的資源配置，因此不會受到資源類別的控制。 例如，建立登入只需要少量的資源，而且即使登入呼叫建立登入是資源類別的成員，也會配置預設資源。  例如，如果 Anna 是 largerc 資源類別的成員，而她提交 CREATE LOGIN 語句，CREATE LOGIN 語句就會以預設的資源數來執行。  
  
由資源類別控管的 SQL 語句和作業：  
  
-   ALTER INDEX REBUILD  
  
-   ALTER INDEX REORGANIZE  
  
-   ALTER TABLE REBUILD  
  
-   建立叢集索引  
  
-   CREATE CLUSTERED COLUMNSTORE INDEX  
  
-   CREATE TABLE AS SELECT  
  
-   建立遠端資料表做為選取  
  
-   使用**dwloader**載入資料。  
  
-   INSERT-SELECT  
  
-   UPDATE  
  
-   刪除  
  
-   還原到具有更多計算節點的應用裝置時，還原資料庫。  
  
-   選取，排除僅限 DMV 的查詢  
  
## <a name="limitations-and-restrictions"></a><a name="Limits"></a>限制事項  
資源類別會管理記憶體和並行配置。  它們不會管理輸入/輸出作業。  
  
## <a name="metadata"></a><a name="Metadata"></a>中繼資料  
Dmv，其中包含資源類別和資源類別成員的相關資訊。  
  
-   [sys.server_role_members](../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
-   [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
Dmv，其中包含要求狀態和所需資源的相關資訊：  
  
-   [sys.dm_pdw_lock_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
-   [sys.dm_pdw_resource_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
從計算節點上的 SQL Server Dmv 公開的相關系統檢視。 如需這些 Dmv 的連結，請參閱 MSDN 上的[SQL Server 動態管理檢視](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)。  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys.dm_pdw_nodes_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys. dm_pdw_nodws_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_exec_sessions  
  
-   sys.dm_pdw_nodes_exec_requests  
  
-   sys.dm_pdw_nodes_exec_query_memory_grants  
  
-   sys.dm_pdw_nodes_exec_query_resource_semaphores  
  
-   sys.dm_pdw_nodes_os_memory_brokers  
  
-   sys.dm_pdw_nodes_os_memory_cache_entries  
  
-   sys.dm_pdw_nodes_exec_cached_plans  
  
## <a name="related-tasks"></a><a name="RelatedTasks"></a>相關工作  
[工作負載管理工作](workload-management-tasks.md)  
  
<!-- MISSING LINKS
See the Workload Management section of [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md) for the following tasks:  
  
1.  Find the number of active requests for each resource group.  
  
2.  Determine if my requests need more memory  
  
3.  Determine if there are a high number of query optimizations or suboptimal plan generations.  
  
4.  Determine Average CPU time per request in each resource pool to date  
  
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
