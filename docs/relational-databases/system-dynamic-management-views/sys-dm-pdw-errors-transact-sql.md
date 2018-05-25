---
title: sys.dm_pdw_errors (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 944eac31-5691-432b-b9f5-f1e11c05191f
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 31f94e0424cbeafac484320adb86b0f5b6849b10
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmpdwerrors-transact-sql"></a>sys.dm_pdw_errors (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保留所有的要求或查詢執行過程中遇到的錯誤相關資訊。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|error_id|**nvarchar(36)**|此檢視的索引鍵。<br /><br /> 與錯誤相關聯的唯一數值識別碼。|唯一的系統中的所有查詢錯誤。|  
|來源|**nvarchar(64)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|型別|**nvarchar(4000)**|發生的錯誤類型。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|create_time|**datetime**|發生錯誤的時間。|小於或等於目前的時間。|  
|pwd_node_id|**int**|相關，如果有任何特定節點的識別碼。 如需有關節點識別碼的詳細資訊，請參閱[sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。||  
|session_id|**nvarchar(32)**|相關，如果有任何工作階段識別項。 如需有關工作階段識別碼的詳細資訊，請參閱[sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。||  
|request_id|**nvarchar(32)**|相關，如果有任何要求的識別碼。 如需有關要求識別碼的詳細資訊，請參閱[sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。||  
|spid|**int**|相關，如果有任何 SQL Server 工作階段的 spid。||  
|thread_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|詳細資料|**nvarchar(4000)**|保存完整的錯誤文字描述。||  
  
 這份檢視所保留的最大資料列的相關資訊，請參閱中的系統檢視的最大值 」 一節[最小和最大值 (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9)主題。  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
