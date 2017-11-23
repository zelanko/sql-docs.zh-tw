---
title: "sys.dm_db_missing_index_group_stats (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_db_missing_index_group_stats_TSQL
- sys.dm_db_missing_index_group_stats
- dm_db_missing_index_group_stats_TSQL
- dm_db_missing_index_group_stats
dev_langs: TSQL
helpviewer_keywords:
- sys.dm_db_missing_index_group_stats dynamic management view
- missing indexes feature [SQL Server], sys.dm_db_missing_index_group_stats dynamic management view
ms.assetid: c2886986-9e07-44ea-a350-feeac05ee4f4
caps.latest.revision: "43"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 938f1e4d13b001899a0695c2141cbaac35a7d7bb
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdbmissingindexgroupstats-transact-sql"></a>sys.dm_db_missing_index_group_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回有關遺漏索引 (不包含空間索引) 群組的摘要資訊。  
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，動態管理檢視不可以公開可能會影響資料庫內含項目的資訊或公開有關使用者可存取之其他資料庫的資訊。 為了避免公開此資訊，包含不屬於連接租用戶之資料的每個資料列都會被篩選出來。  
    
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**group_handle**|**int**|識別一組遺漏的索引。 這個識別碼在伺服器中是唯一的。<br /><br /> 其他資料行提供有關群組中被視為遺漏之索引的所有查詢資訊。<br /><br /> 一個索引群組僅能包含一個索引。|  
|**unique_compiles**|**bigint**|由於此遺漏索引群組而獲益之編譯與重新編譯的次數。 許多不同查詢的編譯和重新編譯都可以構成這個資料行的值。|  
|**sys.dm_db_index_usage_stats**|**bigint**|群組中建議索引適用之使用者查詢所造成的搜尋次數。|  
|**user_seeks**|**bigint**|群組中建議索引適用之使用者查詢所造成的掃描次數。|  
|**last_user_seek**|**datetime**|群組中建議索引適用之使用者查詢所造成的上次搜尋日期和時間。|  
|**last_user_scan**|**datetime**|群組中建議索引適用之使用者查詢所造成的上次掃描日期和時間。|  
|**avg_total_user_cost**|**float**|可依據群組中的索引降低之使用者查詢的平均成本。|  
|**avg_user_impact**|**float**|實作此遺漏索引群組時，使用者查詢可能獲得的平均效益百分比。 這個值表示如果實作此遺漏索引群組，平均查詢成本將會依此百分比降低。|  
|**system_seeks**|**bigint**|群組中建議索引適用之系統查詢 (例如 Auto Stats 查詢) 所造成的搜尋次數。 如需詳細資訊，請參閱[Auto Stats 事件類別](../../relational-databases/event-classes/auto-stats-event-class.md)。|  
|**system_scans**|**bigint**|群組中建議索引適用之系統查詢所造成的掃描次數。|  
|**last_system_seek**|**datetime**|群組中建議索引適用之系統查詢所造成的上次系統搜尋日期和時間。|  
|**last_system_scan**|**datetime**|群組中建議索引適用之系統查詢所造成的上次系統掃描日期和時間。|  
|**avg_total_system_cost**|**float**|可依據群組中的索引降低之系統查詢的平均成本。|  
|**avg_system_impact**|**float**|實作此遺漏索引群組時，系統查詢可能獲得的平均效益百分比。 這個值表示如果實作此遺漏索引群組，平均查詢成本將會依此百分比降低。|  
  
## <a name="remarks"></a>備註  
 所傳回的資訊**sys.dm_db_missing_index_group_stats**會更新每次執行查詢，而不是依每次查詢編譯或重新編譯。 使用狀況統計資料不會一直保存，只會保留到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新啟動為止。 如果資料庫管理員想要在伺服器回收之後保留使用狀況統計資料，應該定期製作遺漏索引資訊的備份副本。  
  
## <a name="permissions"></a>Permissions  
 若要查詢此動態管理檢視，使用者必須取得 VIEW SERVER STATE 權限或隱含 VIEW SERVER STATE 權限的任何權限。  
  
## <a name="examples"></a>範例  
 下列範例說明如何使用**sys.dm_db_missing_index_group_stats**動態管理檢視。  
  
### <a name="a-find-the-10-missing-indexes-with-the-highest-anticipated-improvement-for-user-queries"></a>A. 尋找改善使用者查詢之預期效果最高的 10 個遺漏索引  
 下列查詢決定哪 10 個遺漏查詢對使用者查詢產生的預期累計改善效果最高 (以遞減順序排列)。  
  
```  
SELECT TOP 10 *  
FROM sys.dm_db_missing_index_group_stats  
ORDER BY avg_total_user_cost * avg_user_impact * (user_seeks + user_scans)DESC;  
```  
  
### <a name="b-find-the-individual-missing-indexes-and-their-column-details-for-a-particular-missing-index-group"></a>B. 尋找個別遺漏索引及其特定遺漏索引群組的資料行詳細資料  
 下列查詢決定哪些遺漏索引構成特定的遺漏索引群組，並顯示其資料行詳細資料。 為了符合這個範例的目的，遺漏索引群組控制代碼為 24。  
  
```  
SELECT migs.group_handle, mid.*  
FROM sys.dm_db_missing_index_group_stats AS migs  
INNER JOIN sys.dm_db_missing_index_groups AS mig  
    ON (migs.group_handle = mig.index_group_handle)  
INNER JOIN sys.dm_db_missing_index_details AS mid  
    ON (mig.index_handle = mid.index_handle)  
WHERE migs.group_handle = 24;  
```  
  
 此查詢提供遺漏索引之資料庫、結構描述和資料表的名稱。 它也提供索引鍵應該使用的資料行名稱。 撰寫 CREATE INDEX DDL 陳述式，以實作遺漏的索引，先列出相等資料行，然後不相等資料行中時\< *table_name*> 子句的 CREATE INDEX 陳述式。 您應該將內含資料行列在 CREATE INDEX 陳述式的 INCLUDE 子句中。 若要決定相等資料行的有效次序，請依據其選擇性排列這些資料行，將選擇性最高的資料行列在最前面 (資料行清單的最左邊)。  
  
## <a name="see-also"></a>請參閱＜  
 [sys.dm_db_missing_index_columns &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-columns-transact-sql.md)   
 [sys.dm_db_missing_index_details &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sys.dm_db_missing_index_groups &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
  
