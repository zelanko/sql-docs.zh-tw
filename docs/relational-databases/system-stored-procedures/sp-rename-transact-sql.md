---
description: sp_rename (Transact-SQL)
title: sp_rename (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/14/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_rename_TSQL
- sp_rename
dev_langs:
- TSQL
helpviewer_keywords:
- renaming indexes
- renaming columns
- sp_rename
- renaming tables
ms.assetid: bc3548f0-143f-404e-a2e9-0a15960fc8ed
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=azure-sqldw-latest
ms.openlocfilehash: c180d679075076168d3be510c22d0775ebc7af30
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478899"
---
# <a name="sp_rename-transact-sql"></a>sp_rename (Transact-SQL)
[!INCLUDE [sql-asdb-asa](../../includes/applies-to-version/sql-asdb-asa.md)]

  變更目前資料庫中之使用者建立物件的名稱。 這個物件可以是資料表、索引、資料行、別名資料類型或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] common language RUNTIME (CLR) 使用者定義型別。  
  
> [!NOTE]
> 在中 [!INCLUDE[ssazuresynapse](../../includes/ssazuresynapse_md.md)] ，sp_rename 處於 **預覽** 狀態，只能用來重新命名使用者物件中的資料行。

> [!CAUTION]  
>  變更物件名稱的任何部分，可能破壞指令碼和預存程序。 我們建議您不要使用陳述式來重新命名預存程序、觸發程序、使用者定義函數或檢視；相反地，請卸除物件，再利用新名稱來重新建立它。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
-- Transact-SQL Syntax for sp_rename in SQL Server and Azure SQL Database
sp_rename [ @objname = ] 'object_name' , [ @newname = ] 'new_name'   
    [ , [ @objtype = ] 'object_type' ]   
```  

```sql  
-- Transact-SQL Syntax for sp_rename (preview) in Azure Synapse Analytics
sp_rename [ @objname = ] 'object_name' , [ @newname = ] 'new_name'   
    , [ @objtype = ] 'COLUMN'   
