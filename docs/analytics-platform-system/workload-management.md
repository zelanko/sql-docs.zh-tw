---
title: 工作負載管理
description: Analytics Platform System 中的工作負載管理。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: d14714cb23a9f6b0d6cc63ddca5049cb6741017c
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "74399438"
---
# <a name="workload-management-in-analytics-platform-system"></a>Analytics Platform System 中的工作負載管理

SQL Server PDW 的工作負載管理功能，可讓使用者和系統管理員將要求指派給預先設定的記憶體設定和並行處理。 使用工作負載管理可讓要求具有適當的資源，而不需永遠 starvation 任何要求，以改善工作負載的效能（不論一致或混合）。  
  
例如，利用 SQL Server PDW 中的工作負載管理技術，您可以：  
  
-   配置大量資源給載入作業。  
  
-   指定更多資源以建立資料行存放區索引。  
  
-   針對執行緩慢的雜湊聯結進行疑難排解，以查看它是否需要更多記憶體，然後提供更多的記憶體。  
  
## <a name="workload-management-basics"></a><a name="Basics"></a>工作負載管理基本概念  
  
### <a name="key-terms"></a>主要詞彙：  
工作負載管理  
*工作負載管理* 是瞭解及調整系統資源使用率的能力，以達成並行要求的最佳效能。  
  
資源類別  
在 SQL Server PDW 中， *資源類別* 是內建的伺服器角色，具有預先指派的記憶體和平行存取限制。 SQL Server PDW 會根據提交要求之登入的資源類別伺服器角色成員資格，將資源配置給要求。  
  
在計算節點上，資源類別的執行會使用 SQL Server 中的 Resource Governor 功能。 如需 Resource Governor 的詳細資訊，請參閱 MSDN 上的 [Resource Governor](../relational-databases/resource-governor/resource-governor.md) 。  
  
### <a name="understand-current-resource-utilization"></a>瞭解目前的資源使用量  
若要瞭解目前正在執行之要求的系統資源使用量，請使用 SQL Server PDW 動態管理檢視。 例如，您可以使用 Dmv 來瞭解執行緩慢的大型雜湊聯結是否可利用更多的記憶體來獲益。  
  
<!-- MISSING LINKS
For examples, see [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md).  
-->
  
### <a name="adjust-resource-allocations"></a>調整資源配置  
若要調整資源使用率，請變更提交要求之登入的資源類別成員資格。 資源類別伺服器角色會命名為 **mediumrc**、 **largerc**和 **xlargerc**。 它們分別代表中型、大型和超大型資源配置。  
  
例如，若要將大量系統資源配置給要求，請將提交要求的登入加入至 **largerc** 伺服器角色。 下列 ALTER SERVER ROLE 語句會將登入 Anna 新增至 largerc 伺服器角色。  
  
```sql  
ALTER SERVER ROLE largerc ADD MEMBER Anna;  
```  
  
## <a name="resource-class-descriptions"></a><a name="RC"></a>資源類別描述  
下表說明資源類別及其系統資源配置。  
  
|資源類別|要求重要性|記憶體使用量上限 *|並行插槽 (上限 = 32) |描述|  
|------------------|----------------------|--------------------------|---------------------------------------|---------------|  
|default|中|400 MB|1|根據預設，每個登入都允許少量的記憶體，以及其要求的平行存取資源。<br /><br />將登入新增至資源類別時，會優先使用新的類別。 從所有資源類別卸載登入時，登入就會還原回預設的資源配置。|  
|MediumRC|中|1200 MB|3|可能需要中型資源類別的要求範例：<br /><br />CTAS 具有大型雜湊聯結的作業。<br /><br />選取需要更多記憶體的作業，以避免快取到磁片。<br /><br />將資料載入叢集資料行存放區索引。<br /><br />針對具有10-15 資料行的較小資料表，建立、重建和重新組織叢集資料行存放區索引。|  
|Largerc|高|2.8 GB|7|可能需要大型資源類別的要求範例：<br /><br />具有大量雜湊聯結的大型 CTAS 作業，或包含大型匯總，例如大型 ORDER BY 或 GROUP BY 子句。<br /><br />針對雜湊聯結之類的作業或像是 ORDER BY 或 GROUP BY 子句等的匯總，選取需要極大記憶體量的作業<br /><br />將資料載入叢集資料行存放區索引。<br /><br />針對具有10-15 資料行的較小資料表，建立、重建和重新組織叢集資料行存放區索引。|  
|xlargerc|高|8.4 GB|22|超大型資源類別適用于在執行時間可能需要額外耗用大量資源的要求。|  
  
<sup>*</sup>記憶體使用量上限為近似值。  
  
### <a name="request-importance"></a>要求重要性  
要求的重要性會對應到在計算節點上執行 SQL Server 的 CPU 時間量，以提供給要求。  具有較高優先順序的要求會獲得更多的 CPU 時間。  
  
