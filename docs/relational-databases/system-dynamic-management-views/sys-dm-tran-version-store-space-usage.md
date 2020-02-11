---
title: sys.databases dm_tran_version_store_space_usage （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: savjani
ms.author: pariks
manager: ajayj
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2a4fac732f784a401206f37fb2af9d3d8e0688ba
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68262656"
---
# <a name="sysdm_tran_version_store_space_usage-transact-sql"></a>sys.databases dm_tran_version_store_space_usage （Transact-sql）
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

傳回資料表，其中顯示每個資料庫的版本存放區記錄所使用的 tempdb 中的總空間。 **dm_tran_version_store_space_usage**效率較高，而且執行成本不高，因為它不會流覽個別的版本存放區記錄，而且會傳回每個資料庫的 tempdb 中所耗用的匯總版本存放區空間。
  
每個已建立版本的記錄都會儲存為二進位資料，以及一些追蹤或狀態資訊。 與資料庫資料表中的記錄類似，版本存放區記錄也是儲存在 8192 位元組的頁面中。 如果記錄超出 8192 位元組，該記錄便會分割成兩個不同的記錄。  
  
因為版本控制記錄是以二進位儲存，所以不同資料庫的不同定序不會造成問題。 使用**dm_tran_version_store_space_usage** ，根據 SQL Server 實例中資料庫的版本存放區空間使用量，來監視和規劃 tempdb 大小。
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|資料庫的資料庫識別碼。|  
|**reserved_page_count**|**Bigint**|資料庫的版本存放區記錄之 tempdb 中保留的總頁數。|  
|**reserved_space_kb**|**Bigint**|資料庫的版本存放區記錄在 tempdb 中使用的總空間（以 kb 為單位）。|  
  
## <a name="permissions"></a>權限  
在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]上， `VIEW SERVER STATE`需要許可權。   

## <a name="examples"></a>範例  
下列查詢可用來根據[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例中每個資料庫的版本存放區，來判斷 tempdb 中所耗用的空間。 
  
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
  
