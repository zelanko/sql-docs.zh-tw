---
title: "DB_ID (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 60272ce672c0a32738b0084ea86f8907ec7fc0a5
ms.openlocfilehash: 99497c63e037054daf249ac75ef35073f102a498
ms.contentlocale: zh-tw
ms.lasthandoff: 09/06/2017

---
# <a name="dbid-transact-sql"></a>DB_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

傳回資料庫識別碼。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DB_ID ( [ 'database_name' ] )   
```  
  
## <a name="arguments"></a>引數  
'*database_name*'  
這是用來傳回對應資料庫識別碼的資料庫名稱。 *database_name*是**sysname**。 如果*database_name*已省略，則會傳回目前資料庫識別碼。
  
## <a name="return-types"></a>傳回型別
**int**
  
## <a name="permissions"></a>Permissions  
如果呼叫端的**DB_ID**不是資料庫的擁有者和資料庫不是**主要**或**tempdb**，若要查看對應的資料列所需的最小權限ALTER ANY DATABASE 或 VIEW ANY DATABASE 伺服器層級權限或在 CREATE DATABASE 權限**主要**資料庫。 呼叫端所連接的資料庫，永遠可以在 **sys.databases**中進行檢視。
  
> [!IMPORTANT]  
>  根據預設，公用角色都有 VIEW ANY DATABASE 權限，讓所有的登入，以查看資料庫資訊。 若要封鎖來自能夠偵測資料庫的登入，撤銷 VIEW ANY DATABASE 權限從公用，或拒絕個別登入的 VIEW ANY DATABASE 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-the-database-id-of-the-current-database"></a>A. 傳回目前資料庫的資料庫識別碼  
下列範例會傳回目前資料庫的資料庫識別碼。
  
```sql
SELECT DB_ID() AS [Database ID];  
GO  
```  
  
### <a name="b-returning-the-database-id-of-a-specified-database"></a>B. 傳回指定資料庫的資料庫識別碼  
下列範例會傳回資料庫識別碼[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]資料庫。
  
```sql
SELECT DB_ID(N'AdventureWorks2008R2') AS [Database ID];  
GO  
```  
  
### <a name="c-using-dbid-to-specify-the-value-of-a-system-function-parameter"></a>C. 使用 DB_ID 來指定系統函數參數的值  
下列範例會使用`DB`_`ID`要傳回的資料庫識別碼[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]系統函數中的資料庫`sys.dm_db` \_ `index` \_ `operational` \_ `stats`. 該函數是以資料庫識別碼作為第一個參數。
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-return-the-id-of-the-current-database"></a>D. 傳回目前資料庫的識別碼  
下列範例會傳回目前資料庫的資料庫識別碼。
  
```sql
SELECT DB_ID();  
```  
  
### <a name="e-return-the-id-of-a-named-database"></a>E. 傳回具名資料庫的識別碼。  
下列範例會傳回 AdventureWorksDW2012 資料庫的資料庫識別碼。
  
```sql
SELECT DB_ID('AdventureWorksPDW2012');  
```  
  
## <a name="see-also"></a>另請參閱
[DB_NAME &#40;TRANSACT-SQL &#41;](../../t-sql/functions/db-name-transact-sql.md)  
[中繼資料函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
[sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)
  
  


