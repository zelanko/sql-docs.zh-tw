---
title: sys.dm_exec_query_optimizer_memory_gateways (TRANSACT-SQL) |Microsoft Docs
description: 傳回目前用來進行節流處理並行的查詢最佳化資源信號的狀態
ms.custom: ''
ms.date: 04/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b9d36c4a67fab2f9f7c867a3ba6b7e7d01fc5d29
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38005710"
---
# <a name="sysdmexecqueryoptimizermemorygateways-transact-sql"></a>sys.dm_exec_query_optimizer_memory_gateways (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

傳回目前用來進行節流處理並行的查詢最佳化資源信號的狀態。

|「資料行」|類型|描述|  
|----------|---------------|-----------------|  
|**pool_id**|**int**|資源集區識別碼在資源管理員|  
|**name**|**sysname**|編譯閘道名稱 （小型閘道中閘道的大型閘道）|
|**max_count**|**int**|並行編譯的設定的計數上限|
|**active_count**|**int**|編譯會在此閘道目前作用中的計數|
|**waiter_count**|**int**|在此閘道的等候者數目|
|**threshold_factor**|**bigint**|定義查詢最佳化所使用的最大的記憶體部分閾值因數。  小型閘道，threshold_factor 表示最大的最佳化工具記憶體使用量，以位元組為單位的一項查詢需要能夠存取在小型閘道之前。  中型和大型閘道 threshold_factor 會顯示此閘道可用的總伺服器記憶體的部分。 計算記憶體使用量閾值，對閘道時，它做為除數。|
|**threshold**|**bigint**|下一個臨界值以位元組為單位的記憶體。  查詢，才能存取此閘道如果它的記憶體耗用量已達到此臨界值。  "-1"如果查詢不需要存取此閘道。|
|**is_active**|**bit**|是否將目前的閘道或不需要查詢。|


## <a name="permissions"></a>Permissions  
SQL Server 需要伺服器的 VIEW SERVER STATE 權限。

Azure SQL Database 需要資料庫的 VIEW DATABASE STATE 權限。


## <a name="remarks"></a>備註  
SQL Server 會使用階層式的閘道方法，節流允許並行的編譯數目。  使用三個閘道，包括小型、 中型和大型。 閘道器有助於防止的較大編譯記憶體需要取用者的整體記憶體資源耗盡。

等候閘道會導致延遲編譯。 除了編譯的延遲，節流的要求會有相關聯的 RESOURCE_SEMAPHORE_QUERY_COMPILE 等候類型累積。 RESOURCE_SEMAPHORE_QUERY_COMPILE 等候類型可能表示您的查詢會使用大量記憶體進行編譯和已用盡記憶體，或或者沒有足夠的記憶體可用的整體來說，不過可以使用的單位，在特定閘道已達上限。 輸出**sys.dm_exec_query_optimizer_memory_gateways**可用來疑難排解的案例在存在記憶體不足，無法編譯查詢執行計畫。  

## <a name="examples"></a>範例  

### <a name="a-viewing-statistics-on-resource-semaphores"></a>A. 檢視資源信號的統計資料  
此 SQL Server 執行個體的目前的最佳化工具記憶體閘道統計有哪些？

```  
SELECT [pool_id], [name], [max_count], [active_count],
       [waiter_count], [threshold_factor], [threshold],
       [is_active]
FROM sys.dm_exec_query_optimizer_memory_gateways;   

```  

## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](./system-dynamic-management-views.md)   
 [執行相關的動態管理檢視和函式 &#40;Transact-SQL&#41;](./execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[如何使用 DBCC MEMORYSTATUS 命令來監視 SQL Server 2005 上的記憶體使用量](https://support.microsoft.com/help/907877/how-to-use-the-dbcc-memorystatus-command-to-monitor-memory-usage-on-sql-server-2005)
[大型查詢編譯等候 SQL Server 2014 中 RESOURCE_SEMAPHORE_QUERY_COMPILE](https://support.microsoft.com/help/3024815/large-query-compilation-waits-on-resource-semaphore-query-compile-in-sql-server-2014)
