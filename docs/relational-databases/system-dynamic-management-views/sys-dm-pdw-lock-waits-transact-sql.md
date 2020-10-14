---
description: 'sys.dm_pdw_lock_waits (Transact-sql) '
title: sys.dm_pdw_lock_waits (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: 0e3ddfbf5c6bb0aaa06a28091bce99c90bf4beb6
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035347"
---
# <a name="sysdm_pdw_lock_waits-transact-sql"></a>sys.dm_pdw_lock_waits (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  保存正在等候鎖定之要求的相關資訊。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|要求在等候清單中的位置。|以零為基底的序數。 這在所有等候專案中都不是唯一的。|  
|session_id|**nvarchar(32)**|等候狀態發生所在之會話的識別碼。|請參閱 [sys.dm_pdw_exec_sessions &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)中的 session_id。|  
|type|**nvarchar(255)**|此專案代表的等候類型。|可能的值：<br /><br /> 共用<br /><br /> SharedUpdate<br /><br /> ExclusiveUpdate<br /><br /> 獨佔|  
|object_type|**nvarchar(255)**|受等候影響的物件類型。|可能的值：<br /><br /> OBJECT<br /><br /> DATABASE<br /><br /> 系統<br /><br /> SCHEMA<br /><br /> APPLICATION|  
|object_name|**Nvarchar (386) **|受等候影響之指定物件的名稱或 GUID。|資料表和視圖會以三部分名稱顯示。<br /><br /> 索引和統計資料會以四部分名稱顯示。<br /><br /> 名稱、主體和資料庫都是字串名稱。|  
|request_id|**nvarchar(32)**|等候狀態發生所在要求的識別碼。|要求的識別碼。<br /><br /> 這是載入要求的 GUID。|  
|request_time|**datetime**|要求鎖定或資源的時間。||  
|acquire_time|**datetime**|取得鎖定或資源的時間。||  
|狀態|**nvarchar(50)**|等候狀態的狀態。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|等候專案的優先權。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
## <a name="see-also"></a>另請參閱  
 [Azure Synapse Analytics 和平行處理資料倉儲動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
