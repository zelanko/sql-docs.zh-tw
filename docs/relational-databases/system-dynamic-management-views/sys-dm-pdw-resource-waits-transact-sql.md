---
title: sys.dm_pdw_resource_waits (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a43ce9a2-5261-41e3-97f0-555ba05ebed9
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 6089b18ba68dab6c0d667b0a1ae6397788679ee7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmpdwresourcewaits-transact-sql"></a>sys.dm_pdw_resource_waits (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  顯示等候中的所有資源類型的資訊[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|等待清單中要求的位置。|0 為起始的序數。 這不是唯一在所有等候的項目。|  
|session_id|**nvarchar(32)**|發生等候狀態的工作階段識別碼。|請參閱中的 session_id [sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。|  
|型別|**nvarchar(255)**|此項目所代表的等候類型。|可能的值如下：<br /><br /> 連接<br /><br /> 本機查詢並行<br /><br /> 分散式的查詢並行<br /><br /> DMS 並行<br /><br /> 備份的並行存取|  
|object_type|**nvarchar(255)**|等候受影響的物件類型。|可能的值如下：<br /><br /> **OBJECT**<br /><br /> **DATABASE**<br /><br /> **SYSTEM**<br /><br /> **SCHEMA**<br /><br /> **應用程式**|  
|object_name|**nvarchar(386)**|指定等候受影響之物件的 GUID 或名稱。|資料表和檢視表會顯示具有三部分名稱。<br /><br /> 索引和統計資料會顯示的四部分名稱。<br /><br /> 名稱、 主體和資料庫是字串名稱。|  
|request_id|**nvarchar(32)**|等候狀態發生所在之要求的識別碼。|要求的 //WWW.AMAZON.COM/APPLIED-MICROSOFT-SERVER-ANALYSIS-SERVICES/DP/0976635356/REF 識別項。<br /><br /> 載入要求的 GUID 識別碼。|  
|request_time|**datetime**|要求的鎖定或資源的時間。||  
|acquire_time|**datetime**|取得的鎖定或資源的時間。||  
|state|**nvarchar(50)**|等候狀態的狀態。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|等候項目的優先權。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|concurrency_slots_used|**int**|並行插槽數目 (最大值 32) 保留給此要求。|1 – SmallRC<br /><br /> 3 – MediumRC<br /><br /> 7 代表 LargeRC<br /><br /> 22 – 對於 XLargeRC|  
|resource_class|**nvarchar(20)**|此要求的資源類別。|SmallRC<br /><br /> MediumRC<br /><br /> LargeRC<br /><br /> XLargeRC|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
