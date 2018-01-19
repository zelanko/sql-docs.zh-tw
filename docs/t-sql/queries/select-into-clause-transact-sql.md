---
title: "INTO 子句 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 05/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INTO_TSQL
- INSERT_INTO_TSQL
- INSERT INTO
- INTO
- INTO clause
- INTO_clause_TSQL
dev_langs: TSQL
helpviewer_keywords:
- copying data [SQL Server], into a new table
- INTO clause
- moving data, to a new table
- table creation [SQL Server], INTO clause
- SELECT INTO statement
- inserting rows
- clauses [SQL Server], INTO
- row additions [SQL Server], INTO clause
ms.assetid: b48d69e8-5a00-48bf-b2f3-19278a72dd88
caps.latest.revision: "63"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: da5481a06a3f1e02ea1f0e1ab3429e2d02c238d3
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="select---into-clause-transact-sql"></a>SELECT 的 INTO 子句 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  SELECT INTO 會在預設的檔案群組中建立新的資料表，然後將查詢的結果資料列插入其中。 若要檢視完整的 SELECT 語法，請參閱[SELECT &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-transact-sql.md).  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
[ INTO new_table ]
[ ON filegroup]
```  
  
## <a name="arguments"></a>引數  
 *new_table*  
 根據選取清單中的資料行以及從資料來源中選擇的資料列，指定要建立之新資料表的名稱。  
 
  *filegroup*
 
 指定將建立新的資料表檔案群組的名稱。 指定的檔案群組應該存在於其他資料庫 SQL Server 引擎會擲回錯誤。 從開始才支援這個選項[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]。
 
 格式*new_table*取決於評估選取清單中的運算式。 中的資料行*new_table* select 清單所指定的順序建立。 在每個資料行*new_table*選取清單中對應的運算式具有相同名稱、 資料類型、 null 屬性和值。 此時，系統會傳送資料行的 IDENTITY 屬性，但是＜備註＞一節中「使用識別欄位」內定義的狀況除外。  
  
 若要在相同的執行個體上的另一個資料庫中建立資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，指定*new_table*完整限定名稱，格式為*database.schema.table_name*。  
  
 無法建立*new_table*上的遠端伺服器; 不過，您可以填入*new_table*從遠端資料來源。 若要建立*new_table*從遠端來源資料表中，指定在表單中使用四部分名稱的來源資料表*linked_server*。*目錄*。*結構描述*。*物件*SELECT 陳述式的 FROM 子句中。 或者，您可以使用[OPENQUERY](../../t-sql/functions/openquery-transact-sql.md)函式或[OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) FROM 子句來指定遠端資料來源中的函式。  
  
## <a name="data-types"></a>資料型別  
 FILESTREAM 屬性不會傳送至新的資料表。 已複製 FILESTREAM Blob 時，並將其儲存在新的資料表做為**varbinary （max)** Blob。 若沒有 FILESTREAM 屬性**varbinary （max)**資料類型有 2 GB 的限制。 如果 FILESTREAM BLOB 超過這個值，系統就會引發錯誤 7119 並且停止此陳述式。  
  
 當您將現有的識別欄位選入新的資料表時，除非下列其中一個狀況成立，否則新資料行會繼承 IDENTITY 屬性：  
  
-   SELECT 陳述式包含聯結。  
  
-   利用 UNION 來聯結多個 SELECT 陳述式。  
  
-   在選取清單中，重複列出識別欄位。  
  
-   識別欄位是運算式的一部分。  
  
-   識別欄位來自遠端資料來源。  
  
如果其中任何一個狀況成立，都會將資料行建立成 NOT NULL，而不是繼承 IDENTITY 屬性。 如果新的資料表需要識別欄位，但是無法使用這種資料行，或者您想要與來源識別欄位不同的初始或遞增值，請使用 IDENTITY 函數在選取清單中定義此資料行。 請參閱下面＜範例＞一節中的＜使用 IDENTITY 函數來建立識別欄位＞。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 您無法將資料表變數或資料表值參數指定為新的資料表。  
  
 即使已分割來源資料表，您還是無法使用 SELECT INTO 來建立分割區資料表。 SELECT...INTO 不會使用來源資料表的分割區配置，不過它會在預設的檔案群組中建立新的資料表。 若要將資料列插入分割資料表，您必須先建立分割資料表，然後再使用 INSERT INTO...SELECT FROM 陳述式。  
  
 在來源資料表中定義的索引、條件約束和觸發程序都不會傳送至新的資料表，而且您也無法在 SELECT...INTO 陳述式中指定它們。 如果您需要這些物件，可以在執行 SELECT...INTO 陳述式之後建立它們。  
  
 指定 ORDER BY 子句並不保證會依照指定的順序插入資料列。  
  
 當選取清單包括疏鬆資料行時，疏鬆資料行屬性不會傳送至新資料表中的資料行。 如果新資料表需要這個屬性，請在執行 SELECT...INTO 陳述式來加入這個屬性之後，改變資料行定義。  
  
 當選取清單包括計算資料行時，新資料表變數中對應的資料行並不是計算資料行。 新資料行中的值是執行 SELECT...INTO 時所計算的值。  
  
## <a name="logging-behavior"></a>記錄行為  
 SELECT...INTO 的記錄數量主要取決於資料庫目前使用的復原模式。 在簡單復原模式或大量記錄復原模式下，大量作業會進行最低限度記錄。 使用最低限度記錄，使用 選取... 陳述式可以比建立資料表，然後填入資料表的 INSERT 陳述式更有效率。 如需詳細資訊，請參閱[交易記錄 &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)。  
  
## <a name="permissions"></a>Permissions  
 需要目的地資料庫中的 CREATE TABLE 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-table-by-specifying-columns-from-multiple-sources"></a>A. 指定多個來源的資料行，藉以建立資料表  
 下列範例會從各個員工相關和地址相關的資料表中選取七個資料行，藉以建立 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫的`dbo.EmployeeAddresses` 資料表。  
  
```sql  
SELECT c.FirstName, c.LastName, e.JobTitle, a.AddressLine1, a.City,   
    sp.Name AS [State/Province], a.PostalCode  
