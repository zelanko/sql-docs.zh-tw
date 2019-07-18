---
title: 資料表值建構函式 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- inserting multiple rows
- row value expression
- row constructor [SQL Server]
- table value constructor [SQL Server]
ms.assetid: e57cd31d-140e-422f-8178-2761c27b9deb
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: e1a4ca0732a8ce2dda6a3d8d674b1a74940b4c8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66198195"
---
# <a name="table-value-constructor-transact-sql"></a>資料表值建構函式 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定要建構到資料表中的一組資料列值運算式。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 資料表值建構函式允許在單一 DML 陳述式中指定多個資料列。 資料表值建構函式可以指定為 INSERT ... VALUES 陳述式的 VALUES 子句，或指定為 MERGE 陳述式之 USING 子句或 FROM 子句中的衍生資料表。
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
VALUES ( <row value expression list> ) [ ,...n ]   
  
<row value expression list> ::=  
    {<row value expression> } [ ,...n ]  
  
<row value expression> ::=  
    { DEFAULT | NULL | expression }  
```  
  
## <a name="arguments"></a>引數  
 VALUES  
 導入資料列值運算式清單。 每一個清單都必須以括號括住，並以逗點隔開。  
  
 每一個清單中指定的值數目都必須相同，而且值的順序必須與資料表中的資料行相同。 必須指定資料表中每一個資料行的值，或者資料行清單必須明確指定每一個內送值的資料行。  
  
 DEFAULT  
 強制 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 插入定義給資料行的預設值。 如果資料行的預設值不存在，而且資料行允許 Null 值，就會插入 NULL。 DEFAULT 對識別欄位無效。 在資料表值建構函式中指定時，INSERT 陳述式中只允許 DEFAULT。  
  
 *expression*  
 這是一個常數、變數或運算式。 此運算式不能包含 EXECUTE 陳述式。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 用作衍生資料表時，資料列數目沒有限制。  
 
 作為 INSERT ... VALUES 陳述式的 VALUES 子句時，資料列數目限制為 1000 個。 如果資料列數目超過最大值，就會傳回錯誤 10738。 若要插入 1000 個以上的資料列，請使用下列其中一種方法：  
  
- 建立多個 INSERT 陳述式  
  
- 使用衍生資料表  
  
- 使用 [**bcp** 公用程式](../../tools/bcp-utility.md) ( .NET [SqlBulkCopy class](/dotnet/api/system.data.sqlclient.sqlbulkcopy)、[OPENROWSET (BULK ...))](../../t-sql/functions/openrowset-transact-sql.md) 或 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 陳述式來大量匯入資料  
  
 只允許使用單一純量值當做資料列值運算式。 不允許使用牽涉多個資料行的子查詢當做資料列值運算式。 例如，下列程式碼會產生語法錯誤，因為第三個資料列值運算式清單包含具有多個資料行的子查詢。  
  
```sql
USE AdventureWorks2012;  
GO  
CREATE TABLE dbo.MyProducts (Name varchar(50), ListPrice money);  
GO  
-- This statement fails because the third values list contains multiple columns in the subquery.  
INSERT INTO dbo.MyProducts (Name, ListPrice)  
VALUES ('Helmet', 25.50),  
       ('Wheel', 30.00),  
       (SELECT Name, ListPrice FROM Production.Product WHERE ProductID = 720);  
GO  
```  
  
 不過，您可以個別在子查詢中指定每個資料行，藉以重新撰寫此陳述式。 下列範例會成功地將三個資料列插入 `MyProducts` 資料表中。  
  
```sql
INSERT INTO dbo.MyProducts (Name, ListPrice)  
VALUES ('Helmet', 25.50),  
       ('Wheel', 30.00),  
       ((SELECT Name FROM Production.Product WHERE ProductID = 720),  
        (SELECT ListPrice FROM Production.Product WHERE ProductID = 720));  
