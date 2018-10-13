---
title: Analytics Platform System 中的工作負載管理 |Microsoft Docs
description: Analytics Platform System 中的工作負載管理。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e602cacff0c8f92b2a7748f4113a5a2ec2f34947
ms.sourcegitcommit: 485e4e05d88813d2a8bb8e7296dbd721d125f940
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2018
ms.locfileid: "49100375"
---
# <a name="workload-management-in-analytics-platform-system"></a>Analytics Platform System 中的工作負載管理

SQL Server PDW 的工作負載管理功能可讓使用者和系統管理員指派要求預先設定的記憶體和並行存取的設定。 使用工作負載管理以改善一致或混合式工作負載的效能可讓要求而不造成任何要求永遠有適當的資源。  
  
例如，SQL Server PDW 中，工作負載管理技巧，您可以：  
  
-   配置大量載入作業的資源。  
  
-   指定建立資料行存放區索引的更多資源。  
  
-   疑難排解執行緩慢的雜湊聯結，看看是否需要更多的記憶體，然後為它提供更多的記憶體。  
  
## <a name="Basics"></a>工作負載管理基本概念  
  
### <a name="key-terms"></a>主要詞彙：  
工作負載管理  
*工作負載管理*是了解及調整的系統資源使用率，以達到並行要求的最佳效能的能力。  
  
資源類別  
在 SQL Server PDW 中，*資源類別*是已預先指派的限制的記憶體和並行存取的內建的伺服器角色。 SQL Server PDW 配置根據資源類別伺服器角色成員資格，提交要求的登入要求的資源。  
  
在計算節點上，資源類別的實作會在 SQL Server 中使用資源管理員功能。 如需資源管理員的詳細資訊，請參閱[Resource Governor](../relational-databases/resource-governor/resource-governor.md) MSDN 上。  
  
### <a name="understand-current-resource-utilization"></a>了解目前的資源使用率  
若要了解目前正在執行要求的系統資源使用率，使用 SQL Server PDW 動態管理檢視。 例如，您可以使用 Dmv 以了解是否執行緩慢的大型雜湊聯結獲益的更多的記憶體。  
  
<!-- MISSING LINKS
For examples, see [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md).  
-->
  
### <a name="adjust-resource-allocations"></a>調整資源配置  
若要調整的資源使用率，變更會提交要求的登入的資源類別成員資格。 資源類別的伺服器角色會命名為**mediumrc**， **largerc**，並**xlargerc**。 它們分別代表中型、 大型和超大型資源配置。  
  
比方說，若要配置大量的系統資源的要求，新增 送出要求的登入**largerc**伺服器角色。 下列 ALTER SERVER ROLE 陳述式會將登入 Anna 將 largerc 伺服器角色。  
  
```sql  
ALTER SERVER ROLE largerc ADD MEMBER Anna;  
```  
  
## <a name="RC"></a>資源類別描述  
下表描述的資源類別和其系統資源配置。  
  
|資源類別|要求的重要性|最大記憶體使用量 *|並行存取插槽 (上限 = 32)|描述|  
|------------------|----------------------|--------------------------|---------------------------------------|---------------|  
|預設|中|400 MB|1|根據預設，每個登入允許少量的記憶體和並行存取資源，其要求。<br /><br />登入新增至資源類別時，新的類別會優先使用。 登入卸除所有的資源類別時, 登入會還原回預設資源配置中。|  
|MediumRC|中|1200 MB|3|可能需要之中型資源類別的要求範例：<br /><br />較大的 CTAS 作業雜湊聯結。<br /><br />選取 需要更多的記憶體，以避免快取到磁碟的作業。<br /><br />資料載入叢集資料行存放區索引。<br /><br />建置、 重建和重新組織叢集資料行存放區索引的較小的資料表有 10 到 15 的資料行。|  
|Largerc|高|2.8 GB|7|可能需要大型資源類別的要求範例：<br /><br />超大型 CTAS 作業有很大的雜湊聯結或包含大型的彙總，例如大型的 ORDER BY 或 GROUP BY 子句。<br /><br />選取作業，例如雜湊聯結或彙總，例如 ORDER BY 或 GROUP BY 子句中需要非常大量的記憶體的作業<br /><br />資料載入叢集資料行存放區索引。<br /><br />建置、 重建和重新組織叢集資料行存放區索引的較小的資料表有 10 到 15 的資料行。|  
|xlargerc|高|8.4 GB|22|超大型資源類別是針對可能需要在執行階段的超大型資源耗用量的要求。|  
  
<sup>*</sup>最大記憶體使用量是近似值。  
  
### <a name="request-importance"></a>要求的重要性  
要求的重要性對應至的計算節點上執行的 SQL Server 可讓要求的 CPU 時間量。  具有較高優先順序的要求會收到更多的 CPU 時間。  
  
