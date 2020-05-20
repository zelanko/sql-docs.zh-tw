---
title: DB_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/13/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DB_ID_TSQL
- DB_ID
dev_langs:
- TSQL
helpviewer_keywords:
- viewing database ID numbers
- IDs [SQL Server], databases
- database IDs [SQL Server]
- identification numbers [SQL Server], databases
- displaying database ID numbers
- DB_ID function
ms.assetid: 7b3aef89-a6fd-4144-b468-bf87ebf381b8
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d9908d99f81094b8b8d3c2afd5c82ad870c2de22
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68995744"
---
# <a name="db_id-transact-sql"></a>DB_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

此函式會傳回指定資料庫的資料庫識別碼 (ID)。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DB_ID ( [ 'database_name' ] )   
```  
  
## <a name="arguments"></a>引數  
'*database_name*'  
`DB_ID` 會傳回其資料庫識別碼的資料庫名稱。 如果 `DB_ID` 呼叫省略 *database_name*，`DB_ID` 會傳回目前資料庫的識別碼。
  
## <a name="return-types"></a>傳回類型
**int**

## <a name="remarks"></a>備註
`DB_ID` 只能用來傳回 Azure SQL Database 中目前資料庫的資料庫識別碼。 如果指定的資料庫名稱不是目前資料庫的名稱，就會傳回 NULL。

> [!NOTE]
> 與 Azure SQL Database 搭配使用時，`DB_ID` 可能不會傳回與從 **sys.databases** 查詢 `database_id` 相同的結果。 如果 `DB_ID` 的呼叫者與其他 **sys** 檢視比較結果，則應該改為查詢 **sys.databases**。
  
## <a name="permissions"></a>權限  
如果 `DB_ID` 的呼叫端未擁有特定非 **master** 或非 **tempdb** 資料庫，至少需要 `ALTER ANY DATABASE` 或 `VIEW ANY DATABASE` 伺服器層級權限才能查看對應的 `DB_ID` 資料列。 針對 **master** 資料庫，`DB_ID` 至少需要 `CREATE DATABASE` 權限。 呼叫端所連線的資料庫一律會出現在 **sys.databases** 中。
  
> [!IMPORTANT]  
>  根據預設，公用角色具備 `VIEW ANY DATABASE` 權限，允許所有登入查看資料庫資訊。 若要防止登入偵測資料庫，請 `REVOKE` 公用 `VIEW ANY DATABASE` 權限，或 `DENY` 個別登入的 `VIEW ANY DATABASE` 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-the-database-id-of-the-current-database"></a>A. 傳回目前資料庫的資料庫識別碼  
此範例會傳回目前資料庫的資料庫識別碼。
  
```sql
SELECT DB_ID() AS [Database ID];  
GO  
```  
  
### <a name="b-returning-the-database-id-of-a-specified-database"></a>B. 傳回指定資料庫的資料庫識別碼  
此範例會傳回 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的資料庫識別碼。
  
```sql
SELECT DB_ID(N'AdventureWorks2008R2') AS [Database ID];  
GO  
```  
  
### <a name="c-using-db_id-to-specify-the-value-of-a-system-function-parameter"></a>C. 使用 DB_ID 來指定系統函數參數的值  
此範例會使用 `DB_ID` 來傳回系統函式 `sys.dm_db_index_operational_stats` 中 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的資料庫識別碼。 該函數是以資料庫識別碼作為第一個參數。
  
```sql
DECLARE @db_id int;  
DECLARE @object_id int;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.Person.Address');  
IF @db_id IS NULL   
  BEGIN;  
    PRINT N'Invalid database';  
  END;  
ELSE IF @object_id IS NULL  
  BEGIN;  
    PRINT N'Invalid object';  
  END;  
ELSE  
  BEGIN;  
    SELECT * FROM sys.dm_db_index_operational_stats(@db_id, @object_id, NULL, NULL);  
  END;  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-return-the-id-of-the-current-database"></a>D. 傳回目前資料庫的識別碼  
此範例會傳回目前資料庫的資料庫識別碼。
  
```sql
SELECT DB_ID();  
```  
  
### <a name="e-return-the-id-of-a-named-database"></a>E. 傳回具名資料庫的識別碼。  
此範例會傳回 AdventureWorksDW2012 資料庫的資料庫識別碼。
  
```sql
SELECT DB_ID('AdventureWorksPDW2012');  
```  
  
## <a name="see-also"></a>另請參閱
[DB_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)  
[中繼資料函式 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
[sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)
  
  

