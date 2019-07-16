---
title: sys.dm_db_missing_index_columns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_missing_index_columns_TSQL
- sys.dm_db_missing_index_columns_TSQL
- sys.dm_db_missing_index_columns
- dm_db_missing_index_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_missing_index_columns dynamic management function
- missing indexes feature [SQL Server], sys.dm_db_missing_index_columns dynamic management function
ms.assetid: 3b24e5ed-0c79-47e5-805c-a0902d0aeb86
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 38d21e20ec158ea316caf6acd17f7225c8d3a49d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002657"
---
# <a name="sysdmdbmissingindexcolumns-transact-sql"></a>sys.dm_db_missing_index_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回有關遺漏索引 (不包括空間索引) 之資料庫表格資料行的資訊。 **sys.dm_db_missing_index_columns**是動態管理函數。  

## <a name="syntax"></a>語法  
  
```  
  
sys.dm_db_missing_index_columns(index_handle)  
```  
  
## <a name="arguments"></a>引數  
 *index_handle*  
 唯一識別遺漏索引的整數。 您可以從下列動態管理物件中取得：  
  
 [sys.dm_db_missing_index_details &#40;-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)  
  
 [sys.dm_db_missing_index_groups &#40;-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**column_id**|**int**|資料行的識別碼。|  
|**column_name**|**sysname**|資料表資料行的名稱。|  
|**column_usage**|**varchar(20)**|查詢使用資料行的方式。 可能的值和其描述如下：<br /><br /> 等號比較：表示表單的等號比較述詞作為資料行： <br />                        *table.column* = *constant_value*<br /><br /> 不等比較：作為述詞的表示是否不相等，比方說，形式的述詞的資料行： *table.column* > *constant_value*。 "=" 以外的其他任何比較運算子都可表示不相等。<br /><br /> 包括：資料行不會用來評估述詞，但用於另一個原因，比方說，來涵蓋查詢。|  
  
## <a name="remarks"></a>備註  
 所傳回的資訊**sys.dm_db_missing_index_columns**會更新查詢最佳化，查詢最佳化工具，而不會保存。 遺漏索引資訊只會保留到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新啟動為止。 如果資料庫管理員想要在伺服器回收之後保留遺漏索引資訊，應該定期製作該項資訊的備份副本。  
  
## <a name="transaction-consistency"></a>交易一致性  
 如果交易建立或卸除資料表，便會從這個動態管理物件中移除包含有關已卸除物件之遺漏索引資訊的資料列，以維持交易的一致性。  
  
## <a name="permissions"></a>Permissions  
 使用者必須取得 VIEW SERVER STATE 權限或隱含 VIEW SERVER STATE 權限的任何權限，才能查詢此動態管理函數。  
  
## <a name="examples"></a>範例  
 下列範例會對 `Address` 資料表執行查詢，然後使用 `sys.dm_db_missing_index_columns` 動態管理檢視執行查詢，傳回遺漏索引的資料表資料行。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT City, StateProvinceID, PostalCode  
FROM Person.Address  
WHERE StateProvinceID = 9;  
GO  
SELECT mig.*, statement AS table_name,  
    column_id, column_name, column_usage  
FROM sys.dm_db_missing_index_details AS mid  
CROSS APPLY sys.dm_db_missing_index_columns (mid.index_handle)  
INNER JOIN sys.dm_db_missing_index_groups AS mig ON mig.index_handle = mid.index_handle  
ORDER BY mig.index_group_handle, mig.index_handle, column_id;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_db_missing_index_details &#40;-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sys.dm_db_missing_index_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [sys.dm_db_missing_index_group_stats &#40;-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
  
  