GO  
```  
  
## <a name="data-types"></a>資料型別  
 在多重資料列 INSERT 陳述式中指定的值會遵循 UNION ALL 語法的資料類型轉換屬性。 這會導致將不相符的類型隱含地轉換成較高[優先順序](../../t-sql/data-types/data-type-precedence-transact-sql.md)的類型。 如果轉換不是支援的隱含轉換，就會傳回錯誤。 例如，下列陳述式會將整數值和字元值插入至類型為 **char** 的資料行中。  
  
```sql
CREATE TABLE dbo.t (a int, b char);  
GO  
INSERT INTO dbo.t VALUES (1,'a'), (2, 1);  
GO  
```  
  
 當執行 INSERT 陳述式時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會嘗試將 'a' 轉換成整數，因為資料類型優先順序指出整數的類型高於字元。 轉換會失敗，並傳回錯誤。 您可以適當且明確地轉換值來避免這個錯誤。 例如，可以依照以下方式撰寫上面的陳述式。  
  
```sql
INSERT INTO dbo.t VALUES (1,'a'), (2, CONVERT(CHAR,1));  
```  
  
## <a name="examples"></a>範例  
  
### <a name="a-inserting-multiple-rows-of-data"></a>A. 插入多個資料列  
 下列範例會建立 `dbo.Departments` 資料表，然後使用資料表值建構函式將五個資料列插入此資料表。 由於提供了所有資料行的值，而且依照資料表中資料行的相同順序來列出它們，因此，不需要在資料行清單中指定資料行名稱。  
  
```sql
USE AdventureWorks2012;  
GO  
INSERT INTO Production.UnitMeasure  
VALUES (N'FT2', N'Square Feet ', '20080923'), (N'Y', N'Yards', '20080923'),
       (N'Y3', N'Cubic Yards', '20080923');  
GO  
```  
  
### <a name="b-inserting-multiple-rows-with-default-and-null-values"></a>B. 插入具有 DEFAULT 和 NULL 值的多個資料列  
 下列範例會示範在使用資料表值建構函式將資料列插入資料表時，如何指定 DEFAULT 和 NULL。  
  
```sql
USE AdventureWorks2012;  
GO  
CREATE TABLE Sales.MySalesReason(  
SalesReasonID int IDENTITY(1,1) NOT NULL,  
Name dbo.Name NULL ,  
ReasonType dbo.Name NOT NULL DEFAULT 'Not Applicable' );  
GO  
INSERT INTO Sales.MySalesReason   
VALUES ('Recommendation','Other'), ('Advertisement', DEFAULT), (NULL, 'Promotion');  
  
SELECT * FROM Sales.MySalesReason;  
```  
  
### <a name="c-specifying-multiple-values-as-a-derived-table-in-a-from-clause"></a>C. 將多個值指定為 FROM 子句中的衍生資料表  
 下列範例會使用資料表值建構函式，在 SELECT 陳述式的 FROM 子句中指定多個值。  
  
```sql
SELECT a, b FROM (VALUES (1, 2), (3, 4), (5, 6), (7, 8), (9, 10) ) AS MyTable(a, b);  
GO  
-- Used in an inner join to specify values to return.  
SELECT ProductID, a.Name, Color  
FROM Production.Product AS a  
INNER JOIN (VALUES ('Blade'), ('Crown Race'), ('AWC Logo Cap')) AS b(Name)   
ON a.Name = b.Name;  
```  
  
### <a name="d-specifying-multiple-values-as-a-derived-source-table-in-a-merge-statement"></a>D. 在 MERGE 陳述式中將多個值指定為衍生的來源資料表  
 下列範例會使用 MERGE，藉由更新或插入資料列來修改 `SalesReason` 資料表。 當來源資料表中的 `NewName` 值符合目標資料表 (`Name`) 中 `SalesReason` 資料行內的值時，就會更新目標資料表中的 `ReasonType` 資料行。 當 `NewName` 的值不相符時，來源資料列會插入目標資料表中。 來源資料表是一種衍生資料表，可使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 資料表值建構函式針對來源資料表指定多個資料列。  
  
```sql
USE AdventureWorks2012;  
GO  
-- Create a temporary table variable to hold the output actions.  
DECLARE @SummaryOfChanges TABLE(Change VARCHAR(20));  
  
MERGE INTO Sales.SalesReason AS Target  
USING (VALUES ('Recommendation','Other'), ('Review', 'Marketing'), ('Internet', 'Promotion'))  
       AS Source (NewName, NewReasonType)  
ON Target.Name = Source.NewName  
WHEN MATCHED THEN  
UPDATE SET ReasonType = Source.NewReasonType  
WHEN NOT MATCHED BY TARGET THEN  
INSERT (Name, ReasonType) VALUES (NewName, NewReasonType)  
OUTPUT $action INTO @SummaryOfChanges;  
  
-- Query the results of the table variable.  
SELECT Change, COUNT(*) AS CountPerChange  
FROM @SummaryOfChanges  
GROUP BY Change;  
```  
  
### <a name="e-inserting-more-than-1000-rows"></a>E. 插入超過 1000 個資料列
  下列範例示範如何使用資料表值建構函式作為衍生資料表。 這允許從單一資料表值建構函式插入超過 1000 個資料列。
  
```sql
CREATE TABLE dbo.Test ([Value] int);  
  
INSERT INTO dbo.Test ([Value])  
  SELECT drvd.[NewVal]
  FROM   (VALUES (0), (1), (2), (3), ..., (5000)) drvd([NewVal]);
```  


## <a name="see-also"></a>另請參閱  
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)  
  
  