INTO dbo.EmployeeAddresses  
FROM Person.Person AS c  
    JOIN HumanResources.Employee AS e   
    ON e.BusinessEntityID = c.BusinessEntityID  
    JOIN Person.BusinessEntityAddress AS bea  
    ON e.BusinessEntityID = bea.BusinessEntityID  
    JOIN Person.Address AS a  
    ON bea.AddressID = a.AddressID  
    JOIN Person.StateProvince as sp   
    ON sp.StateProvinceID = a.StateProvinceID;  
GO  
```  
  
### <a name="b-inserting-rows-using-minimal-logging"></a>B. 使用最低限度記錄來插入資料列  
 下列範例會建立 `dbo.NewProducts` 資料表，然後插入 `Production.Product` 資料表的資料列。 此範例會假設 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫的復原模式設定為 FULL。 為了確保使用最低限度記錄，[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫的復原模式會在插入資料列之前設定為 BULK_LOGGED，然後在 SELECT...INTO 陳述式之後重設為 FULL。 此程序可確保 SELECT...INTO 陳述式會在交易記錄中使用最小的空間並有效率地執行作業。  
  
```sql  
ALTER DATABASE AdventureWorks2012 SET RECOVERY BULK_LOGGED;  
GO  
  
SELECT * INTO dbo.NewProducts  
FROM Production.Product  
WHERE ListPrice > $25   
AND ListPrice < $100;  
GO  
ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
GO  
```  
  
### <a name="c-creating-an-identity-column-using-the-identity-function"></a>C. 使用 IDENTITY 函數來建立識別欄位  
 下列範例會使用 IDENTITY 函數，在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫的新資料表 `Person.USAddress` 中建立識別欄位。 因為定義此資料表的 SELECT 陳述式包含聯結，導致 IDENTITY 屬性無法傳送至新的資料表，所以需要進行此步驟。 請注意，在 IDENTITY 函數中指定的初始和遞增值與來源資料表 `AddressID` 中 `Person.Address` 資料行的初始和遞增值不同。  
  
```sql  
-- Determine the IDENTITY status of the source column AddressID.  
SELECT OBJECT_NAME(object_id) AS TableName, name AS column_name, 
  is_identity, seed_value, increment_value  
FROM sys.identity_columns  
WHERE name = 'AddressID';  
  
-- Create a new table with columns from the existing table Person.Address. 
-- A new IDENTITY column is created by using the IDENTITY function.  
SELECT IDENTITY (int, 100, 5) AS AddressID,   
       a.AddressLine1, a.City, b.Name AS State, a.PostalCode  
INTO Person.USAddress   
FROM Person.Address AS a  
INNER JOIN Person.StateProvince AS b 
  ON a.StateProvinceID = b.StateProvinceID  
WHERE b.CountryRegionCode = N'US';   
  
