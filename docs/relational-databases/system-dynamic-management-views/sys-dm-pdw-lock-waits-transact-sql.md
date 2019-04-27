---
title: sys.dm_pdw_lock_waits (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: a376ac534182f5ebdae8a3af5e32f9c4a536f8aa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62668220"
---
# <a name="sysdmpdwlockwaits-transact-sql"></a>sys.dm_pdw_lock_waits (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保留的要求正在等待鎖定的相關資訊。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|要求的等候清單中的位置。|0 為基底的序數。 這不是唯一在所有等候的項目。|  
|session_id|**nvarchar(32)**|發生等候狀態的工作階段識別碼。|請參閱中的 session_id [sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。|  
|型別|**nvarchar(255)**|此項目所代表的等候類型。|可能的值如下：<br /><br /> 共用<br /><br /> SharedUpdate<br /><br /> ExclusiveUpdate<br /><br /> 排除|  
|object_type|**nvarchar(255)**|等候受影響的物件型別。|可能的值如下：<br /><br /> OBJECT<br /><br /> DATABASE<br /><br /> SYSTEM<br /><br /> SCHEMA<br /><br /> APPLICATION|  
|object_name|**nvarchar(386)**|指定等候受影響之物件的 GUID 或名稱。|資料表和檢視表會顯示使用三部分名稱。<br /><br /> 索引和統計資料會顯示四部分名稱。<br /><br /> 名稱、 主體及資料庫是字串名稱。|  
|request_id|**nvarchar(32)**|等候狀態發生所在之要求的識別碼。|要求的識別碼。<br /><br /> 這是載入要求的 GUID。|  
|request_time|**datetime**|要求的鎖定或資源的時間。||  
|acquire_time|**datetime**|取得的鎖定或資源的時間。||  
|state|**nvarchar(50)**|等候狀態的狀態。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|等候項目的優先順序。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
