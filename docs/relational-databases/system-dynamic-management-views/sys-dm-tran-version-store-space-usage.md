---
title: sys.dm_tran_version_store_space_usage (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_version_store_space_usage_TSQL
- sys.dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_version_store_space_usage dynamic management view
ms.assetid: 7ab44517-0351-4f91-bdd9-7cf940f03c51
caps.latest.revision: 10
author: savjani
ms.author: pariks
manager: ajayj
ms.workload: Inactive
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 1459dd2b98ed9579bc1939c60c1e74e14157d0b6
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="sysdmtranversionstorespaceusage-transact-sql"></a>sys.dm_tran_version_store_space_usage (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

傳回資料表，以顯示在 tempdb 版本存放區記錄所使用的每個資料庫中的總空間。 **sys.dm_tran_version_store_space_usage**是有效率且不耗費資源，若要執行，它不會不瀏覽個別的版本存放區記錄，並傳回彙總每個資料庫 tempdb 中取用的版本存放區空間。
  
每個版本控制記錄會儲存為二進位資料，連同一些追蹤或狀態資訊。 與資料庫資料表中的記錄類似，版本存放區記錄也是儲存在 8192 位元組的頁面中。 如果記錄超出 8192 位元組，該記錄便會分割成兩個不同的記錄。  
  
因為版本控制記錄是以二進位儲存，所以不同資料庫的不同定序不會造成問題。 使用**sys.dm_tran_version_store_space_usage**根據 SQL Server 執行個體中的資料庫版本存放區空間使用量的監視和規劃的 tempdb 大小。
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|資料庫的資料庫識別碼。|  
|**reserved_page_count**|**bigint**|Tempdb 的版本中保留的頁面的總計數存放區資料庫的記錄。|  
|**reserved_space_kb**|**bigint**|版本在 tempdb （kb） 所使用的總空間存放區資料庫的記錄。|  
  
## <a name="permissions"></a>Permissions  
在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   

## <a name="examples"></a>範例  
下列查詢可判斷在 tempdb 中，使用的空間供版本存放區中每個資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。 
  
```sql  
SELECT 
  DB_NAME(database_id) as 'Database Name',
  reserved_page_count,
  reserved_space_kb 
FROM sys.dm_tran_version_store_space_usage;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Database Name            reserved_page_count reserved_space_kb  
------------------------ -------------------- -----------  
msdb                      0                    0             
AdventureWorks2016        10                   80             
AdventureWorks2016DW      0                    0             
WideWorldImporters        20                   160             
```
 
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [交易相關的動態管理檢視和函數 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
