---
title: "工作負載管理 (SQL Server PDW)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/12/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 69063b1a-a8f3-453a-83ab-afbe7eb4f463
caps.latest.revision: "11"
ms.openlocfilehash: 596fba5031e3183a9278e20384d51852cea0f2b8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="workload-management"></a>工作負載管理
SQL Server PDW 的工作負載管理功能可讓使用者和系統管理員將指派到預先設定的記憶體和並行處理設定要求。 使用工作負載管理來改善效能的負載，一致或 mixed 時，允許要求而不會佔用任何要求永遠將適當的資源。  
  
例如，與在 SQL Server PDW 工作負載管理技術，您可以：  
  
-   配置大量載入作業的資源。  
  
-   指定更多資源來建立資料行存放區索引。  
  
-   疑難排解執行緩慢的雜湊聯結，看看是否需要更多記憶體，並再提供更多記憶體。  
  
## <a name="Basics"></a>工作負載管理基本概念  
  
### <a name="key-terms"></a>主要詞彙：  
工作負載管理  
*工作負載管理*是了解及調整系統資源使用情形，為了達到最佳效能的並行要求的能力。  
  
資源類別  
在 SQL Server PDW，*資源類別*是已預先指派的記憶體和並行限制的內建的伺服器角色。 SQL Server PDW 分配資源，以根據資源類別伺服器角色成員資格，會送出要求的登入要求。  
  
