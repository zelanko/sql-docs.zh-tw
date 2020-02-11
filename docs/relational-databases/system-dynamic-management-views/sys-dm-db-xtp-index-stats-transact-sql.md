---
title: sys.databases dm_db_xtp_index_stats （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6e6370f4cbfcbc38478e562c3b74ff24ffde962f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68026829"
---
# <a name="sysdm_db_xtp_index_stats-transact-sql"></a>sys.dm_db_xtp_index_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  包含上次重新啟動資料庫之後收集的統計資料。  
  
 如需詳細資訊，請參閱記憶體內部[&#40;記憶體優化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)和在[記憶體優化資料表上使用索引的指導方針](https://msdn.microsoft.com/library/16ef63a4-367a-46ac-917d-9eebc81ab29b)。  

  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|object_id|**Bigint**|這個索引所屬物件的識別碼。|  
|xtp_object_id|**Bigint**|對應至目前物件版本的內部識別碼。<br /><br /> 注意：適用于[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。|  
|index_id|**Bigint**|索引的識別碼。 index_id 只在物件內才是唯一的。|  
|scans_started|**Bigint**|已執行之記憶體中 OLTP 索引掃描的數目。 每個選取、插入、更新或刪除都需要索引掃描。|  
|scans_retries|**Bigint**|必須重試的索引掃描數目。|  
|rows_returned|**Bigint**|建立資料表或啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之後傳回的資料列累計數目。|  
|rows_touched|**Bigint**|建立資料表或啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之後存取的資料列累計數目。|  
|rows_expiring|**Bigint**|僅供內部使用。|  
|rows_expired|**Bigint**|僅供內部使用。|  
|rows_expired_removed|**Bigint**|僅供內部使用。|  
|phantom_scans_started|**Bigint**|僅供內部使用。|  
|phatom_scans_retries|**Bigint**|僅供內部使用。|  
|phantom_rows_touched|**Bigint**|僅供內部使用。|  
|phantom_expiring_rows_encountered|**Bigint**|僅供內部使用。|  
|phantom_expired_rows_encountered|**Bigint**|僅供內部使用。|  
|phantom_expired_removed_rows_encountered|**Bigint**|僅供內部使用。|  
|phantom_expired_rows_removed|**Bigint**|僅供內部使用。|  
|object_address|**varbinary(8)**|僅供內部使用。|  
  
## <a name="permissions"></a>權限  
 需要目前資料庫的 VIEW DATABASE STATE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的記憶體優化資料表動態管理檢視](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