### <a name="maximum-memory-usage"></a>最大記憶體使用量  
最大記憶體使用量會是個要求可以使用每個處理空間內的可用記憶體的最大數量。 比方說 mediumrc 要求可以使用最多有 1200 MB 的每個散發內的處理。 它是以確保資料不會扭曲若要避免執行大部分工作的幾個散發套件仍然很重要。  
  
### <a name="concurrency-slots"></a>並行存取插槽  
配置 1、 3、 7 和 22 的並行存取插槽的目標是允許在相同時間執行，而不會封鎖小型的程序，當大型的處理序正在執行的大型和小型程序。  例如，SQL Server PDW 可以配置最多 32 個並行位置同時執行 1 個超大型要求 （22 位置）、 1 個大型要求 （7 的位置） 和 1 個中型要求 （3 個插槽）。  
  
配置最多可包含 32 個並行要求的並行存取插槽的範例：  
  
-   28 位置 = 4 大  
  
-   30 位置 = 10 中  
  
-   32 個位置 = 32 的預設值  
  
-   32 個位置 = 超大型 1 + 1 的大型 + 1 媒體  
  
-   32 個位置 = 2 的大型 + 4 媒體 + 6 的預設值  
  
假設 6 個大型要求提交給 SQL Server PDW 中，然後提交 10 個預設的要求。 SQL Server PDW 會處理中優先順序的要求，如下所示：  
  
-   配置 28 的並行存取插槽，若要開始處理 4 個大型要求，因為記憶體可供使用，並保留在佇列中的 2 的大量要求。  
  
-   開始處理 4 個預設要求的 4 個並行存取插槽的配置和保留 6 個的預設要求等候佇列中。  
  
當要求完成並變成可用的並行存取插槽時，SQL Server PDW 會配置剩餘的要求，根據可用的資源和優先順序。 比方說，7 的並行存取插槽開啟時，等候大型的要求會有較高的優先權比等候中要求 7 的位置。  如果 6 的位置開啟時，SQL Server PDW 將配置 6 更多的預設大小要求。 不過，記憶體和並行存取插槽都必須使用 SQL Server PDW 允許執行的要求之前。  
  
在每個資源類別中，要求會在先進先出 (FIFO) 順序執行。  
  
## <a name="GeneralRemarks"></a>一般備註  
如果登入是一個以上的資源類別的成員，大多數的資源類別的優先順序較高。  
  
當登入加入或卸除資源類別時，變更將會立即針對所有未來的要求; 的效果不會影響目前的要求是執行中或等候。 登入不需要中斷連線，然後重新連線以便進行變更。  
  
每個登入，資源類別設定會套用至個別的陳述式和作業，而非工作階段。  
  
SQL Server PDW 執行陳述式之前，它會嘗試取得要求所需的並行存取插槽。 如果它無法取得足夠的並行位置，則 SQL Server PDW 會將要求進入執行等候的狀態。 已配置給要求的所有資源系統會都傳回到系統中。  
  
大部分的 SQL 陳述式永遠需要預設的資源配置，並因此不受資源類別。 比方說，建立登入只需要少量的資源，，和已配置的預設資源，即使呼叫建立的登入的登入的資源類別的成員。  比方說，如果 Anna 為 largerc 資源類別的成員，她將提交的 CREATE LOGIN 陳述式 CREATE LOGIN 陳述式會使用預設的資源數目。  
  
SQL 陳述式和作業都受到資源類別控管：  
  
-   ALTER INDEX REBUILD  
  
-   ALTER INDEX REORGANIZE  
  
-   重建資料表的 ALTER  
  
-   建立叢集的索引  
  
-   CREATE CLUSTERED COLUMNSTORE INDEX  
  
-   CREATE TABLE AS SELECT  
  
-   CREATE REMOTE TABLE AS SELECT  
  
-   使用載入資料**dwloader**。  
  
-   INSERT SELECT  
  
-   UPDATE  
  
-   Delete  
  
-   還原資料庫還原到具有多個計算節點的應用裝置時。  
  
-   選取時，不包括僅限 DMV 的查詢  
  
## <a name="Limits"></a>限制事項  
資源類別控管記憶體和並行存取的配置。  不會控制輸入/輸出作業。  
  
## <a name="Metadata"></a>中繼資料  
包含資源類別和資源類別成員的相關資訊的 Dmv。  
  
-   [sys.server_role_members](../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
-   [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
包含要求和所需的資源的狀態資訊的 Dmv:  
  
-   [sys.dm_pdw_lock_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
-   [sys.dm_pdw_resource_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
從 SQL Server Dmv，在計算節點上公開相關的系統檢視表。 請參閱[SQL Server 動態管理檢視](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)如需這些 Dmv 在 MSDN 上的連結。  
  
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
  