``` 
  
## <a name="arguments"></a>引數  
 [ @objname =] '*object_name*'  
 這是使用者物件或資料類型目前的完整或非完整名稱。 如果要重新命名的物件是資料表中的資料行， *object_name* 必須在 table 或 *schema*.*資料行中*。 如果要重新命名的物件是索引， *object_name* 必須在 table 或 *schema* 格式的 *資料表* 中。 如果要重新命名的物件是條件約束， *object_name* 必須是 *schema 格式。*  
  
 只有在指定限定物件時，才需要引號。 如果提供其中包括資料庫名稱的完整名稱，資料庫名稱就必須是目前資料庫的名稱。 *object_name* 是 **Nvarchar (776)**，沒有預設值。  
  
 [ @newname =] '*new_name*'  
 這是指定物件的新名稱。 *new_name* 必須是一個部分的名稱，且必須遵照識別碼的規則。 *newname* 是 **sysname**，沒有預設值。  
  
> [!NOTE]  
>  觸發程序名稱的開頭不能是 # 或 ##。  
  
 [ @objtype =] '*object_type*'  
 這是要重新命名的物件類型。 *object_type* 是 **Varchar (13)**，預設值是 Null，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|COLUMN|要重新命名的資料行。|  
|DATABASE|使用者定義資料庫。 當重新命名資料庫時，需要這個物件類型。|  
|INDEX|使用者自訂索引。 重新命名具有統計資料的索引時，也會自動重新命名統計資料。|  
|OBJECT|[Sys. 物件](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)中所追蹤之類型的專案。 例如，您可以利用 OBJECT 來重新命名物件，其中包括條件約束 (CHECK、FOREIGN KEY、PRIMARY/UNIQUE KEY)、使用者資料表和規則。|  
|STATISTICS|**適用於**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。<br /><br /> 使用者明確建立的統計資料，或使用索引隱含建立的統計資料。 重新命名索引的統計資料時，也會自動重新命名索引。|  
|USERDATATYPE|藉由執行[CREATE TYPE](../../t-sql/statements/create-type-transact-sql.md)或[Sp_addtype](../../relational-databases/system-stored-procedures/sp-addtype-transact-sql.md)加入的[CLR 使用者自訂類型](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)。|  
  
[ @objtype =] '*COLUMN*' **適用** 于： Azure Synapse Analytics  
在 sp_rename 的 (preview) 中 [!INCLUDE[ssazuresynapse](../../includes/ssazuresynapse_md.md)] ，資料 *行* 是必要參數，指定要重新命名的物件類型是資料行。 它是 **Varchar (13)** 沒有預設值，而且必須一律包含在 sp_rename (preview) 語句中。 只有當資料行是非散發資料行時，才能重新命名資料行。

## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或非零數字 (失敗)  
  
## <a name="remarks"></a>備註  
**適用** 于SQL Server (所有支援的版本) 和 Azure SQL Database  
 每當重新命名 PRIMARY KEY 或 UNIQUE 條件約束時，sp_rename 都會自動重新命名相關聯的索引。 如果是重新命名的索引繫結於 PRIMARY KEY 條件約束，sp_rename 也會自動重新命名 PRIMARY KEY 條件約束。  

**適用** 于SQL Server (所有支援的版本) 和 Azure SQL Database  
 您可以利用 sp_rename 來重新命名主要和次要 XML 索引。  
  
**適用** 于SQL Server (所有支援的版本) 和 Azure SQL Database  
 重新命名預存程式、函數、視圖或觸發程式，不會在 [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) 目錄檢視的定義資料行中變更對應物件的名稱，也不會變更使用 [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md) 內建函數所取得的名稱。 因此，我們建議您不要利用 sp_rename 來重新命名這些物件類型。 相反地，請卸除物件，再利用它的新名稱來重新建立物件。  

**適用** 于SQL Server (所有支援的版本) 、Azure SQL Database 和 Azure Synapse Analytics  
 重新命名資料表或資料行之類的物件，不會自動重新命名指向這個物件的參考。 您必須手動修改任何參考重新命名之物件的物件。 例如，如果您重新命名資料表資料行，且有觸發程序參考這個資料行，您必須修改觸發程序來反映新的資料行名稱。 在重新命名物件之前，請利用 [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) 來列出其相依性。  

**適用** 于SQL Server (所有支援的版本) 、Azure SQL Database 和 Azure Synapse Analytics  
 您只能變更目前資料庫中的物件或資料類型的名稱。 您無法改變大部分系統資料類型和系統物件的名稱。  
  
## <a name="permissions"></a>權限  
 若要重新命名物件、資料行和索引，需要物件的 ALTER 權限。 若要重新命名使用者類型，需要這個類型的 CONTROL 權限。 若要重新命名資料庫，需要系統管理員 (sysadmin) 或資料庫建立者 (dbcreator) 固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
  
### <a name="a-renaming-a-table"></a>A. 重新命名資料表  
 下列範例會將 `SalesTerritory` 資料表重新命名為 `SalesTerr` 結構描述中的 `Sales` 。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_rename 'Sales.SalesTerritory', 'SalesTerr';  
GO  
```  
  
### <a name="b-renaming-a-column"></a>B. 重新命名資料行  
 下列範例會將資料表中的資料行重新命名 `TerritoryID` `SalesTerritory` 為 `TerrID` 。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_rename 'Sales.SalesTerritory.TerritoryID', 'TerrID', 'COLUMN';  
GO  
```  
  
### <a name="c-renaming-an-index"></a>C. 重新命名索引  
 下列範例會將 `IX_ProductVendor_VendorID` 索引重新命名成 `IX_VendorID`。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_rename N'Purchasing.ProductVendor.IX_ProductVendor_VendorID', N'IX_VendorID', N'INDEX';  
GO  
```  
  
### <a name="d-renaming-an-alias-data-type"></a>D. 重新命名別名資料類型  
 下列範例會將 `Phone` 別名資料類型重新命名成 `Telephone`。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_rename N'Phone', N'Telephone', N'USERDATATYPE';  
