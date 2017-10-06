---
title: "宣告@local_variable(TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 76
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 70decceb0fb5bc34f5ac7a32c64ca80cb0977de2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="declare-localvariable-transact-sql"></a>宣告@local_variable(TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  變數是利用 DECLARE 陳述式宣告在批次或程序的主體中，並利用 SET 或 SELECT 陳述式來指派值。 資料指標變數可以是利用這個陳述式來宣告，且可以搭配其他與資料指標相關的陳述式來使用。 在宣告之後，所有變數都會初始化成 NULL，除非在宣告中有提供值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
DECLARE   
{   
    { @local_variable [AS] data_type  | [ = value ] }  
  | { @cursor_variable_name CURSOR }  
} [,...n]   
| { @table_variable_name [AS] <table_type_definition> }   
  
<table_type_definition> ::=   
     TABLE ( { <column_definition> | <table_constraint> } [ ,... ] )   
  
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
     { { PRIMARY KEY | UNIQUE } ( column_name [ ,... ] )   
     | CHECK ( search_condition )   
     }   
  
<index_option> ::=  
See CREATE TABLE for index option syntax.  
  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DECLARE   
{{ @local_variable [AS] data_type } [ =value [ COLLATE <collation_name> ] ] } [,...n]  
  
```  
  
## <a name="arguments"></a>引數  
@*local_variable*  
 此為變數的名稱。 變數名稱的開頭必須是 at (@) 符號。 本機變數名稱必須遵守的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。  
  
*data_type*  
 這是任何系統提供的 Common Language Runtime (CLR) 使用者定義資料表類型或別名資料類型。 變數不能是**文字**， **ntext**，或**映像**資料型別。  
  
 如需有關系統資料類型的詳細資訊，請參閱[資料類型 &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/data-types-transact-sql.md). 如需有關 CLR 使用者定義型別或別名資料類型的詳細資訊，請參閱[CREATE TYPE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-type-transact-sql.md).  
  
 =*值*  
 以內嵌方式指派值給變數。 此值可以是常數或運算式，但是它必須符合變數宣告類型，或是必須可隱含轉換成該類型。 如需詳細資訊，請參閱[運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
@*cursor_variable_name*  
 這是資料指標變數的名稱。 資料指標變數名稱的開頭必須是 at (@) 符號，且必須符合識別碼的規則。  
  
CURSOR  
 指定變數是本機資料指標變數。  
  
@*table_variable_name*  
 類型的變數名稱**資料表**。 變數名稱的開頭必須是 at (@) 符號，且必須符合識別碼的規則。  
  
<table_type_definition>  
定義**資料表**資料型別。 資料表宣告包括資料行定義、名稱、資料類型和條件約束。 允許使用的條件約束類型只有 PRIMARY KEY、UNIQUE、NULL 和 CHECK。 如果規則或預設定義繫結至別名資料類型，就無法利用別名資料類型來當做資料行純量資料類型。
  
\<table_type_definiton > 是用來建立資料表中定義資料表的資訊子集。 這裡包括元素和必要定義。 如需詳細資訊，請參閱 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)。  
  
 *n*  
 這是一個預留位置，表示可以指定多個變數，且可以指派這些變數的值。 當您宣告**資料表**變數**資料表**變數必須是 DECLARE 陳述式所宣告的唯一變數。  
  
 *column_name*  
 這是資料表中之資料行的名稱。  
  
 *scalar_data_type*  
 指定資料行是一種純量資料類型。  
  
 *computed_column_expression*  
 這是定義計算資料行值的運算式。 它是從運算式中，利用相同資料表中其他資料行計算而得。 例如，計算資料行可以有定義**成本**AS**價格\*qty**。運算式可以是非計算的資料行名稱、常數、內建函數、變數，或是一個或多個運算子所連接之這些項目的任何組合。 運算式不能是子查詢或使用者定義函數。 運算式不能參考 CLR 使用者定義類型。  
  
 [自動分頁*sys.databases*]  
 指定資料行的定序。 *sys.databases*可以是 Windows 定序名稱或 SQL 定序名稱，而且只適用於資料行的**char**， **varchar**，**文字****nchar**， **nvarchar**，和**ntext**資料型別。 若未指定，便會將使用者定義資料類型的定序指派給這個資料行 (如果資料行是使用者定義資料類型)，否則，便會指派目前資料庫的定序。  
  
 如需有關 Windows 和 SQL 定序名稱的詳細資訊，請參閱[COLLATE &#40;TRANSACT-SQL &#41;](~/t-sql/statements/collations.md).  
  
 DEFAULT  
 指定在插入期間未明確提供值時，提供給資料行的值。 可以套用 DEFAULT 定義，除了那些定義為任何資料行**時間戳記**或含有 IDENTITY 屬性。 當卸除資料表時，便會移除 DEFAULT 定義。 預設值只能使用常數值 (如字元字串)、系統函數 (如 SYSTEM_USER()) 或 NULL。 若要維護與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的相容性，您可以將條件約束名稱指派給 DEFAULT。  
  
 *constant_expression*  
 這是用來當做資料行預設值的常數、NULL 或系統函數。  
  
 IDENTITY  
 指出新資料行是識別欄位。 當新資料列加入資料表時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會提供資料行的唯一累加值。 識別欄位通常用來結合 PRIMARY KEY 條件約束一起使用，當做資料表的唯一資料列識別碼。 IDENTITY 屬性可以指派給**tinyint**， **smallint**， **int**， **decimal(p,0)**，或**numeric(p,0)**資料行。 每份資料表都只能建立一個識別欄位。 繫結的預設值和 DEFAULT 條件約束無法搭配識別欄位使用。 您必須同時指定種子和遞增，或同時不指定這兩者。 如果同時不指定這兩者，預設值便是 (1,1)。  
  
 *種子*  
 這是載入資料表的第一個資料列所用的值。  
  
 *遞增*  
 這是加入先前載入的資料列之識別值的累加值。  
  
 ROWGUIDCOL  
 指出新資料行是一個資料列全域唯一識別碼資料行。 只有一個**uniqueidentifier**每個資料表的資料行可以指定為 ROWGUIDCOL 資料行。 ROWGUIDCOL 屬性指派給只**uniqueidentifier**資料行。  
  
 NULL | NOT NULL  
 指出變數中是否允許 null。 預設值是 NULL。  
  
 PRIMARY KEY  
 這是一個條件約束，它利用唯一索引來強制執行一個或多個給定資料行的實體完整性。 每份資料表都只能建立一個 PRIMARY KEY 條件約束。  
  
 UNIQUE  
 這是一個條件約束，它利用唯一索引來提供一個或多個給定資料行的實體完整性。 一份資料表可以有多個 UNIQUE 條件約束。  
  
 CHECK  
 這是一個條件約束，藉由限制可能輸入一個或多個資料行的值，強制執行範圍完整性。  
  
 *logical_expression*  
 這是一個傳回 TRUE 或 FALSE 的邏輯運算式。  
  
## <a name="remarks"></a>備註  
 批次或程序通常會利用變數來當做 WHILE、LOOP 或 IF...ELSE 區塊的計數器。  
  
 變數只能用在運算式中，不能用來取代物件名稱或關鍵字。 若要建構動態 SQL 陳述式，請使用 EXECUTE。  
  
 本機變數的範圍是宣告它的批次。  
 
 資料表變數不一定是記憶體駐留。 記憶體不足的壓力，屬於資料表變數的頁面可以推送到 tempdb。
  
 下列陳述式可以將目前指派了資料指標的資料指標變數當做一項來源來參考：  
  
-   CLOSE 陳述式。  
  
-   DEALLOCATE 陳述式。  
  
-   FETCH 陳述式。  
  
-   OPEN 陳述式。  
  
-   定位 DELETE 或 UPDATE 陳述式。  
  
-   SET CURSOR 變數陳述式 (在右側)。  
  
 在所有的這些陳述式中，如果參考的資料指標變數存在，但目前未配置資料指標給它，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 便會引發錯誤。 如果所參考的資料指標變數不存在，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 便會產生其他類型之未宣告的變數所產生的相同錯誤。  
  
 資料指標變數：  
  
-   可以是資料指標類型或另一個資料指標變數的目標。 如需詳細資訊，請參閱[設定@local_variable&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md).  
  
-   如果資料指標變數目前未指派任何資料指標，就可以在 EXECUTE 陳述式中，將它當做輸出資料指標參數的目標來參考。  
  
-   應該視為指向資料指標的指標。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-declare"></a>A. 使用 DECLARE  
 下列範例會利用名稱為 `@find` 的本機變數來擷取開頭是 `Man` 的所有姓氏的連絡資訊。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @find varchar(30);   
/* Also allowed:   
DECLARE @find varchar(30) = 'Man%';   
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
 下列範例會擷取在北美銷售地區且年度銷售額至少 $2,000,000 的 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 銷售代表姓名。  
  
```  
USE AdventureWorks2012;  
GO  
SET NOCOUNT ON;  
GO  
DECLARE @Group nvarchar(50), @Sales money;  
SET @Group = N'North America';  
SET @Sales = 2000000;  
SET NOCOUNT OFF;  
SELECT FirstName, LastName, SalesYTD  
FROM Sales.vSalesPerson  
WHERE TerritoryGroup = @Group and SalesYTD >= @Sales;  
```  
  
### <a name="c-declaring-a-variable-of-type-table"></a>C. 宣告類型資料表的變數  
 下列範例會建立一個 `table` 變數來儲存 UPDATE 陳述式的 OUTPUT 子句所指定的值。 之後的兩個 `SELECT` 陳述式會傳回 `@MyTableVar` 中的值，以及 `Employee` 資料表中更新作業的結果。 請注意，在結果`INSERTED.ModifiedDate`資料行中值的不同`ModifiedDate`中的資料行`Employee`資料表。 這是因為將 `AFTER UPDATE` 值更新成目前日期的 `ModifiedDate` 觸發程序是定義在 `Employee` 資料表上。 不過，從 `OUTPUT` 傳回的資料行會反映引發觸發程序之前的資料。 如需詳細資訊，請參閱[OUTPUT 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/output-clause-transact-sql.md).  
  
```  
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
  
### <a name="d-declaring-a-variable-of-user-defined-table-type"></a>D. 宣告使用者定義資料表類型的變數  
 下列範例會建立資料表值參數或稱為 `@LocationTVP` 的資料表變數。 這需要稱為 `LocationTableType` 的對應使用者定義資料表類型。 如需如何建立使用者定義資料表類型的詳細資訊，請參閱[CREATE TYPE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-type-transact-sql.md). 如需有關資料表值參數的詳細資訊，請參閱[使用資料表值參數 &#40; Database engine&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)。  
  
```  
DECLARE @LocationTVP   
AS LocationTableType;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-declare"></a>E. 使用 DECLARE  
 下列範例會利用名稱為 `@find` 的本機變數來擷取開頭是 `Walt` 的所有姓氏的連絡資訊。  
  
```  
-- Uses AdventureWorks  
  
DECLARE @find varchar(30);  
/* Also allowed:   
DECLARE @find varchar(30) = 'Man%';  
*/  
SET @find = 'Walt%';  
  
SELECT LastName, FirstName, Phone  
FROM DimEmployee   
WHERE LastName LIKE @find;  
```  
  
### <a name="f-using-declare-with-two-variables"></a>F. 使用 DECLARE 與兩個變數  
 下列範例會擷取使用變數來指定員工的名字和姓氏名稱`DimEmployee`資料表。  
  
```  
-- Uses AdventureWorks  
  
DECLARE @lastName varchar(30), @firstName varchar(30);  
  
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
 [資料表 &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/table-transact-sql.md)   
 [比較具類型的 XML 與不具類型的 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)  
  
  





