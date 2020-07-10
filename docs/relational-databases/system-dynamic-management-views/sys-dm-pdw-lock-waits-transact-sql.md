---
title: dm_pdw_lock_waits (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8ef966f8-d14e-40d3-9626-3508ada9b8fb
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 14ce0e2aa5b99878ccf9a704defe6ed305ec04a2
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2020
ms.locfileid: "86197056"
---
# <a name="sysdm_pdw_lock_waits-transact-sql"></a>dm_pdw_lock_waits (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  保存等候鎖定之要求的相關資訊。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|要求在等候清單中的位置。|以零為基底的序數。 這在所有等候專案中都不是唯一的。|  
|session_id|**nvarchar(32)**|發生等候狀態之會話的識別碼。|請參閱[dm_pdw_exec_sessions &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)中的 session_id。|  
|類型|**nvarchar(255)**|此專案所代表的等候類型。|可能的值：<br /><br /> 共用<br /><br /> SharedUpdate<br /><br /> ExclusiveUpdate<br /><br /> 獨佔|  
|object_type|**nvarchar(255)**|受等候影響的物件類型。|可能的值：<br /><br /> OBJECT<br /><br /> DATABASE<br /><br /> 系統<br /><br /> SCHEMA<br /><br /> APPLICATION|  
|object_name|**Nvarchar (386) **|受等候影響之指定物件的名稱或 GUID。|資料表和 views 會以三個部分的名稱顯示。<br /><br /> 索引和統計資料會顯示四部分名稱。<br /><br /> 名稱、主體和資料庫都是字串名稱。|  
|request_id|**nvarchar(32)**|發生等候狀態之要求的識別碼。|要求的識別碼。<br /><br /> 這是載入要求的 GUID。|  
|request_time|**datetime**|要求鎖定或資源的時間。||  
|acquire_time|**datetime**|取得鎖定或資源的時間。||  
|state|**nvarchar(50)**|等候狀態的狀態。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|等待專案的優先順序。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