### <a name="maximum-memory-usage"></a>記憶體使用量上限  
記憶體使用量上限是要求可在每個處理空間內使用的可用記憶體數量上限。 例如，mediumrc 要求最多可在每個散發內使用 1200 MB 進行處理。 確保資料不會扭曲是很重要的，以免有幾個散發執行大部分的工作。  
  
### <a name="concurrency-slots"></a>平行存取插槽  
配置1、3、7和22個平行存取插槽的目標是同時允許大型和小型進程執行，而不會在執行大型進程時封鎖小型進程。  例如，SQL Server PDW 可以配置最多32個平行存取插槽，以執行1個額外的大型要求 (22 個位置) 、1個大型要求 (7 個插槽) ，以及1個中型要求 (3 個插槽) 。  
  
針對並行要求配置最多32個平行存取插槽的範例：  
  
-   28個插槽 = 4 個大型  
  
-   30個插槽 = 10 個中型  
  
-   32插槽 = 32 預設值  
  
-   32插槽 = 1 個超大型 + 1 大型 + 1 中型  
  
-   32插槽 = 2 大型 + 4 中型 + 6 預設值  
  
假設有6個大型要求提交給 SQL Server PDW，然後提交10個預設要求。 SQL Server PDW 會依下列連續處理要求：  
  
-   配置28個平行存取插槽，以在記憶體可用時開始處理4個大型要求，並在佇列中保留2個大型要求。  
  
-   配置4個平行存取插槽以開始處理4個預設要求，並在等候佇列中保留6個預設要求。  
  
當要求完成且平行存取插槽可供使用時，SQL Server PDW 會根據可用的資源和優先順序配置其餘的要求。 例如，當有7個並行位置開啟時，等候中的大型要求在7個插槽中的優先順序會高於等候中度要求。  如果開啟6個位置，則 SQL Server PDW 會配置6個預設大小的要求。 不過，在 SQL Server PDW 允許要求執行之前，必須全部都可以使用記憶體和平行存取插槽。  
  
在每個資源類別內，要求會先從先出 (FIFO) 順序中執行。  
  
## <a name="general-remarks"></a><a name="GeneralRemarks"></a>一般備註  
如果登入是一個以上資源類別的成員，則具有最多資源的類別會優先使用。  
  
將登入新增至資源類別或從中卸載時，變更會立即對所有未來的要求生效;目前正在執行或等候中的要求不受影響。 登入不需要中斷連接再重新連線，就會發生變更。  
  
針對每個登入，資源類別設定會套用至個別的語句和作業，而不會套用至會話。  
  
在 SQL Server PDW 執行語句之前，它會嘗試取得要求所需的平行存取插槽。 如果無法取得足夠的並行位置，SQL Server PDW 會將要求移至等待執行的狀態。 所有已配置給要求的資源系統都會傳回系統。  
  
大部分的 SQL 語句一律需要預設資源配置，因此不受資源類別控制。 例如，CREATE LOGIN 只需要少量的資源，而且即使呼叫 CREATE LOGIN 的登入是資源類別的成員，也會配置預設資源。  例如，如果 Anna 是 largerc 資源類別的成員，而她提交 CREATE LOGIN 語句，CREATE LOGIN 語句將會以預設的資源數目來執行。  
  
由資源類別控管的 SQL 語句和作業：  
  
-   ALTER INDEX REBUILD  
  
-   ALTER INDEX REORGANIZE  
  
-   ALTER TABLE REBUILD  
  
-   建立叢集索引  
  
-   CREATE CLUSTERED COLUMNSTORE INDEX  
  
-   CREATE TABLE AS SELECT  
  
-   CREATE REMOTE TABLE AS SELECT  
  
-   使用 **dwloader**載入資料。  
  
-   INSERT-SELECT  
  
-   UPDATE  
  
-   刪除  
  
-   還原至具有更多計算節點的應用裝置時，請將資料庫還原。  
  
-   選取，排除僅限 DMV 的查詢  
  
## <a name="limitations-and-restrictions"></a><a name="Limits"></a>限制事項  
資源類別會管理記憶體和並行配置。  它們不會管理輸入/輸出作業。  
  
## <a name="metadata"></a><a name="Metadata"></a>元  
Dmv，其中包含資源類別和資源類別成員的相關資訊。  
  
-   [sys.server_role_members](../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
-   [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
Dmv，其中包含要求狀態及其所需資源的相關資訊：  
  
-   [sys.dm_pdw_lock_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
-   [sys.dm_pdw_resource_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
從計算節點上的 SQL Server Dmv 公開的相關系統檢視。 請參閱 MSDN 上的 [SQL Server 動態管理檢視](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) ，以取得這些 dmv 的連結。  
  
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
  