-- Verify the IDENTITY status of the AddressID columns in both tables.  
SELECT OBJECT_NAME(object_id) AS TableName, name AS column_name, 
  is_identity, seed_value, increment_value  
FROM sys.identity_columns  
WHERE name = 'AddressID';  
```  
  
### <a name="d-creating-a-table-by-specifying-columns-from-a-remote-data-source"></a>D. 指定遠端資料來源的資料行，藉以建立資料表  
 下列範例將示範三種根據遠端資料來源在本機伺服器上建立新資料表的方法。 此範例一開始會建立遠端資料來源的連結。 然後，連結的伺服器名稱 `MyLinkServer,` 會指定於第一個 SELECT...INTO 陳述式的 FROM 子句和第二個 SELECT...INTO 陳述式的 OPENQUERY 函數中。 最後，第三個 SELECT...INTO 陳述式會使用 OPENDATASOURCE 函數，以便直接指定遠端資料來源，而非使用連結的伺服器名稱。  
  
 **適用於：** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```sql
USE master;  
GO  
-- Create a link to the remote data source.   
-- Specify a valid server name for @datasrc as 'server_name' 
-- or 'server_name\instance_name'.  
EXEC sp_addlinkedserver @server = N'MyLinkServer',  
    @srvproduct = N' ',  
    @provider = N'SQLNCLI',   
    @datasrc = N'server_name',  
    @catalog = N'AdventureWorks2012';  
GO  

USE AdventureWorks2012;  
GO  
-- Specify the remote data source in the FROM clause using a four-part name   
-- in the form linked_server.catalog.schema.object.  
SELECT DepartmentID, Name, GroupName, ModifiedDate  
INTO dbo.Departments  
FROM MyLinkServer.AdventureWorks2012.HumanResources.Department  
GO  
-- Use the OPENQUERY function to access the remote data source.  
SELECT DepartmentID, Name, GroupName, ModifiedDate  
INTO dbo.DepartmentsUsingOpenQuery  
FROM OPENQUERY(MyLinkServer, 'SELECT *  
               FROM AdventureWorks2012.HumanResources.Department');   
GO  
-- Use the OPENDATASOURCE function to specify the remote data source.  
-- Specify a valid server name for Data Source using the format 
-- server_name or server_name\instance_name.  
SELECT DepartmentID, Name, GroupName, ModifiedDate  
INTO dbo.DepartmentsUsingOpenDataSource  
FROM OPENDATASOURCE('SQLNCLI',  
    'Data Source=server_name;Integrated Security=SSPI')  
    .AdventureWorks2012.HumanResources.Department;  
GO  
```  
  
### <a name="e-import-from-an-external-table-created-with--polybase"></a>E. 從外部資料表建立使用 PolyBase 匯入  
 將資料從 Hadoop 或 Azure 儲存體匯入至 SQL Server 以便持續儲存。 使用`SELECT INTO`匯入 SQL Server 中的永續性儲存體的外部資料表所參考的資料。 在第二個步驟中，快速建立關聯式資料表，然後在資料表上建立資料行存放區索引。  
  
 **適用於：** [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```sql
-- Import data for car drivers into SQL Server to do more in-depth analysis.  
SELECT DISTINCT   
        Insured_Customers.FirstName, Insured_Customers.LastName,   
        Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
INTO Fast_Customers from Insured_Customers INNER JOIN   
(  
        SELECT * FROM CarSensor_Data where Speed > 35   
) AS SensorD  
ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
ORDER BY YearlyIncome  
  
```  
### <a name="f-creating-a-new-table-as-a-copy-of-another-table-and-loading-it-a-specified-filegroup"></a>F. 建立新的資料表做為另一個資料表的複本並將其載入指定的檔案群組
下列範例會示範做為另一個資料表的複本建立新的資料表，並將它載入到指定的檔案群組不同於使用者的預設檔案群組。

 **適用於：**[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]

```sql
ALTER DATABASE [AdventureWorksDW2016] ADD FILEGROUP FG2;
ALTER DATABASE [AdventureWorksDW2016]
ADD FILE
(
NAME='FG2_Data',
FILENAME = '/var/opt/mssql/data/AdventureWorksDW2016_Data1.mdf'
)
TO FILEGROUP FG2;
GO
SELECT *  INTO [dbo].[FactResellerSalesXL] ON FG2 from [dbo].[FactResellerSales]
```
  
## <a name="see-also"></a>另請參閱  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [精選的範例 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-examples-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [IDENTITY &#40;函式 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/functions/identity-function-transact-sql.md)  
  
  