在計算節點上資源類別的實作會在 SQL Server 中使用資源管理員功能。 資源管理員的相關資訊，請參閱[Resource Governor](http://msdn.microsoft.com/en-us/library/bb933866(v=sql.11).aspx) MSDN 上。  
  
### <a name="understand-current-resource-utilization"></a>了解目前的資源使用率  
若要了解目前正在執行要求的系統資源使用量，請使用 SQL Server PDW 動態管理檢視。 例如，您可以使用 Dmv 來了解是否是執行緩慢的大型雜湊聯結獲益有更多記憶體。  
  
<!-- MISSING LINKS
For examples, see [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md).  
-->
  
### <a name="adjust-resource-allocations"></a>調整資源配置  
若要調整的資源使用率，變更會提交要求的登入的資源類別成員資格。 資源類別的伺服器角色會命名為**mediumrc**， **largerc**，和**xlargerc**。 它們分別代表中型、 大型和超大型資源配置。  
  
比方說，配置大量的系統資源的要求，將 送出要求的登入**largerc**伺服器角色。 下列 ALTER SERVER ROLE 陳述式會將登入 Anna 加入 largerc 伺服器角色。  
  
```sql  
ALTER SERVER ROLE largerc ADD MEMBER Anna;  
```  
  
## <a name="RC"></a>資源類別的描述  
下表描述的資源類別和其系統資源配置。  
  
|資源類別|要求的重要性|最大記憶體使用量 *|並行插槽 (上限 = 32)|Description|  
|------------------|----------------------|--------------------------|---------------------------------------|---------------|  
|預設|中|400 MB|1|根據預設，每個登入允許少量的記憶體和其要求的並行存取資源。<br /><br />登入加入至資源類別時，新的類別會優先使用。 卸除登入後從所有資源類別，登入會還原回預設資源配置。|  
|MediumRC|中|1200 MB|3|要求可能需要的媒體資源類別的範例包括：<br /><br />較大的 CTAS 作業雜湊聯結。<br /><br />選取 需要更多的記憶體，以避免快取到磁碟的作業。<br /><br />資料載入叢集資料行存放區索引。<br /><br />建置、 重建和重新組織叢集資料行存放區索引的較小的資料表有 10-15 資料行。|  
|largerc|高|2.8 GB|7|要求可能需要大量的資源類別的範例包括：<br /><br />超大型 CTAS 作業有很大的雜湊聯結或包含大型的彙總，例如大型的 ORDER BY 或 GROUP BY 子句。<br /><br />選取作業，例如雜湊聯結或彙總，例如 ORDER BY 或 GROUP BY 子句需要非常大量的記憶體的作業<br /><br />資料載入叢集資料行存放區索引。<br /><br />建置、 重建和重新組織叢集資料行存放區索引的較小的資料表有 10-15 資料行。|  
|xlargerc|高|8.4 GB|22|超大型的資源類別是針對可能需要在執行階段的額外大型的資源耗用量的要求。|  
  
<sup>*</sup>最大記憶體使用量是近似值。  
  
### <a name="request-importance"></a>要求的重要性  
要求的重要性會對應至的要求將會在計算節點上執行的 SQL Server 的 CPU 時間量。  優先順序較高的要求接收更多的 CPU 時間。  
  
### <a name="maximum-memory-usage"></a>最大記憶體使用量  
最大記憶體使用量是要求可以使用每個處理空間內的可用記憶體的最大數量。 比方說 mediumrc 要求可以使用 1200 MB 的每個發佈內處理。 務必仍然以確保資料不會扭曲若要避免執行大部分的工作數分佈。  
  
### <a name="concurrency-slots"></a>並行存取的位置  
配置 1、 3、 7 和 22 的並行存取位置的目標是允許在相同時間執行，而不會封鎖小型的程序時執行大型程序的小型和大型處理序。  例如，SQL Server PDW 可以配置最多 32 並行位置同時執行 1 項超大型要求 （22 的位置）、 1 大型要求 （7 位置） 和 1 中的要求 （3 個插槽）。  
  
配置最多 32 個並行要求的並行位置的範例包括：  
  
-   28 位置 = 4 大  
  
-   30 位置 = 10 中  
  
-   32 個位置 = 32 的預設值  
  
-   32 個位置 = 超大型 1 + 1 的大型 + 1 媒體  
  
-   32 個位置 = 2 的大型 + 4 媒體 + 6 的預設值  
  
假設 6 的大型要求提交到 SQL Server PDW，，然後提交由 10 個預設的要求。 SQL Server PDW 會處理中優先順序的要求，如下所示：  
  
-   配置 28 並行位置開始的記憶體可用時處理 4 的大型要求，並保留 2 的大型要求在佇列中。  
  
-   配置 4 的並行存取位置開始處理 4 的預設要求，並保留 6 個預設要求等候佇列中。  
  
當要求完成並並行插槽可用時，SQL Server PDW 將配置剩餘根據可用的資源和優先順序的要求。 比方說，7 位置開啟的並行存取時，等候較大的要求將會有更高的優先順序比等候中要求的 7 插槽。  如果開啟 6 的插槽，SQL Server PDW 將配置 6 更多的預設大小要求。 不過，記憶體和並行插槽所有之前必須先有 SQL Server PDW 允許執行的要求。  
  
在每個資源類別中，要求先出 (FIFO) 順序中第一個執行。  
  
## <a name="GeneralRemarks"></a>一般備註  
如果登入是一種以上的資源類別的成員，具有最多資源的類別會優先使用。  
  
加入或卸除資源類別從登入時，變更時會立即生效日後所有要求。不會影響目前的要求所執行，或等候。 登入不需要中斷連線，然後重新連線中發生變更的順序。  
  
每個登入，資源類別設定會套用至個別的陳述式和作業，並不適用於工作階段。  
  
SQL Server PDW 執行陳述式之前，它會嘗試取得要求所需的並行插槽。 如果它無法取得足夠的並行存取位置，SQL Server PDW 將移至要求執行等候的狀態。 所有已配置給要求的資源系統會傳回回系統中。  
  
大部分的 SQL 陳述式永遠需要預設的資源配置，並因此不受控制資源類別。 例如，建立登入只需要少量的資源，和即使呼叫建立登入的登入的成員配置的預設資源的資源類別。  例如，如果 Anna largerc 資源類別的成員，她將提交的 CREATE LOGIN 陳述式 CREATE LOGIN 陳述式會執行與資源的預設數目。  
  
SQL 陳述式和資源類別所控管的作業：  
  
-   ALTER INDEX REBUILD  
  
-   ALTER INDEX REORGANIZE  
  
-   ALTER 資料表重建  
  
-   建立叢集的索引  
  
-   CREATE CLUSTERED COLUMNSTORE INDEX  
  
-   建立 TABLE AS SELECT  
  
-   建立遠端 TABLE AS SELECT  
  
-   載入具有資料**dwloader**。  
  
-   INSERT SELECT  
  
-   UPDATE  
  
-   DELETE  
  
-   還原資料庫還原至應用裝置與多個運算節點時。  
  
-   選取時，不包括只有 DMV 查詢  
  
## <a name="Limits"></a>限制事項  
資源類別管理記憶體和並行的配置。  不會控制輸入/輸出作業。  
  
## <a name="Metadata"></a>中繼資料  
包含資源類別和資源類別成員的相關資訊的 Dmv。  
  
-   [sys.server_role_members](../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
-   [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
包含要求和所需的資源的狀態資訊的 Dmv:  
  
-   [sys.dm_pdw_lock_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
-   [sys.dm_pdw_resource_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
從 SQL Server Dmv 的計算節點上公開相關的系統檢視表。 請參閱[SQL Server 動態管理檢視](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)如需這些 Dmv MSDN 上的連結。  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys.dm_pdw_nodes_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys.dm_pdw_nodws_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_exec_sessions  
  
-   sys.dm_pdw_nodes_exec_requests  
  
-   sys.dm_pdw_nodes_exec_query_memory_grants  
  
-   sys.dm_pdw_nodes_exec_query_resource_semaphores  
  
-   sys.dm_pdw_nodes_os_memory_brokers  
  
-   sys.dm_pdw_nodes_os_memory_cache_entries  
  
-   sys.dm_pdw_nodes_exec_cached_plans  
  
## <a name="RelatedTasks"></a>相關的工作  
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
  
