---
title: "變數 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: f372ae86-a003-40af-92de-fa52e3eea13f
caps.latest.revision: "12"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 7e113be00cbfdaf0dd1e0164623aec3516327a23
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="variables-transact-sql"></a>變數 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

TRANSACT-SQL 本機變數是可保存特定類型的單一資料值的物件。 批次和指令碼中的變數通常的用途為： 

* 作為計數器 (Counter)，計算迴圈 (Loop) 執行的次數，或控制迴圈執行的次數。
* 容納由流程控制陳述式測試的資料值。
* 若要儲存預存程序傳回碼或函數傳回值所傳回的資料值。

> [!NOTE]
> 一些 TRANSACT-SQL 系統函式的名稱開頭為兩個*在*符號 （@ @）。 雖然在舊版的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 @@functions會參照為全域變數，它們並不是變數，沒有做為變數相同的行為。 @@functions系統函式，以及其語法使用方式會遵循函式的規則。

以下指令碼建立一個小型測試資料表，並於其中填入 26 個資料列。 指令碼將使用變數進行三個用途： 

* 藉由控制迴圈執行次數，來控制插入的資料列數。
* 提供插入整數資料行的數值。
* 當作運算式的一部份，用來產生插入字元資料行的文字。  

```sql
-- Create the table.
CREATE TABLE TestTable (cola int, colb char(3));
GO
SET NOCOUNT ON;
GO
-- Declare the variable to be used.
DECLARE @MyCounter int;

-- Initialize the variable.
SET @MyCounter = 0;

-- Test the variable to see if the loop is finished.
WHILE (@MyCounter < 26)
BEGIN;
   -- Insert a row into the table.
   INSERT INTO TestTable VALUES
       -- Use the variable to provide the integer value
       -- for cola. Also use it to generate a unique letter
       -- for each row. Use the ASCII function to get the
       -- integer value of 'a'. Add @MyCounter. Use CHAR to
       -- convert the sum back to the character @MyCounter
       -- characters after 'a'.
       (@MyCounter,
        CHAR( ( @MyCounter + ASCII('a') ) )
       );
   -- Increment the variable to count this iteration
   -- of the loop.
   SET @MyCounter = @MyCounter + 1;
END;
GO
SET NOCOUNT OFF;
GO
-- View the data.
SELECT cola, colb
FROM TestTable;
GO
DROP TABLE TestTable;
GO
```

## <a name="declaring-a-transact-sql-variable"></a>宣告 Transact-SQL 變數
DECLARE 陳述式會初始化 TRANSACT-SQL 變數： 
* 指派名稱。 名稱必須帶有單一 @ 作為第一個字元。
* 指派系統提供或使用者自訂的資料類型和長度。 若是數值變數，也會指派有效位數和小數位數。 若是 XML 類型的變數，可能會指派選擇性結構描述集合。
* 設定值為 NULL。

例如，下列**DECLARE**陳述式會建立名為區域變數 **@mycounter**  int 資料類型。  
```sql
DECLARE @MyCounter int;
```
若要宣告一個以上的本機變數，請在第一個定義的本機變數後加上逗號，再指定下一個本機變數名稱與資料類型。

例如，下列**DECLARE**陳述式會建立三個本機變數，名為 **@LastName** ，  **@FirstName** 和 **@StateProvince** ，均初始化為 NULL:  
```sql
DECLARE @LastName nvarchar(30), @FirstName nvarchar(20), @StateProvince nchar(2);
```

變數的範圍是可以參考變數的範圍的 TRANSACT-SQL 陳述式。 變數範圍會維持在宣告點上，直到宣告批次或預存程序的結尾為止。 例如，下列指令碼會產生語法錯誤，因為變數是在某個批次中宣告並在其他批次中參考：  
```sql
USE AdventureWorks2014;
GO
DECLARE @MyVariable int;
SET @MyVariable = 1;
-- Terminate the batch by using the GO keyword.
GO 
-- @MyVariable has gone out of scope and no longer exists.

-- This SELECT statement generates a syntax error because it is
-- no longer legal to reference @MyVariable.
SELECT BusinessEntityID, NationalIDNumber, JobTitle
FROM HumanResources.Employee
WHERE BusinessEntityID = @MyVariable;
```

變數具有區域範圍並且只能在定義變數的批次或程序中看到。 在下列範例中，為執行 sp_executesql 所建立的巢狀範圍沒有在較高範圍中宣告變數的存取權，並會傳回錯誤。  

```sql
DECLARE @MyVariable int;
SET @MyVariable = 1;
EXECUTE sp_executesql N'SELECT @MyVariable'; -- this produces an error
```

## <a name="setting-a-value-in-a-transact-sql-variable"></a>設定 Transact-SQL 變數的值

首次宣告變數時，其值會設為 NULL。 若要指派值給變數，請使用 SET 陳述式。 這是將值指派給變數所慣用的方法。 您也可以參考 SELECT 陳述式的選取清單，將值指派給變數。

若要使用 SET 陳述式指派值給變數，請加入變數名稱和值以指派給變數。 這是將值指派給變數所慣用的方法。 例如，下列批次會宣告兩個變數、指派值給變數，然後在 `WHERE` 陳述式的 `SELECT` 子句中使用這些變數：  

```sql
USE AdventureWorks2014;
GO
-- Declare two variables.
DECLARE @FirstNameVariable nvarchar(50),
   @PostalCodeVariable nvarchar(15);

-- Set their values.
SET @FirstNameVariable = N'Amy';
SET @PostalCodeVariable = N'BA5 3HX';

-- Use them in the WHERE clause of a SELECT statement.
SELECT LastName, FirstName, JobTitle, City, StateProvinceName, CountryRegionName
FROM HumanResources.vEmployee
WHERE FirstName = @FirstNameVariable
   OR PostalCode = @PostalCodeVariable;
GO
```

您也可以建立參考變數的選取清單，將值指派給變數。 如果變數參考至選取清單，應該指派變數的純量值 (Scalar)，不然 SELECT 陳述式僅傳回一個資料列。 例如：  

```sql
USE AdventureWorks2014;
GO
DECLARE @EmpIDVariable int;

SELECT @EmpIDVariable = MAX(EmployeeID)
FROM HumanResources.Employee;
GO
```

> [!WARNING]
> 如果在單一 SELECT 陳述式中有多個指派子句，SQL Server 則無法保證運算式評估的次序。 請注意，只有當指派中有一些參考時，才能看到產生的效果。

如果 SELECT 陳述式傳回多個資料列，且變數參考非純量運算式，此變數會設為結果集的最後一個資料列中的運算式的傳回值。 例如，在下列批次 **@EmpIDVariable** 設**BusinessEntityID**傳回最後一個資料列的值，也就是 1:  

```sql
USE AdventureWorks2014;
GO
DECLARE @EmpIDVariable int;

SELECT @EmpIDVariable = BusinessEntityID
FROM HumanResources.Employee
ORDER BY BusinessEntityID DESC;

SELECT @EmpIDVariable;
GO
```

## <a name="see-also"></a>請參閱＜  
 [宣告@local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
 [SET@local_variable](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
 [SELECT @local_variable](../../t-sql/language-elements/select-local-variable-transact-sql.md)  
 [運算式 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [複合運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
  
  
