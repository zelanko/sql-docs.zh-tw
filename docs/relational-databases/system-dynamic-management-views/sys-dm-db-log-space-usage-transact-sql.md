---
description: 'sys. dm_db_log_space_usage (Transact-sql) '
title: sys. dm_db_log_space_usage (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a250e6b6cb322e2cda9f63304779ebc9609a6bb6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89518896"
---
# <a name="sysdm_db_log_space_usage-transact-sql"></a>sys. dm_db_log_space_usage (Transact-sql) 
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

傳回交易記錄檔的空間使用量資訊。 
  
> [!NOTE]
> 所有交易記錄檔都會合並。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|database_id|**smallint**|資料庫識別碼。|  
|total_log_size_in_bytes |**bigint** |記錄檔的大小  |
|used_log_space_in_bytes |**bigint** |記錄檔的佔用大小  |     
|used_log_space_in_percent |**real** |記錄檔大小總計占百分比的記錄檔大小 |
|log_space_in_bytes_since_last_backup |**bigint** |自上次記錄備份之後使用的空間量 <br />**適用于：** [!INCLUDE[sssql14-md](../../includes/sssql14-md.md)] 到 [!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)] 、  [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 。|
    
  
## <a name="permissions"></a>權限  

在上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，需要 `VIEW SERVER STATE` 許可權。   
在進階層中 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] ，需要 `VIEW DATABASE STATE` 資料庫中的許可權。 在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 標準和基本層中，需要  **伺服器管理員** 或 **Azure Active Directory 系統管理員** 帳戶。   
  
## <a name="examples"></a>範例  
  
### <a name="a-determine-the-amount-of-free-log-space-in-tempdb"></a>A. 判斷 tempdb 中的可用記錄檔空間量   
下列查詢會傳回 tempdb 中可用的總可用記錄空間（以 mb 為單位） (MB) 。

```sql
USE tempdb;  
GO  

SELECT (total_log_size_in_bytes - used_log_space_in_bytes)*1.0/1024/1024 AS [free log space in MB]  
FROM sys.dm_db_log_space_usage;  
```
  
## <a name="see-also"></a>另請參閱  
[動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[資料庫相關的動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys. dm_db_file_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)    
[sys. dm_db_task_space_usage &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)   
[sys.dm_db_session_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)  
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
[sys.dm_db_log_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md) 



