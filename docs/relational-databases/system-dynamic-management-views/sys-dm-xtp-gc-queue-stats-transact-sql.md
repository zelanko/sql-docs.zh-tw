---
title: sys.dm_xtp_gc_queue_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xtp_gc_stats
- dm_xtp_gc_stats_TSQL
- sys.dm_xtp_gc_stats_TSQL
- sys.dm_xtp_gc_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xtp_gc_stats dynamic management view
ms.assetid: addef774-318d-46a7-85df-f93168a800cb
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = azuresqldb-mi-current || >= sql-server-2016 || >= sql-server-linux-2017 || = sqlallproducts-allversions
ms.openlocfilehash: c56fe40ec6864ac48a991e155d06ce7c505ed593
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090204"
---
# <a name="sysdmxtpgcqueuestats-transact-sql"></a>sys.dm_xtp_gc_queue_stats (Transact-SQL)

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  伺服器上每一個記憶體回收工作者佇列的相關輸出資訊，以及有關每一個項目的各種統計資料。 每個邏輯 CPU 都有一個佇列。  
  
 主要記憶體回收執行緒 (閒置的執行緒) 會追蹤自從上一次叫用主要記憶體回收執行緒之後所完成之所有交易的已更新、刪除及插入的資料列。 當記憶體回收執行緒喚醒時，它會判斷最舊作用中交易的時間戳記是否已變更。 如果最舊的作用中交易已經變更，則閒置的執行緒會針對不再需要寫入集合的交易將工作項目加入佇列 (以 16 個資料列的區塊為單位)。 例如，如果您刪除 1,024 個資料列，您最終將會看到 64 個記憶體回收工作項目加入佇列，每個項目都包含 16 個已刪除的資料列。  使用者交易在認可之後，它會選取其排程器上所有加入佇列的項目。 如果其排程器上沒有任何項目加入佇列，使用者交易將會在目前 NUMA 節點中的任何佇列上搜尋。  
  
 您可以藉由執行 sys.dm_xtp_gc_queue_stats 來了解已加入佇列的工作是否已經在處理，藉以判斷記憶體回收是否釋出已刪除之資料列的記憶體。 如果 current_queue_depth 中的項目不會被處理，或沒有新的工作項目都會加入 current_queue_depth，這會是表示記憶體回收並未釋放記憶體。 例如，如果有長時間執行的交易，無法執行記憶體回收。  
  
 如需詳細資訊，請參閱[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  

|資料行名稱|type|描述|  
|-----------------|----------|-----------------|  
|queue_id|**int**|佇列的唯一識別碼。|  
|total_enqueues|**bigint**|自從伺服器啟動之後加入這個佇列中的記憶體回收工作項目的總數。|  
|total_dequeues|**bigint**|自從伺服器啟動之後從這個佇列清除的記憶體回收工作項目的總數。|  
|current_queue_depth|**bigint**|目前存在這個佇列中的記憶體回收工作項目的數目。 這個項目可能代表有一個或多個要進行記憶體回收的項目。|  
|maximum_queue_depth|**bigint**|這個佇列已經看到的最大深度。|  
|last_service_ticks|**bigint**|佇列上次接受服務時的 CPU 刻度。|  
  
## <a name="permissions"></a>Permissions  
 需要 VIEW SERVER STATE 權限。  
  
## <a name="user-scenario"></a>使用者案例  
 此輸出顯示，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在 4 核心上執行，或者 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體已經相似化為 4 核心：  
  
 此輸出顯示，佇列中沒有任何要處理的工作項目。 對於佇列 0 而言，自從 SQL 啟動以來已清除佇列的總工作項目數為 15625，而最大佇列深度一直是 215625。  
  
```  
queue_id total_enqueues total_dequeues current_queue_depth  maximum_queue_depth  last_service_ticks  
----------------------------------------------------------------------------------------------------  
0        15625                15625    0                    15625                1233573168347  
1        15625                15625    0                    15625                1234123295566  
2        15625                15625    0                    15625                1233569418146  
3        15625                15625    0                    15625                1233571605761  
```  
  
## <a name="see-also"></a>另請參閱  
 [記憶體最佳化的資料表動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
