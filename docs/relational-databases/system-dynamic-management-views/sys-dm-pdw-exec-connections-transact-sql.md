---
title: sys.databases dm_pdw_exec_connections （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2625466b-d0ef-4c71-bedc-6d13491a8351
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: b333af29e3d39c0f4ce59ea68602f652c042003f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67899422"
---
# <a name="sysdm_pdw_exec_connections-transact-sql"></a>sys.databases dm_pdw_exec_connections （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  傳回有關與這個 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 執行個體建立之連接及每一個連接之詳細資料的資訊。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|session_id|**int**|識別這項連接的相關工作階段。 `session_id`使用`SESSION_ID()`傳回目前連接的。|  
|connect_time|**datetime**|建立連接的時間戳記。 不可為 Null。|  
|encrypt_option|**nvarchar(40)**|表示 TRUE （連接已加密）或 FALSE （連接未 enctypred）。|  
|auth_scheme|**nvarchar(40)**|指定搭配這個連接使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Windows 驗證配置。 不可為 Null。|  
|client_id|**varchar(48)**|連接到這部伺服器之用戶端的 IP 位址。 可為 Null。|  
|sql_spid|**int**|連接的伺服器處理序識別碼。 `sql_spid`使用`@@SPID`傳回目前連接的。對於大部分的制定目的，請`session_id`改用。|  
  
## <a name="permissions"></a>權限  
 需要伺服器的**VIEW SERVER STATE**許可權。  
  
## <a name="relationship-cardinalities"></a>關聯性基數  
  
||||  
|-|-|-|  
|dm_pdw_exec_sessions。 session_id|dm_pdw_exec_connections。 session_id|一對一|  
|dm_pdw_exec_requests。 connection_id|dm_pdw_exec_connections。 connection_id|多對一|  
  
## <a name="examples-sssdwfull-and-sspdw"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
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
 [SQL 資料倉儲和平行處理資料倉儲動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  

