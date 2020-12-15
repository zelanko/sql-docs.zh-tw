---
description: 'sys.dm_pdw_errors (Transact-sql) '
title: sys.dm_pdw_errors (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 944eac31-5691-432b-b9f5-f1e11c05191f
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: f89d6ce4c8a385906856dde4c71e97d8a6e24ad2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482580"
---
# <a name="sysdm_pdw_errors-transact-sql"></a>sys.dm_pdw_errors (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  保存執行要求或查詢期間發生之所有錯誤的相關資訊。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|error_id|**Nvarchar (36)**|此視圖的索引鍵。<br /><br /> 與錯誤相關聯的唯一數值識別碼。|在系統的所有查詢錯誤中都是唯一的。|  
|source|**Nvarchar (64)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|類型|**nvarchar(4000)**|發生的錯誤類型。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|create_time|**datetime**|發生錯誤的時間。|小於或等於目前時間。|  
|pwd_node_id|**int**|相關特定節點的識別碼（如果有的話）。 如需節點識別碼的詳細資訊，請參閱 [sys.dm_pdw_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。||  
|session_id|**nvarchar(32)**|相關會話的識別碼（如果有的話）。 如需會話識別碼的詳細資訊，請參閱  [sys.dm_pdw_exec_sessions &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。||  
|request_id|**nvarchar(32)**|牽涉到的要求識別碼（如果有的話）。 如需要求識別碼的詳細資訊，請參閱 [sys.dm_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。||  
|spid|**int**|牽涉到的 SQL Server 會話的 spid （如果有的話）。||  
|thread_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|詳細資料|**nvarchar(4000)**|保存完整的錯誤文字描述。||  
  
 如需此視圖所保留之最大資料列的相關資訊，請參閱「 [容量限制](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) 」主題中的「中繼資料」一節。  
  
## <a name="see-also"></a>另請參閱  
 [Azure Synapse Analytics 和平行處理資料倉儲動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
