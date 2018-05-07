---
title: sys.dm_exec_query_optimizer_memory_gateways (TRANSACT-SQL) |Microsoft 文件
description: 傳回目前用來進行節流處理並行的查詢最佳化資源信號的狀態
ms.custom: ''
ms.date: 04/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
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
ms.openlocfilehash: 90645c4d2d0bff9716926c0260853a76d39941d5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmexecqueryoptimizermemorygateways-transact-sql"></a>sys.dm_exec_query_optimizer_memory_gateways (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

傳回目前用來進行節流處理並行的查詢最佳化資源信號的狀態。

|資料行|型別|Description|  
|----------|---------------|-----------------|  
|**pool_id**|**int**|在 資源管理員的資源集區識別碼|  
|**name**|**sysname**|編譯閘道名稱 （小型、 中型閘道大閘道）|
|**max_count**|**int**|並行編譯目的設定的計數上限|
|**active_count**|**int**|編譯此閘道中的目前計數|
|**waiter_count**|**int**|此閘道中的等候者數目|
|**threshold_factor**|**bigint**|定義查詢最佳化所使用的最大記憶體部分臨界值比例。  小型的閘道，threshold_factor 表示最大最佳化工具記憶體使用量，以位元組為單位的一個查詢要求來存取在小型閘道前。  中型和大型閘道 threshold_factor 會顯示總伺服器記憶體可供此閘道的一部分。 計算此閘道的記憶體使用量閾值時，它做為除數。|
|**threshold**|**bigint**|下一個臨界值以位元組為單位的記憶體。  查詢，才能存取此閘道如果其記憶體耗用量到達此臨界值。  "-1"如果查詢不需要存取這個閘道器。|
|**is_active**|**bit**|是否將目前的閘道，或不需要查詢。|


## <a name="permissions"></a>Permissions  
SQL Server 需要在伺服器上的 VIEW SERVER STATE 權限。

Azure SQL Database 需要資料庫的 VIEW DATABASE STATE 權限。


## <a name="remarks"></a>備註  
SQL Server 會使用階層式的閘道方法以啟用節流設定允許的並行編譯數目。  三個閘道使用，包括小型、 中型和大小。 閘道有助於避免較大編譯記憶體需要取用者的整體記憶體資源耗盡。

等候閘道中的結果延遲編譯。 編譯的延遲，除了節流的要求會有相關聯的 RESOURCE_SEMAPHORE_QUERY_COMPILE 等候類型累積。 RESOURCE_SEMAPHORE_QUERY_COMPILE 等候類型可能表示編譯的查詢使用大量的記憶體和已用盡記憶體，或或者沒有足夠的記憶體可用整體而言，不過可用單位特定的閘道已用完。 輸出**sys.dm_exec_query_optimizer_memory_gateways**可以用於疑難排解案例在先前存在記憶體不足，無法編譯查詢執行計畫。  

## <a name="examples"></a>範例  

### <a name="a-viewing-statistics-on-resource-semaphores"></a>A. 檢視資源信號的統計資料  
目前此執行個體的 SQL Server 最佳化工具記憶體閘道統計有哪些？

```  
SELECT [pool_id], [name], [max_count], [active_count],
       [waiter_count], [threshold_factor], [threshold],
       [is_active]
FROM sys.dm_exec_query_optimizer_memory_gateways;   

```  

## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](./system-dynamic-management-views.md)   
 [執行相關動態管理檢視和函數&#40;Transact SQL&#41;](./execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[如何使用 DBCC MEMORYSTATUS 命令來監視 SQL Server 2005 上的記憶體使用量](https://support.microsoft.com/help/907877/how-to-use-the-dbcc-memorystatus-command-to-monitor-memory-usage-on-sql-server-2005)
[大型查詢編譯等候這項 SQL Server 2014 中 RESOURCE_SEMAPHORE_QUERY_COMPILE](https://support.microsoft.com/help/3024815/large-query-compilation-waits-on-resource-semaphore-query-compile-in-sql-server-2014)
