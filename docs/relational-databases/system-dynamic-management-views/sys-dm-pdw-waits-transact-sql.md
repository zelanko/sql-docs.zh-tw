---
description: 'sys.dm_pdw_waits (Transact-sql) '
title: sys.dm_pdw_waits (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5130e498-1c77-4ae3-a80b-9aae396494e9
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: 3a3e3e4754b831b28be323c194f9eef70bd64f9b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477189"
---
# <a name="sysdm_pdw_waits-transact-sql"></a>sys.dm_pdw_waits (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  保存執行要求或查詢期間所遇到之所有等候狀態的相關資訊，包括鎖定、等候傳輸佇列等等。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|與等候狀態相關聯的唯一數值識別碼。<br /><br /> 此視圖的索引鍵。|系統中的所有等候都是唯一的。|  
|session_id|**nvarchar(32)**|等候狀態發生所在之會話的識別碼。|請參閱 [sys.dm_pdw_exec_sessions &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)中的 session_id。|  
|類型|**nvarchar(255)**|此專案代表的等候類型。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|object_type|**nvarchar(255)**|受等候影響的物件類型。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|object_name|**Nvarchar (386)**|受等候影響之指定物件的名稱或 GUID。||  
|request_id|**nvarchar(32)**|等候狀態發生所在要求的識別碼。|請參閱 [sys.dm_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)中的 request_id。|  
|request_time|**datetime**|要求等候狀態的時間。||  
|acquire_time|**datetime**|取得鎖定或資源的時間。||  
|state|**nvarchar(50)**|等候狀態的狀態。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|等候專案的優先權。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
## <a name="see-also"></a>另請參閱  
 [Azure Synapse Analytics 和平行處理資料倉儲動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [sys.dm_pdw_wait_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-wait-stats-transact-sql.md)  
  
  
