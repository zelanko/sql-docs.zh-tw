---
title: sys.dm_db_log_space_usage (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sys.dm_db_log_space_usage
- sys.dm_db_log_space_usage_TSQL
- dm_db_log_space_usage
- dm_db_log_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_log_space_usage dynamic management view
ms.assetid: f6b40060-c17d-472f-b0a3-3b350275d487
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9bedbe8d5aa7b4e50ce4f486f2f3dbbf84e48a9c
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38061436"
---
# <a name="sysdmdblogspaceusage-transact-sql"></a>sys.dm_db_log_space_usage & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

傳回空間供交易記錄的使用方式資訊。 
  
> [!NOTE]
> 所有交易記錄檔會都結合。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|database_id|**smallint**|資料庫識別碼。|  
|total_log_size_in_bytes |**bigint** |記錄檔大小  |
|used_log_space_in_bytes |**bigint** |記錄檔佔用的大小  |     
|used_log_space_in_percent |**real** |以記錄檔大小總計的百分比表示的記錄檔佔用的大小 |
|log_space_in_bytes_since_last_backup |**bigint** |最後一個記錄備份之後所使用的空間量 <br />**適用於：** [!INCLUDE[sssql14-md](../../includes/sssql14-md.md)]透過[!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。|
    
  
## <a name="permissions"></a>Permissions  

在  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在  [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   
  
## <a name="examples"></a>範例  
  
### <a name="a-determine-the-amount-of-free-log-space-in-tempdb"></a>A. 判斷的可用記錄檔空間量在 tempdb 中   
下列查詢會傳回可用的總記錄空間 (mb) 可在 tempdb 中。

```sql
USE tempdb;  
GO  

SELECT (total_log_size_in_bytes - used_log_space_in_bytes)*1.0/1024/1024 AS [free log space in MB]  
FROM sys.dm_db_log_space_usage;  
```
  
## <a name="see-also"></a>另請參閱  
[動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[與資料庫相關動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_file_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)    
[sys.dm_db_task_space_usage &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)   
[sys.dm_db_session_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)  
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
[sys.dm_db_log_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md) 



