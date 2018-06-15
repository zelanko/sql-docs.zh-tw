---
title: sys.dm_db_xtp_index_stats (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_index_stats
- dm_db_xtp_index_stats
- sys.dm_db_xtp_index_stats_TSQL
- dm_db_xtp_index_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_index_stats dynamic management view
ms.assetid: 8d0a50b8-2015-4576-930f-e3307dfc888e
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e59eeea065a0346a623d929562fc554ad842e416
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2018
ms.locfileid: "34468504"
---
# <a name="sysdmdbxtpindexstats-transact-sql"></a>sys.dm_db_xtp_index_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  包含上次重新啟動資料庫之後收集的統計資料。  
  
 如需詳細資訊，請參閱[記憶體內部 OLTP&#40;記憶體中最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)和[使用記憶體最佳化資料表的索引指導方針](http://msdn.microsoft.com/library/16ef63a4-367a-46ac-917d-9eebc81ab29b)。  

  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|object_id|**bigint**|這個索引所屬物件的識別碼。|  
|xtp_object_id|**bigint**|對應至物件的目前版本的內部識別碼。<br /><br /> 注意： 適用於[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。|  
|index_id|**bigint**|索引的識別碼。 index_id 只在物件內才是唯一的。|  
|scans_started|**bigint**|已執行之記憶體中 OLTP 索引掃描的數目。 每個選取、插入、更新或刪除都需要索引掃描。|  
|scans_retries|**bigint**|必須重試的索引掃描數目。|  
|rows_returned|**bigint**|建立資料表或啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之後傳回的資料列累計數目。|  
|rows_touched|**bigint**|建立資料表或啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之後存取的資料列累計數目。|  
|rows_expiring|**bigint**|僅供內部使用。|  
|rows_expired|**bigint**|僅供內部使用。|  
|rows_expired_removed|**bigint**|僅供內部使用。|  
|phantom_scans_started|**bigint**|僅供內部使用。|  
|phatom_scans_retries|**bigint**|僅供內部使用。|  
|phantom_rows_touched|**bigint**|僅供內部使用。|  
|phantom_expiring_rows_encountered|**bigint**|僅供內部使用。|  
|phantom_expired_rows_encountered|**bigint**|僅供內部使用。|  
|phantom_expired_removed_rows_encountered|**bigint**|僅供內部使用。|  
|phantom_expired_rows_removed|**bigint**|僅供內部使用。|  
|object_address|**varbinary(8)**|僅供內部使用。|  
  
## <a name="permissions"></a>Permissions  
 需要目前資料庫的 VIEW DATABASE STATE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體最佳化的資料表動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
