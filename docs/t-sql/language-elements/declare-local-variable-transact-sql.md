---
title: DECLARE @local_variable (Transact-SQL) | Microsoft Docs
description: 使用 DECLARE 定義區域變數的 Transact-SQL 參考，可用於批次或程序中。
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECLARE
- DECLARE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- table-valued parameters
- variables [SQL Server], declaring
- DECLARE statement
- declaring variables
ms.assetid: d1635ebb-f751-4de1-8bbc-cae161f90821
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4fcb156d48e619a0d5ac399bf4c04a91720d3f0d
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196612"
---
# <a name="declare-local_variable-transact-sql"></a>DECLARE @local_variable (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  變數是利用 DECLARE 陳述式宣告在批次或程序的主體中，並利用 SET 或 SELECT 陳述式來指派值。 資料指標變數可以是利用這個陳述式來宣告，且可以搭配其他與資料指標相關的陳述式來使用。 在宣告之後，所有變數都會初始化成 NULL，除非在宣告中有提供值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql  
-- Syntax for SQL Server and Azure SQL Database  
  
DECLARE   
{   
    { @local_variable [AS] data_type  [ = value ] }  
  | { @cursor_variable_name CURSOR }  
} [,...n]   
| { @table_variable_name [AS] <table_type_definition> }   
  
<table_type_definition> ::=   
     TABLE ( { <column_definition> | <table_constraint> } [ ,...n] )   
  
<column_definition> ::=   
     column_name { scalar_data_type | AS computed_column_expression }  
     [ COLLATE collation_name ]   
     [ [ DEFAULT constant_expression ] | IDENTITY [ (seed ,increment ) ] ]   
     [ ROWGUIDCOL ]   
     [ <column_constraint> ]   
  
<column_constraint> ::=   
     { [ NULL | NOT NULL ]   
     | [ PRIMARY KEY | UNIQUE ]   
     | CHECK ( logical_expression )   
     | WITH ( <index_option > )  
     }   
  
<table_constraint> ::=   
     { { PRIMARY KEY | UNIQUE } ( column_name [ ,...n] )   
     | CHECK ( search_condition )   
     }   
  
<index_option> ::=  
See CREATE TABLE for index option syntax.  
  
