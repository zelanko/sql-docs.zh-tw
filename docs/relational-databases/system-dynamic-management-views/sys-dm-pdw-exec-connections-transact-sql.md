---
title: sys.dm_pdw_exec_connections (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2625466b-d0ef-4c71-bedc-6d13491a8351
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 008c820955ba45e4b73a0705a2aa06f5bc9986af
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmpdwexecconnections-transact-sql"></a>sys.dm_pdw_exec_connections (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  傳回有關與這個 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 執行個體建立之連接及每一個連接之詳細資料的資訊。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|session_id|**int**|識別這項連接的相關工作階段。 使用`SESSION_ID()`傳回`session_id`目前連接。|  
|connect_time|**datetime**|建立連接的時間戳記。 不可為 Null。|  
|encrypt_option|**nvarchar(40)**|表示 TRUE （連接已加密） 或 FALSE （連線不 enctypred）。|  
|auth_scheme|**nvarchar(40)**|指定搭配這個連接使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Windows 驗證配置。 不可為 Null。|  
|client_id|**varchar(48)**|連接到這部伺服器的用戶端的 IP 位址。 可為 Null。|  
|sql_spid|**int**|連接的伺服器處理序識別碼。 使用`@@SPID`傳回`sql_spid`目前連接。使用最 pki，`session_id`改為。|  
  
## <a name="permissions"></a>Permissions  
 需要**VIEW SERVER STATE**伺服器的權限。  
  
## <a name="relationship-cardinalities"></a>關聯性基數  
  
||||  
|-|-|-|  
|dm_pdw_exec_sessions.session_id|dm_pdw_exec_connections.session_id|一對一|  
|dm_pdw_exec_requests.connection_id|dm_pdw_exec_connections.connection_id|多對一|  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 收集查詢自有連接相關資訊的典型查詢。  
  
```  
SELECT  
    c.session_id, c.encrypt_option,  
    c.auth_scheme, s.client_id, s.login_name,   
    s.status, s.query_count  
FROM sys.dm_pdw_exec_connections AS c  
JOIN sys.dm_pdw_exec_sessions AS s  
    ON c.session_id = s.session_id  
WHERE c.session_id = SESSION_ID();  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  

