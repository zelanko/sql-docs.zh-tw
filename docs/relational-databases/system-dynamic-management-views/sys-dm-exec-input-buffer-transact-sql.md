---
title: sys.dm_exec_input_buffer (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 10/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_input_buffer
- sys.dm_exec_input_buffer _tsql
- dm_exec_input_buffer
- dm_exec_input_buffer_tsql
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_input_buffer dynamic management function
ms.assetid: fb34a560-bde9-4ad9-aa96-0d4baa4fc104
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b36607c9bb20e1d2e4e4cabd0680a19640e56c7f
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="sysdmexecinputbuffer-transact-sql"></a>sys.dm_exec_input_buffer (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-2014sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2014sp2-asdb-xxxx-xxx-md.md)]

  傳回陳述式的執行個體的相關資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="syntax"></a>語法  
  
```  
sys.dm_exec_input_buffer ( session_id , request_id )
```  
  
## <a name="arguments"></a>引數  
*session_id*  
執行要查閱之批次的工作階段識別碼。 *session_id*是**smallint**。 *session_id*可以從下列動態管理物件取得：  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
-   [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)   
  
*request_id*  
從 request_id [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)。 *request_id*是**int**。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**event_type**|**nvarchar(256)**|指定的 spid 的輸入緩衝區中的事件類型。|  
|**parameters**|**smallint**|陳述式所提供的任何參數。|  
|**event_info**|**nvarchar(max)**|指定的 spid 的輸入緩衝區中的陳述式文字。|  
  
## <a name="permissions"></a>Permissions  
 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，如果使用者有 VIEW SERVER STATE 權限，使用者會看到所有執行的工作階段的執行個體上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; 否則使用者會看到目前工作階段。  
  
 在[!INCLUDE[ssSDS](../../includes/sssds-md.md)]，如果使用者是資料庫擁有者，使用者會看到所有執行的工作階段上[!INCLUDE[ssSDS](../../includes/sssds-md.md)]; 否則使用者會看到目前工作階段。  
  
## <a name="remarks"></a>備註  
 此動態管理函數可搭配 sys.dm_exec_sessions 或 sys.dm_exec_requests 供這麼做**CROSS APPLY**。  
  
## <a name="examples"></a>範例  
  
### <a name="a-simple-example"></a>A. 簡單範例  
 下列範例會示範將工作階段識別碼 (SPID) 和要求識別碼傳遞至函式。  
  
```sql  
SELECT * FROM sys.dm_exec_input_buffer (52, 0);
GO
```  
  
### <a name="b-using-cross-apply-to-additional-information"></a>B. 使用跨套用的其他資訊  
 下列範例會列出工作階段識別碼大於 50 的工作階段的輸入的緩衝區。  
  
```sql  
SELECT es.session_id, ib.event_info   
FROM sys.dm_exec_sessions AS es  
CROSS APPLY sys.dm_exec_input_buffer(es.session_id, NULL) AS ib  
WHERE es.session_id > 50;
GO
```  
  
## <a name="see-also"></a>另請參閱  
 [執行相關動態管理檢視和函數&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [DBCC INPUTBUFFER &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)  
