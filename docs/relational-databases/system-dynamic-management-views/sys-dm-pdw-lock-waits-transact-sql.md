---
title: "sys.dm_pdw_lock_waits (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 8ef966f8-d14e-40d3-9626-3508ada9b8fb
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 659b4750c0cad521cdc34fe7b07763dea7238581
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwlockwaits-transact-sql"></a>sys.dm_pdw_lock_waits (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保留正在等待鎖定之要求的相關資訊。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|等待清單中要求的位置。|0 為起始的序數。 這不是唯一在所有等候的項目。|  
|session_id|**nvarchar （32)**|發生等候狀態的工作階段識別碼。|請參閱中的 session_id [sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|型別|**nvarchar(255)**|此項目所代表的等候類型。|可能的值如下：<br /><br /> 共用<br /><br /> SharedUpdate<br /><br /> ExclusiveUpdate<br /><br /> 排除|  
|object_type|**nvarchar(255)**|等候受影響的物件類型。|可能的值如下：<br /><br /> OBJECT<br /><br /> DATABASE<br /><br /> SYSTEM<br /><br /> SCHEMA<br /><br /> APPLICATION|  
|object_name|**nvarchar （386)**|指定等候受影響之物件的 GUID 或名稱。|資料表和檢視表會顯示具有三部分名稱。<br /><br /> 索引和統計資料會顯示的四部分名稱。<br /><br /> 名稱、 主體和資料庫是字串名稱。|  
|request_id|**nvarchar （32)**|等候狀態發生所在之要求的識別碼。|要求的識別碼。<br /><br /> 這是載入要求的 GUID。|  
|request_time|**datetime**|要求的鎖定或資源的時間。||  
|acquire_time|**datetime**|取得的鎖定或資源的時間。||  
|state|**nvarchar(50)**|等候狀態的狀態。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|等候項目的優先權。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
## <a name="see-also"></a>請參閱＜  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
