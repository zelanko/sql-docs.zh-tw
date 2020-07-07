---
title: sys.databases dm_exec_query_optimizer_memory_gateways （Transact-sql）
description: 傳回用來節流並行查詢優化的資源信號目前狀態
ms.custom: seo-dt-2019
ms.date: 04/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: language-reference
f1_keywords:
- dm_exec_query_optimizer_memory_gateways_TSQL
- dm_exec_query_optimizer_memory_gateways
- sys.dm_exec_query_optimizer_memory_gateways_TSQL
- sys.dm_exec_query_optimizer_memory_gateways
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_optimizer_memory_gateways dynamic management view
author: josack
ms.author: josack
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: da47c1b31551abd538adca6a447ac57a3fc429ff
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86005192"
---
# <a name="sysdm_exec_query_optimizer_memory_gateways-transact-sql"></a>sys.databases dm_exec_query_optimizer_memory_gateways （Transact-sql）
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

傳回用來節流並行查詢優化的資源信號目前狀態。

|資料行|類型|描述|  
|----------|---------------|-----------------|  
|**pool_id**|**int**|Resource Governor 下的資源集區識別碼|  
|**name**|**sysname**|編譯閘道名稱（小型閘道、中型閘道、大型閘道）|
|**max_count**|**int**|最大設定的並行編譯計數|
|**active_count**|**int**|此閘道目前的使用中編譯計數|
|**waiter_count**|**int**|此閘道中的等候者數目|
|**threshold_factor**|**bigint**|此臨界值因數會定義查詢優化所使用的最大記憶體部分。  針對小型閘道，threshold_factor 會在需要取得小型閘道的存取權之前，指出一個查詢的最大優化工具記憶體使用量（以位元組為單位）。  對於中型和大型閘道，threshold_factor 會顯示此閘道可用的總伺服器記憶體的部分。 計算閘道的記憶體使用量臨界值時，會使用它做為除數。|
|**threshold**|**bigint**|下一個閾值記憶體（以位元組為單位）。  如果此閘道的記憶體耗用量達到此閾值，則需要此查詢才能取得此閘道的存取權。  如果不需要查詢即可取得此閘道的存取權，則為 "-1"。|
|**is_active**|**bit**|查詢是否需要傳遞目前的閘道。|


## <a name="permissions"></a>權限  
SQL Server 需要伺服器的 VIEW SERVER STATE 許可權。

Azure SQL Database 需要資料庫的 VIEW DATABASE STATE 許可權。


## <a name="remarks"></a>備註  
SQL Server 使用分層閘道方法來節流允許的並行編譯數目。  系統會使用三個閘道，包括 small、medium 和 big。 閘道可透過較大的編譯記憶體，協助防止耗盡整體記憶體資源-需要取用者。

等待閘道產生延遲的編譯。 除了編譯中的延遲，節流的要求也會有相關聯的 RESOURCE_SEMAPHORE_QUERY_COMPILE 等候類型累積。 RESOURCE_SEMAPHORE_QUERY_COMPILE 等候類型可能表示查詢正在使用大量的記憶體進行編譯，而且記憶體已用盡，或有足夠的記憶體可供整體使用，但是特定閘道上的可用單位已耗盡。 當記憶體不足以編譯查詢執行計畫時，可以使用**dm_exec_query_optimizer_memory_gateways**的輸出進行疑難排解。  

## <a name="examples"></a>範例  

### <a name="a-viewing-statistics-on-resource-semaphores"></a>A. 查看資源信號的統計資料  
這個 SQL Server 的實例目前的優化工具記憶體閘道統計資料為何？

```  
SELECT [pool_id], [name], [max_count], [active_count],
       [waiter_count], [threshold_factor], [threshold],
       [is_active]
FROM sys.dm_exec_query_optimizer_memory_gateways;   

```  

## <a name="see-also"></a>另請參閱  
 [動態管理 Views 和函數 &#40;Transact-sql&#41;](./system-dynamic-management-views.md)   
 [執行相關的動態管理檢視和函式 &#40;Transact-SQL&#41;](./execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[如何使用 DBCC MEMORYSTATUS 命令監視 SQL Server 2005](https://support.microsoft.com/help/907877/how-to-use-the-dbcc-memorystatus-command-to-monitor-memory-usage-on-sql-server-2005) 
 上的記憶體使用量[大型查詢編譯會等候 SQL Server 2014 中的 RESOURCE_SEMAPHORE_QUERY_COMPILE](https://support.microsoft.com/help/3024815/large-query-compilation-waits-on-resource-semaphore-query-compile-in-sql-server-2014)
