---
title: "聯合 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COALESCE
- COALESCE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- expressions [SQL Server], nonnull
- COALESCE function
- first nonnull expressions [SQL Server]
- nonnull expressions
ms.assetid: fafc0dba-f8a8-4aad-9b7f-908e34b74d88
caps.latest.revision: "52"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: b2d67040ae1f55e94baf03eb45929459fc39a84a
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="coalesce-transact-sql"></a>COALESCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

評估順序的引數，並傳回一開始未評估的第一個運算式的目前值`NULL`。 例如，`SELECT COALESCE(NULL, NULL, 'third_value', 'fourth_value');`傳回第三個值，因為第三個值不是 null 的第一個值。 
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
COALESCE ( expression [ ,...n ] )   
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)任何型別。  
  
## <a name="return-types"></a>傳回類型  
 傳回的資料型別*運算式*具有最高的資料類型優先順序。 如果所有運算式都不可為 Null，結果的類型也是不可為 Null。  
  
## <a name="remarks"></a>備註  
 如果所有引數`NULL`，`COALESCE`傳回`NULL`。 至少一個 null 的值必須是具型別的`NULL`。  
  
## <a name="comparing-coalesce-and-case"></a>比較 COALESCE 和 CASE  
 `COALESCE`運算式是的語法捷徑`CASE`運算式。  也就是程式碼`COALESCE`(*expression1*，*...n*) 重寫查詢最佳化工具，如下所示`CASE`運算式：  
  
 ```sql  
 CASE  
 WHEN (expression1 IS NOT NULL) THEN expression1  
 WHEN (expression2 IS NOT NULL) THEN expression2  
 ...  
 ELSE expressionN  
 END  
 ```  
  
 這表示輸入的值 (*expression1*， *expression2*， *expressionN*等等) 而評估多次。 此外，為了符合 SQL 標準，包含子查詢的值運算式會視為不具決定性，且會評估子查詢兩次。 不論是哪一種情況，第一次評估和後續評估之間都可能傳回不同的結果。  
  
 例如，執行程式碼 `COALESCE((subquery), 1)` 時，會評估子查詢兩次。 因此，您會根據查詢的隔離等級取得不同的結果。 例如，程式碼可以傳回`NULL`下`READ COMMITTED`多使用者環境中的隔離等級。 若要確保傳回的結果穩定，請使用`SNAPSHOT ISOLATION`隔離層級或取代`COALESCE`與`ISNULL`函式。 或者，您可以撰寫查詢，以將子查詢推入子選擇，如下列範例所示：  
  
```sql  
SELECT CASE WHEN x IS NOT NULL THEN x ELSE 1 END  
from  
(  
SELECT (SELECT Nullable FROM Demo WHERE SomeCol = 1) AS x  
) AS T;  
  
```  
  
## <a name="comparing-coalesce-and-isnull"></a>比較 COALESCE 和 ISNULL  
 `ISNULL`函式和`COALESCE`運算式具有相似的目的，但可以有不同的行為。  
  
1.  因為`ISNULL`是函數，它只評估一次。  如上面所述，輸入值`COALESCE`運算式可以評估多次。  
  
2.  結果運算式所決定的資料類型會不同。 `ISNULL`會使用第一個參數的資料型別`COALESCE`遵循`CASE`規則運算式，並傳回具有最高優先順序值的資料類型。  
  
3.  結果運算式的 null 屬性是不同的`ISNULL`和`COALESCE`。 `ISNULL`傳回值一律視為不可為 Null （假設傳回的值一個不可為 null） 而`COALESCE`和非 null 參數會被視為`NULL`。 因此運算式`ISNULL(NULL, 1)`和`COALESCE(NULL, 1)`，不過，對等，有不同的 null 屬性的值。 如果您要在計算資料行中使用這些運算式、 建立索引鍵條件約束或進行的純量 UDF 的傳回值具有決定性，以便可以在下列範例所示索引，這會形成差異：  
  
    ```sql  
    USE tempdb;  
    GO  
    -- This statement fails because the PRIMARY KEY cannot accept NULL values  
    -- and the nullability of the COALESCE expression for col2   
    -- evaluates to NULL.  
    CREATE TABLE #Demo   
    (   
    col1 integer NULL,   
    col2 AS COALESCE(col1, 0) PRIMARY KEY,   
    col3 AS ISNULL(col1, 0)   
    );   
  
    -- This statement succeeds because the nullability of the   
    -- ISNULL function evaluates AS NOT NULL.  
  
    CREATE TABLE #Demo   
    (   
    col1 integer NULL,   
    col2 AS COALESCE(col1, 0),   
    col3 AS ISNULL(col1, 0) PRIMARY KEY   
    );  
    ```  
  
4.  驗證`ISNULL`和`COALESCE`也會不同。 例如，`NULL`值`ISNULL`轉換成**int**而如`COALESCE`，您必須提供資料類型。  
  
5.  `ISNULL`會採用只有兩個參數，而`COALESCE`接受可變數目的參數。  
  
## <a name="examples"></a>範例  
  
