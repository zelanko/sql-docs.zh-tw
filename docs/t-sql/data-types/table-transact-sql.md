---
title: "資料表 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- table data type [SQL Server]
- table variables [SQL Server]
ms.assetid: 1ef0b60e-a64c-4e97-847b-67930e3973ef
caps.latest.revision: 48
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b22ecfa04f949af77df974abc3359b7bc5144a82
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="table-transact-sql"></a>資料表 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

一種特殊的資料類型，可用於儲存結果集以供後續處理。 **資料表**主要用於暫時儲存當做資料表值函式的結果集傳回的資料列集。 函式和變數可以宣告為類型**資料表**。 **資料表**變數可以用於函式、 預存程序和批次。 若要宣告類型的變數**資料表**，使用[DECLARE @local_variable ](../../t-sql/language-elements/declare-local-variable-transact-sql.md)。
  

**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
table_type_definition ::=   
    TABLE ( { <column_definition> | <table_constraint> } [ ,...n ] )   
  
<column_definition> ::=   
    column_name scalar_data_type   
    [ COLLATE <collation_definition> ]   
    [ [ DEFAULT constant_expression ] | IDENTITY [ ( seed , increment ) ] ]   
    [ ROWGUIDCOL ]   
    [ column_constraint ] [ ...n ]   
  
 <column_constraint> ::=   
    { [ NULL | NOT NULL ]   
    | [ PRIMARY KEY | UNIQUE ]   
    | CHECK ( logical_expression )   
    }   
  
<table_constraint> ::=   
     { { PRIMARY KEY | UNIQUE } ( column_name [ ,...n ] )  
     | CHECK ( logical_expression )   
     }   
```  
  
## <a name="arguments"></a>引數  
*table_type_definition*  
這是在 CREATE TABLE 中，用來定義資料表的相同資訊子集。 資料表宣告包括資料行定義、名稱、資料類型和條件約束。 允許使用的條件約束類型只有 PRIMARY KEY、UNIQUE KEY 和 NULL。  
如需語法的詳細資訊，請參閱[CREATE TABLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-table-transact-sql.md)，[建立函式 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-function-transact-sql.md)，和[DECLARE @local_variable &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md).
  
*collation_definition*  
由所組成的資料行的定序[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 地區設定和比較樣式、 Windows 地區設定和二進位標記法，或[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]定序。 如果*collation_definition*未指定，則資料行會繼承目前資料庫的定序。 如果將資料行定義為 Common Language Runtime (CLR) 使用者定義型別，此資料行便會繼承使用者定義型別的定序。
  
## <a name="remarks"></a>備註  
**資料表**可以批次中的 FROM 子句中依據名稱參考變數，如下列範例所示：
  
```sql
SELECT Employee_ID, Department_ID FROM @MyTableVar;  
```  
  
FROM 子句，之外**資料表**變數必須參考使用別名，如下列範例所示：
  
```sql
SELECT EmployeeID, DepartmentID   
FROM @MyTableVar m  
JOIN Employee on (m.EmployeeID =Employee.EmployeeID AND  
   m.DepartmentID = Employee.DepartmentID);  
