---
title: sys.databases dm_exec_external_operations （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_EXTERNAL_OPERATIONS_TSQL
- DM_EXEC_EXTERNAL_OPERATIONS
- SYS.DM_EXEC_EXTERNAL_OPERATIONS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- sys.dm_exec_external_operations management view
- dm_exec_external_operations management view
ms.assetid: d268217a-85b8-4b7f-9cd1-87865eba2be1
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d410afc256f0a1c12694f826bc73570cfee84172
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68097782"
---
# <a name="sysdm_exec_external_operations-transact-sql"></a>sys.databases dm_exec_external_operations （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  捕捉外部 PolyBase 作業的相關資訊。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|與 PolyBase 查詢相關聯的唯一查詢識別碼|請參閱[dm_exec_requests &#40;transact-sql](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)中的識別碼&#41;|  
|step_index|**int**|查詢步驟的索引|請參閱 sys.databases 中的 step_index [dm_exec_distributed_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)|  
|operation_ 類型|**nvarchar(128)**|描述 Hadoop 作業或其他外部作業|「外部 Hadoop 作業」|  
|operation_ 名稱|**nvarchar(4000)**|指出作業的狀態（以百分比表示）（已耗用的輸入量）|0-1-乘以係數100（已完成）|  
|map_ 進度|**float**|指出減少工作的狀態（以百分比表示）（如果有的話）|0-1-乘以係數100（已完成）|  
  
## <a name="see-also"></a>另請參閱  
 [使用動態管理檢視進行 PolyBase 疑難排解](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [動態管理 Views 和函數 &#40;Transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [資料庫相關的動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