### <a name="a-running-a-simple-example"></a>A. 執行簡單範例  
 下列範例示範  `COALESCE` 如何從具有非  Null  值的第一個資料行選取資料。 這個範例會使用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫。  
  
```sql  
SELECT Name, Class, Color, ProductNumber,  
COALESCE(Class, Color, ProductNumber) AS FirstNotNull  
FROM Production.Product;  
```  
  
### <a name="b-running-a-complex-example"></a>B. 執行複雜範例  
 在下列範例中，`wages` 資料表有三個含員工年薪 (時薪、月薪加上分紅) 相關資訊的資料行。 不過，員工只會收到其中一種款項。 若要算出支付給所有員工的總金額，請使用 `COALESCE`，只接收 `hourly_wage`、`salary` 和 `commission` 中的非 Null 值。  
  
```sql  
SET NOCOUNT ON;  
GO  
USE tempdb;  
IF OBJECT_ID('dbo.wages') IS NOT NULL  
    DROP TABLE wages;  
GO  
CREATE TABLE dbo.wages  
(  
    emp_id        tinyint   identity,  
    hourly_wage   decimal   NULL,  
    salary        decimal   NULL,  
    commission    decimal   NULL,  
    num_sales     tinyint   NULL  
);  
GO  
INSERT dbo.wages (hourly_wage, salary, commission, num_sales)  
VALUES  
    (10.00, NULL, NULL, NULL),  
    (20.00, NULL, NULL, NULL),  
    (30.00, NULL, NULL, NULL),  
    (40.00, NULL, NULL, NULL),  
    (NULL, 10000.00, NULL, NULL),  
    (NULL, 20000.00, NULL, NULL),  
    (NULL, 30000.00, NULL, NULL),  
    (NULL, 40000.00, NULL, NULL),  
    (NULL, NULL, 15000, 3),  
    (NULL, NULL, 25000, 2),  
    (NULL, NULL, 20000, 6),  
    (NULL, NULL, 14000, 4);  
GO  
SET NOCOUNT OFF;  
GO  
SELECT CAST(COALESCE(hourly_wage * 40 * 52,   
   salary,   
   commission * num_sales) AS money) AS 'Total Salary'   
FROM dbo.wages  
ORDER BY 'Total Salary';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```   
 Total Salary  
 ------------  
 10000.00  
 20000.00  
 20800.00  
 30000.00  
 40000.00  
 41600.00  
 45000.00  
 50000.00  
 56000.00  
 62400.00  
 83200.00  
 120000.00  
  
 (12 row(s) affected)
 ```  
  
### <a name="c-simple-example"></a>C： 簡單的範例  
 下列範例會示範如何`COALESCE`選取具有非 null 值的第一個資料行中的資料。 此範例假設，`Products`資料表包含此資料：  
  
 ```  
 Name         Color      ProductNumber  
 ------------ ---------- -------------  
 Socks, Mens  NULL       PN1278  
 Socks, Mens  Blue       PN1965  
 NULL         White      PN9876
 ```  
  
 然後，我們會執行下列聯合查詢：  
  
```sql  
SELECT Name, Color, ProductNumber, COALESCE(Color, ProductNumber) AS FirstNotNull   
FROM Products ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 Name         Color      ProductNumber  FirstNotNull  
 ------------ ---------- -------------  ------------  
 Socks, Mens  NULL       PN1278         PN1278  
 Socks, Mens  Blue       PN1965         Blue  
 NULL         White      PN9876         White
 ```  
  
 請注意，在第一個資料列，`FirstNotNull`值是`PN1278`，而非`Socks, Mens`。 這是因為`Name`做為參數，如未指定資料行`COALESCE`在範例中。  
  
### <a name="d-complex-example"></a>D： 複雜的範例  
 下列範例會使用`COALESCE`比較三個資料行中的值，並只傳回非 null 值的資料行中找到。  
  
```sql  
CREATE TABLE dbo.wages  
(  
    emp_id        tinyint   NULL,  
    hourly_wage   decimal   NULL,  
    salary        decimal   NULL,  
    commission    decimal   NULL,  
    num_sales     tinyint   NULL  
);  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (1, 10.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (2, 20.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (3, 30.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (4, 40.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (5, NULL, 10000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (6, NULL, 20000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (7, NULL, 30000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (8, NULL, 40000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (9, NULL, NULL, 15000, 3);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (10,NULL, NULL, 25000, 2);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (11, NULL, NULL, 20000, 6);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (12, NULL, NULL, 14000, 4);  
  
SELECT CAST(COALESCE(hourly_wage * 40 * 52,   
   salary,   
   commission * num_sales) AS decimal(10,2)) AS TotalSalary   
FROM dbo.wages  
ORDER BY TotalSalary;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Total Salary  
 ------------  
 10000.00  
 20000.00  
 20800.00  
 30000.00  
 40000.00  
 41600.00  
 45000.00  
 50000.00  
 56000.00  
 62400.00  
 83200.00  
 120000.00
 ```  
  
## <a name="see-also"></a>另請參閱  
 [ISNULL &#40;TRANSACT-SQL &#41;](../../t-sql/functions/isnull-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)  
  
  
