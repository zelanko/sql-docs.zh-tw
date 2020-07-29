---
title: OBJECT_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OBJECT_ID
- OBJECT_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], IDs
- identification numbers [SQL Server], database objects
- checking object exists
- IDs [SQL Server], database objects
- OBJECT_ID function
- database objects [SQL Server], IDs
- displaying object IDs
- viewing object IDs
- verifying object exists
ms.assetid: f89286db-440f-4218-a828-30881ce3077a
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f2ae4289776787d2e91b3c9c911629b38ced975d
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87112678"
---
# <a name="object_id-transact-sql"></a>OBJECT_ID (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  傳回結構描述範圍的物件之資料庫物件識別碼。  
  
> [!IMPORTANT]  
>  範圍不是結構描述的物件 (例如 DDL 觸發程序) 無法利用 OBJECT_ID 進行查詢。 如果是在 [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) 目錄檢視中找不到的物件，請查詢適當的目錄檢視來取得物件識別碼。 例如，若要傳回 DDL 觸發程序的物件識別碼，請使用 `SELECT OBJECT_ID FROM sys.triggers WHERE name = 'DatabaseTriggerLog``'`。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
OBJECT_ID ( '[ database_name . [ schema_name ] . | schema_name . ]   
  object_name' [ ,'object_type' ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 **'** *object_name* **'**  
 這是要使用的物件。 *object_name* 是 **varchar** 或 **nvarchar**。 如果 *object_name* 是 **varchar**，則會隱含地轉換成 **nvarchar**。 資料庫和結構描述名稱的指定是選擇性的。  
  
 **'** *object_type* **'**  
 這是結構描述範圍物件類型。 *object_type* 是 **varchar** 或 **nvarchar**。 如果 *object_type* 是 **varchar**，則會隱含地轉換成 **nvarchar**。 如需物件類型清單，請參閱 **sys.objects &#40;Transact-SQL&#41;** 中的[類型](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)資料行。  
  
## <a name="return-types"></a>傳回型別  
 **int**  
  
## <a name="exceptions"></a>例外狀況  
 若為空間索引，OBJECT_ID 會傳回 NULL。  
  
 發生錯誤時傳回 NULL。  
  
 使用者只能檢視使用者擁有或被授與某些權限之安全性實體的中繼資料。 這表示發出中繼資料的內建函數 (例如，OBJECT_ID) 會在使用者不具有該物件任何權限時傳回 NULL。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="remarks"></a>備註  
 當系統函數的參數是選擇性時，就會假設使用目前資料庫、主機電腦、伺服器使用者或資料庫使用者。 內建函數後面一律必須接著括號。  
  
 當指定暫存資料表名稱時，除非目前資料庫是 **tempdb**，否則，資料庫名稱必須在暫存資料表名稱前面。 例如： `SELECT OBJECT_ID('tempdb..#mytemptable')` 。  
  
 系統函數可以用於選取清單、WHERE 子句以及任何可以使用運算式的位置。 如需詳細資訊，請參閱[運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md) 及 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-the-object-id-for-a-specified-object"></a>A. 傳回指定物件的物件識別碼  
 下列範例會傳回 `Production.WorkOrder`資料庫之 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料表的物件識別碼。  
  
```  
USE master;  
GO  
SELECT OBJECT_ID(N'AdventureWorks2012.Production.WorkOrder') AS 'Object ID';  
GO  
```  
  
### <a name="b-verifying-that-an-object-exists"></a>B. 確認物件存在  
 下列範例會確認資料表有物件識別碼，來檢查指定的資料表是否存在。 如果資料表存在，就會刪除它。 如果資料表不存在，就不會執行 `DROP TABLE` 陳述式。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'dbo.AWBuildVersion', N'U') IS NOT NULL  
DROP TABLE dbo.AWBuildVersion;  
GO  
```  
  
### <a name="c-using-object_id-to-specify-the-value-of-a-system-function-parameter"></a>C. 使用 OBJECT_ID 來指定系統函數參數的值  
 下列範例使用 `Person.Address`sys.dm_db_index_operational_stats[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 函數，來傳回 [ 資料庫中 ](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md) 資料表之所有索引和資料分割的資訊。  
  
> [!IMPORTANT]  
>  當您使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數 DB_ID 和 OBJECT_ID 傳回參數值時，請務必確定所傳回的是有效的識別碼。 如果找不到資料庫或物件名稱 (例如，因為不存在或是拼錯了)，這兩個函數都會傳回 NULL。 **sys.dm_db_index_operational_stats** 函數會將 NULL 解譯為指定所有資料庫或物件的萬用字元值。 由於這不見得是刻意安排的作業，因此本節所舉的範例，只會示範決定資料庫和物件識別碼的安全方法。  
  
```  
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
  
### <a name="d-returning-the-object-id-for-a-specified-object"></a>D：傳回指定物件的物件識別碼  
 下列範例會傳回 `FactFinance`資料庫之 [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] 資料表的物件識別碼。  
  
```  
SELECT OBJECT_ID('AdventureWorksPDW2012.dbo.FactFinance') AS 'Object ID';  
```  
  
## <a name="see-also"></a>另請參閱  
 [中繼資料函數 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [OBJECT_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/object-name-transact-sql.md)  
  
  