```  
  

-- Azure Synapse Analytics 和平行處理資料倉儲的語法  
  
DECLARE   
{{ @local_variable [AS] data_type } [ =value [ COLLATE <collation_name> ] ] } [,...n]  
  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
@*local_variable*  
 Is the name of a variable. Variable names must begin with an at (@) sign. Local variable names must comply with the rules for [identifiers](../../relational-databases/databases/database-identifiers.md).  
  
*data_type*  
 Is any system-supplied, common language runtime (CLR) user-defined table type, or alias data type. A variable cannot be of **text**, **ntext**, or **image** data type.  
  
 For more information about system data types, see [Data Types &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md). For more information about CLR user-defined types or alias data types, see [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md).  
  
 =*value*  
 Assigns a value to the variable in-line. The value can be a constant or an expression, but it must either match the variable declaration type or be implicitly convertible to that type. For more information, see [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
@*cursor_variable_name*  
 Is the name of a cursor variable. Cursor variable names must begin with an at (@) sign and conform to the rules for identifiers.  
  
CURSOR  
 Specifies that the variable is a local cursor variable.  
  
@*table_variable_name*  
 Is the name of a variable of type **table**. Variable names must begin with an at  (@) sign and conform to the rules for identifiers.  
  
<table_type_definition>  
Defines the **table** data type. The table declaration includes column definitions, names, data types, and constraints. The only constraint types allowed are PRIMARY KEY, UNIQUE, NULL, and CHECK. An alias data type cannot be used as a column scalar data type if a rule or default definition is bound to the type.
  
\<table_type_definiton>
Is a subset of information used to define a table in CREATE TABLE. Elements and essential definitions are included here. For more information, see [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 *n*  
 Is a placeholder indicating that multiple variables can be specified and assigned values. When declaring **table** variables, the **table** variable must be the only variable being declared in the DECLARE statement.  
  
 *column_name*  
 Is the name of the column in the table.  
  
 *scalar_data_type*  
 Specifies that the column is a scalar data type.  
  
 *computed_column_expression*  
 Is an expression defining the value of a computed column. It is computed from an expression using other columns in the same table. For example, a computed column can have the definition **cost** AS **price \* qty**. The expression can be a noncomputed column name, constant, built-in function, variable, or any combination of these connected by one or more operators. The expression cannot be a subquery or a user-defined function. The expression cannot reference a CLR user-defined type.  
  
 [ COLLATE *collation_name*]  
 Specifies the collation for the column. *collation_name* can be either a Windows collation name or an SQL collation name, and is applicable only for columns of the **char**, **varchar**, **text**, **nchar**, **nvarchar**, and **ntext** data types. If not specified, the column is assigned either the collation of the user-defined data type (if the column is of a user-defined data type) or the collation of the current database.  
  
 For more information about the Windows and SQL collation names, see [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md).  
  
 DEFAULT  
 Specifies the value provided for the column when a value is not explicitly supplied during an insert. DEFAULT definitions can be applied to any columns except those defined as **timestamp** or those with the IDENTITY property. DEFAULT definitions are removed when the table is dropped. Only a constant value, such as a character string; a system function, such as a SYSTEM_USER(); or NULL can be used as a default. To maintain compatibility with earlier versions of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a constraint name can be assigned to a DEFAULT.  
  
 *constant_expression*  
 Is a constant, NULL, or a system function used as the default value for the column.  
  
 IDENTITY  
 Indicates that the new column is an identity column. When a new row is added to the table, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provides a unique incremental value for the column. Identity columns are commonly used in conjunction with PRIMARY KEY constraints to serve as the unique row identifier for the table. The IDENTITY property can be assigned to **tinyint**, **smallint**, **int**, **decimal(p,0)**, or **numeric(p,0)** columns. Only one identity column can be created per table. Bound defaults and DEFAULT constraints cannot be used with an identity column. You must specify both the seed and increment, or neither. If neither is specified, the default is (1,1).  
  
 *seed*  
 Is the value used for the very first row loaded into the table.  
  
 *increment*  
 Is the incremental value added to the identity value of the previous row that was loaded.  
  
 ROWGUIDCOL  
 Indicates that the new column is a row global unique identifier column. Only one **uniqueidentifier** column per table can be designated as the ROWGUIDCOL column. The ROWGUIDCOL property can be assigned only to a **uniqueidentifier** column.  
  
 NULL | NOT NULL  
 Indicates if null is allowed in the variable. The default is NULL.  
  
 PRIMARY KEY  
 Is a constraint that enforces entity integrity for a given column or columns through a unique index. Only one PRIMARY KEY constraint can be created per table.  
  
 UNIQUE  
 Is a constraint that provides entity integrity for a given column or columns through a unique index. A table can have multiple UNIQUE constraints.  
  
 CHECK  
 Is a constraint that enforces domain integrity by limiting the possible values that can be entered into a column or columns.  
  
 *logical_expression*  
 Is a logical expression that returns TRUE or FALSE.  
  
## Remarks  
 Variables are often used in a batch or procedure as counters for WHILE, LOOP, or for an IF...ELSE block.  
  
 Variables can be used only in expressions, not in place of object names or keywords. To construct dynamic SQL statements, use EXECUTE.  
  
 The scope of a local variable is the batch in which it is declared.  
 
 A table variable is not necessarily memory resident. Under memory pressure, the pages belonging to a table variable can be pushed out to tempdb.
  
 A cursor variable that currently has a cursor assigned to it can be referenced as a source in a:  
  
-   CLOSE statement.  
  
-   DEALLOCATE statement.  
  
-   FETCH statement.  
  
-   OPEN statement.  
  
-   Positioned DELETE or UPDATE statement.  
  
-   SET CURSOR variable statement (on the right side).  
  
 In all of these statements, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] raises an error if a referenced cursor variable exists but does not have a cursor currently allocated to it. If a referenced cursor variable does not exist, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] raises the same error raised for an undeclared variable of another type.  
  
 A cursor variable:  
  
-   Can be the target of either a cursor type or another cursor variable. For more information, see [SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md).  
  
-   Can be referenced as the target of an output cursor parameter in an EXECUTE statement if the cursor variable does not have a cursor currently assigned to it.  
  
-   Should be regarded as a pointer to the cursor.  
  
## Examples  
  
### A. Using DECLARE  
 The following example uses a local variable named `@find` to retrieve contact information for all last names beginning with `Man`.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @find VARCHAR(30);   
/* Also allowed:   
DECLARE @find VARCHAR(30) = 'Man%';   
*/  
SET @find = 'Man%';   
SELECT p.LastName, p.FirstName, ph.PhoneNumber  
FROM Person.Person AS p   
JOIN Person.PersonPhone AS ph ON p.BusinessEntityID = ph.BusinessEntityID  
WHERE LastName LIKE @find;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
LastName            FirstName               Phone
------------------- ----------------------- -------------------------
Manchepalli         Ajay                    1 (11) 500 555-0174
Manek               Parul                   1 (11) 500 555-0146
Manzanares          Tomas                   1 (11) 500 555-0178
  
(3 row(s) affected)
```  
  