```  
  
**資料表**變數的小規模查詢，查詢計劃不會變更和重新編譯考量主控時提供下列優點：
-   A**資料表**變數的行為類似於本機變數。 它有一個定義妥善的範圍。 這是其宣告所在的函數、預存程序或批次。  
     其在範圍內，**資料表**可以使用變數，就像是一般資料表。 在 SELECT、INSERT、UPDATE 和 DELETE 陳述式中，任何使用資料表或資料表運算式的位置都可以套用它。 不過，**資料表**不能在下列陳述式：  
  
```sql
SELECT select_list INTO table_variable;
```
  
**資料表**變數會自動清除函式、 預存程序或批次中所定義的結尾。
  
-   **資料表**預存程序中使用的變數會造成較少的重新編譯的預存程序比不會影響效能的成本考量選擇時，當使用暫存資料表。  
-   交易涉及**資料表**變數只在進行更新的上次上**資料表**變數。 因此，**資料表**變數需要較少的鎖定和記錄資源。  
  
## <a name="limitations-and-restrictions"></a>限制事項
**資料表**變數沒有散發統計資料，它們不會觸發重新編譯的次數。 因此，在許多情況下，最佳化工具都將以資料表變數沒有資料列當做假設前提，建立查詢計劃。 基於這個原因，若您預期會有較多數目的資料列 (超過 100 列)，就應該謹慎使用資料表變數。 如果是這類情況，暫存資料表也許是更適宜的方案。 或者，如果查詢聯結了資料表變數與其他資料表，使用 RECOMPILE 提示，這會造成最佳化工具針對資料表變數使用正確的基數。
  
**資料表**中不支援變數[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]最佳化工具的成本考量推論模型。 因此，需要成本考量選擇來達成有效率的查詢計劃時，就不應該使用這些變數。 需要成本考量選擇時，最好使用暫存資料表。 這種資料表通常會包含具有聯結的查詢、平行處理原則決定，以及索引選取範圍選擇。
  
修改的查詢**資料表**變數並不會產生平行查詢執行計畫。 當非常大，可能會影響效能**資料表**變數，或**資料表**複雜的查詢中的變數會被修改。 在這些狀況中，請改用暫存資料表。 如需詳細資訊，請參閱 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)。 讀取的查詢**資料表**仍可平行處理而不需修改這些變數。
  
索引無法明確建立**資料表**變數和任何統計資料會保留在**資料表**變數。 在某些情況下，改用支援索引和統計資料的暫存資料表可以提升效能。 如需暫存資料表的詳細資訊，請參閱[CREATE TABLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-table-transact-sql.md).
  
檢查條件約束、 預設值和計算資料行中的**資料表**類型宣告不能呼叫使用者定義函數。
  
指派作業之間**資料表**不支援變數。
  
因為**資料表**變數範圍受到限制，而且不是保存資料庫的一部分，不受交易回復。
  
資料表變數在建立之後無法修改。
  
## <a name="examples"></a>範例  
  
### <a name="a-declaring-a-variable-of-type-table"></a>A. 宣告類型資料表的變數  
下列範例會建立一個 `table` 變數來儲存 UPDATE 陳述式的 OUTPUT 子句所指定的值。 之後的兩個 `SELECT` 陳述式會傳回 `@MyTableVar` 中的值，以及 `Employee` 資料表中更新作業的結果。 請注意，在結果`INSERTED.ModifiedDate`資料行中值的不同`ModifiedDate`中的資料行`Employee`資料表。 這是因為將 `AFTER UPDATE` 值更新成目前日期的 `ModifiedDate` 觸發程序是定義在 `Employee` 資料表上。 不過，從 `OUTPUT` 傳回的資料行會反映引發觸發程序之前的資料。 如需詳細資訊，請參閱[OUTPUT 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/output-clause-transact-sql.md).
  
```sql
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    OldVacationHours int,  
    NewVacationHours int,  
    ModifiedDate datetime);  
UPDATE TOP (10) HumanResources.Employee  
SET VacationHours = VacationHours * 1.25   
OUTPUT INSERTED.BusinessEntityID,  
       DELETED.VacationHours,  
       INSERTED.VacationHours,  
       INSERTED.ModifiedDate  
INTO @MyTableVar;  
--Display the result set of the table variable.  
SELECT EmpID, OldVacationHours, NewVacationHours, ModifiedDate  
FROM @MyTableVar;  
GO  
--Display the result set of the table.  
--Note that ModifiedDate reflects the value generated by an  
--AFTER UPDATE trigger.  
SELECT TOP (10) BusinessEntityID, VacationHours, ModifiedDate  
FROM HumanResources.Employee;  
GO  
```  
  
### <a name="b-creating-an-inline-table-valued-function"></a>B. 建立內嵌資料表值函式  
下列範例會傳回內嵌資料表值函式。 它會傳回三個資料行`ProductID`，`Name`和依商店的年度迄今總計的彙總`YTD Total`每項產品銷售給商店。
  
```sql
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'Sales.ufn_SalesByStore', N'IF') IS NOT NULL  
    DROP FUNCTION Sales.ufn_SalesByStore;  
GO  
CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
    FROM Production.Product AS P   
    JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
    JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
    JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
    WHERE C.StoreID = @storeid  
    GROUP BY P.ProductID, P.Name  
);  
GO  
```  
  
若要叫用函數，請執行這項查詢。
  
```sql
SELECT * FROM Sales.ufn_SalesByStore (602);  
```  
  
## <a name="see-also"></a>另請參閱
[COLLATE &#40;TRANSACT-SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)  
[使用者定義的函式](../../relational-databases/user-defined-functions/user-defined-functions.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[使用資料表值參數 &#40; Database Engine &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)  
[查詢提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)
  
  

