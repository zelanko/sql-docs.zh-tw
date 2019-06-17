---
title: sys.dm_exec_compute_node_errors (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_COMPUTE_NODE_ERRORS_TSQL
- DM_EXEC_COMPUTE_NODE_ERRORS
- DM_EXEC_COMPUTE_NODE_ERRORS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase
- PolyBase, views
- dm_exec_compute_node_errors
- sys.dm_exec_compute_node_errors management view
ms.assetid: 9a03c039-70e4-4974-95d8-d3fa45984ffb
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b5a11a5e7090f89f4a31ffd15f8ebbce78ea395a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63013394"
---
# <a name="sysdmexeccomputenodeerrors-transact-sql"></a>sys.dm_exec_compute_node_errors (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  傳回錯誤發生在 PolyBase 計算節點。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|error_id|**nvarchar(36)**|與錯誤相關聯的唯一數值識別碼。|系統中的所有查詢錯誤|  
|來源|**nvarchar(255)**|來源執行緒或處理序的描述||  
|type|**nvarchar(255)**|錯誤的類型。||  
|create_time|**datetime**|錯誤發生時間||  
|compute_node_id|**int**|特定的計算節點的識別碼|請參閱的 compute_node_id [sys.dm_exec_compute_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)|  
|rexecution_id|**nvarchar(36)**|PolyBase 查詢，如果有任何識別項。||  
|spid|**int**|SQL Server 工作階段識別項||  
|thread_id|**int**|發生錯誤之執行緒的數值識別碼。||  
|詳細資料|nvarchar(4000)|完整描述錯誤的詳細資料。||  
  
## <a name="see-also"></a>另請參閱  
 [PolyBase 疑難排解動態管理檢視](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [與資料庫相關動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