### <a name="b-using-declare-with-two-variables"></a>B. 使用 DECLARE 與兩個變數  
 下列範例會擷取在北美洲銷售地區且年度銷售額至少 $2,000,000 的 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 銷售代表姓名。  
  
```sql  
USE AdventureWorks2012;  
GO  
SET NOCOUNT ON;  
GO  
DECLARE @Group nvarchar(50), @Sales MONEY;  
SET @Group = N'North America';  
SET @Sales = 2000000;  
SET NOCOUNT OFF;  
SELECT FirstName, LastName, SalesYTD  
FROM Sales.vSalesPerson  
WHERE TerritoryGroup = @Group and SalesYTD >= @Sales;  
```  
  
### <a name="c-declaring-a-variable-of-type-table"></a>C. 宣告類型資料表的變數  
 下列範例會建立一個 `table` 變數來儲存 UPDATE 陳述式的 OUTPUT 子句所指定的值。 之後的兩個 `SELECT` 陳述式會傳回 `@MyTableVar` 中的值，以及 `Employee` 資料表中更新作業的結果。 請注意，`INSERTED.ModifiedDate` 資料行中的結果不同於 `Employee` 資料表中 `ModifiedDate` 資料行的值。 這是因為將 `AFTER UPDATE` 值更新成目前日期的 `ModifiedDate` 觸發程序是定義在 `Employee` 資料表上。 不過，從 `OUTPUT` 傳回的資料行會反映引發觸發程序之前的資料。 如需詳細資訊，請參閱 [OUTPUT 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md)。  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar TABLE(  
    EmpID INT NOT NULL,  
    OldVacationHours INT,  
    NewVacationHours INT,  
    ModifiedDate DATETIME);  
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
  
### <a name="d-declaring-a-variable-of-user-defined-table-type"></a>D. 宣告使用者定義資料表類型的變數  
 下列範例會建立資料表值參數或稱為 `@LocationTVP` 的資料表變數。 這需要稱為 `LocationTableType` 的對應使用者定義資料表類型。 如需有關如何建立使用者定義資料表類型的詳細資訊，請參閱 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)。 如需詳細資訊，請參閱[使用資料表值參數 &#40;Database Engine&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)。  
  
```sql  
DECLARE @LocationTVP   
AS LocationTableType;  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-declare"></a>E. 使用 DECLARE  
 下列範例會利用名稱為 `@find` 的本機變數來擷取開頭是 `Walt` 的所有姓氏的連絡資訊。  
  
```sql  
-- Uses AdventureWorks  
  
DECLARE @find VARCHAR(30);  
/* Also allowed:   
DECLARE @find VARCHAR(30) = 'Man%';  
*/  
SET @find = 'Walt%';  
  
SELECT LastName, FirstName, Phone  
FROM DimEmployee   
WHERE LastName LIKE @find;  
```  
  
### <a name="f-using-declare-with-two-variables"></a>F. 使用 DECLARE 與兩個變數  
 下列範例會擷取使用變數來指定 `DimEmployee` 資料表中員工的名字和姓氏。  
  
```sql  
-- Uses AdventureWorks  
  
DECLARE @lastName VARCHAR(30), @firstName VARCHAR(30);  
  
SET @lastName = 'Walt%';  
SET @firstName = 'Bryan';  
  
SELECT LastName, FirstName, Phone  
FROM DimEmployee   
WHERE LastName LIKE @lastName AND FirstName LIKE @firstName;  
```  
  
## <a name="see-also"></a>另請參閱  
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [內建函數 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [table &#40;Transact-SQL&#41;](../../t-sql/data-types/table-transact-sql.md)   
 [比較具類型的 XML 與不具類型的 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)  
  
  