GO  
```  
  
### <a name="e-renaming-constraints"></a>E. 重新命名條件約束  
 下列範例會重新命名 PRIMARY KEY 條件約束、CHECK 條件約束和 FOREIGN KEY 條件約束。 重新命名條件約束時，您必須指定條件約束所屬的結構描述。  
  
```sql  
USE AdventureWorks2012;   
GO  
-- Return the current Primary Key, Foreign Key and Check constraints for the Employee table.  
SELECT name, SCHEMA_NAME(schema_id) AS schema_name, type_desc  
FROM sys.objects  
WHERE parent_object_id = (OBJECT_ID('HumanResources.Employee'))   
AND type IN ('C','F', 'PK');   
GO  
  
-- Rename the primary key constraint.  
sp_rename 'HumanResources.PK_Employee_BusinessEntityID', 'PK_EmployeeID';  
GO  
  
-- Rename a check constraint.  
sp_rename 'HumanResources.CK_Employee_BirthDate', 'CK_BirthDate';  
GO  
  
-- Rename a foreign key constraint.  
sp_rename 'HumanResources.FK_Employee_Person_BusinessEntityID', 'FK_EmployeeID';  
  
-- Return the current Primary Key, Foreign Key and Check constraints for the Employee table.  
SELECT name, SCHEMA_NAME(schema_id) AS schema_name, type_desc  
FROM sys.objects  
WHERE parent_object_id = (OBJECT_ID('HumanResources.Employee'))   
AND type IN ('C','F', 'PK');  
  
```  
  
```  
  
name                                  schema_name        type_desc  
------------------------------------- ------------------ ----------------------  
FK_Employee_Person_BusinessEntityID   HumanResources     FOREIGN_KEY_CONSTRAINT  
PK_Employee_BusinessEntityID          HumanResources     PRIMARY_KEY_CONSTRAINT  
CK_Employee_BirthDate                 HumanResources     CHECK_CONSTRAINT  
CK_Employee_MaritalStatus             HumanResources     CHECK_CONSTRAINT  
CK_Employee_HireDate                  HumanResources     CHECK_CONSTRAINT  
CK_Employee_Gender                    HumanResources     CHECK_CONSTRAINT  
CK_Employee_VacationHours             HumanResources     CHECK_CONSTRAINT  
CK_Employee_SickLeaveHours            HumanResources     CHECK_CONSTRAINT  
  
(7 row(s) affected)  
  
name                                  schema_name        type_desc  
------------------------------------- ------------------ ----------------------  
FK_Employee_ID                        HumanResources     FOREIGN_KEY_CONSTRAINT  
PK_Employee_ID                        HumanResources     PRIMARY_KEY_CONSTRAINT  
CK_BirthDate                          HumanResources     CHECK_CONSTRAINT  
CK_Employee_MaritalStatus             HumanResources     CHECK_CONSTRAINT  
CK_Employee_HireDate                  HumanResources     CHECK_CONSTRAINT  
CK_Employee_Gender                    HumanResources     CHECK_CONSTRAINT  
CK_Employee_VacationHours             HumanResources     CHECK_CONSTRAINT  
CK_Employee_SickLeaveHours            HumanResources     CHECK_CONSTRAINT  
  
(7 row(s) affected)  
  
```  
  
### <a name="f-renaming-statistics"></a>F. 重新命名統計資料  
 下列範例會建立名為 contactMail1 的統計資料物件，然後使用 sp_rename 將統計資料重新命名為 NewContact。 當重新命名統計資料時，必須以 schema.table.statistics_name 格式指定物件。  
  
```sql  
CREATE STATISTICS ContactMail1  
    ON Person.Person (BusinessEntityID, EmailPromotion)  
    WITH SAMPLE 5 PERCENT;  
  
sp_rename 'Person.Person.ContactMail1', 'NewContact','Statistics';  
  
```  

## <a name="examples-sssdwfull"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]
### <a name="g-renaming-a-column"></a>G. 重新命名資料行  
 下列範例會將資料表中的資料行重新命名 `c1` `table1` 為 `col1` 。  
  
```sql  
CREATE TABLE table1 (c1 INT, c2 INT);
EXEC sp_rename 'table1.c1', 'col1', 'COLUMN';
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [&#40;Transact-sql&#41;的資料庫引擎預存程式 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
