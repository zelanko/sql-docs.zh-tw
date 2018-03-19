---
title: MERGE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- MERGE
- MERGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- updating data [SQL Server]
- modifying data [SQL Server], MERGE statement
- MERGE statement [SQL Server]
- adding data
- DML [SQL Server], MERGE statement
- table modifications [SQL Server], MERGE statement
- data manipulation language [SQL Server], MERGE statement
- inserting data
ms.assetid: c17996d6-56a6-482f-80d8-086a3423eecc
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: dd8ecb3609dd70516023afe84125252c708ad1ad
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="merge-transact-sql"></a>MERGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  根據與來源資料表聯結的結果，在目標資料表上執行插入、更新或刪除作業。 例如，您可以根據在另一個資料表中所找到的差異在資料表中插入、更新或刪除資料列，以同步處理兩個資料表。  
  
 **效能提示：**當兩個資料表有複雜的比對特性時，MERGE 陳述式的條件式行為表現最佳。 例如沒有資料列時插入資料列，或資料列相符時更新資料列。 只要根據另一個資料表的資料列更新資料表，基本 INSERT、 UPDATE 及 DELETE 陳述式就能提升效能及可調適性。 例如：  
  
```  
INSERT tbl_A (col, col2)  
SELECT col, col2   
FROM tbl_B   
WHERE NOT EXISTS (SELECT col FROM tbl_A A2 WHERE A2.col = tbl_B.col);  
```  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
[ WITH <common_table_expression> [,...n] ]  
MERGE   
    [ TOP ( expression ) [ PERCENT ] ]   
    [ INTO ] <target_table> [ WITH ( <merge_hint> ) ] [ [ AS ] table_alias ]  
    USING <table_source>   
    ON <merge_search_condition>  
    [ WHEN MATCHED [ AND <clause_search_condition> ]  
        THEN <merge_matched> ] [ ...n ]  
    [ WHEN NOT MATCHED [ BY TARGET ] [ AND <clause_search_condition> ]  
        THEN <merge_not_matched> ]  
    [ WHEN NOT MATCHED BY SOURCE [ AND <clause_search_condition> ]  
        THEN <merge_matched> ] [ ...n ]  
    [ <output_clause> ]  
    [ OPTION ( <query_hint> [ ,...n ] ) ]      
;  
  
<target_table> ::=  
{   
    [ database_name . schema_name . | schema_name . ]  
  target_table  
}  
  
<merge_hint>::=  
{  
    { [ <table_hint_limited> [ ,...n ] ]  
    [ [ , ] INDEX ( index_val [ ,...n ] ) ] }  
}  
  
<table_source> ::=   
{  
    table_or_view_name [ [ AS ] table_alias ] [ <tablesample_clause> ]   
        [ WITH ( table_hint [ [ , ]...n ] ) ]   
  | rowset_function [ [ AS ] table_alias ]   
        [ ( bulk_column_alias [ ,...n ] ) ]   
  | user_defined_function [ [ AS ] table_alias ]  
  | OPENXML <openxml_clause>   
  | derived_table [ AS ] table_alias [ ( column_alias [ ,...n ] ) ]   
  | <joined_table>   
  | <pivoted_table>   
  | <unpivoted_table>   
}  
  
<merge_search_condition> ::=  
    <search_condition>  
  
<merge_matched>::=  
    { UPDATE SET <set_clause> | DELETE }  
  
<set_clause>::=  
SET  
  { column_name = { expression | DEFAULT | NULL }  
  | { udt_column_name.{ { property_name = expression  
                        | field_name = expression }  
                        | method_name ( argument [ ,...n ] ) }  
    }  
  | column_name { .WRITE ( expression , @Offset , @Length ) }  
  | @variable = expression  
  | @variable = column = expression  
  | column_name { += | -= | *= | /= | %= | &= | ^= | |= } expression  
  | @variable { += | -= | *= | /= | %= | &= | ^= | |= } expression  
  | @variable = column { += | -= | *= | /= | %= | &= | ^= | |= } expression  
  } [ ,...n ]   
  
<merge_not_matched>::=  
{  
    INSERT [ ( column_list ) ]   
        { VALUES ( values_list )  
        | DEFAULT VALUES }  
}  
  
<clause_search_condition> ::=  
    <search_condition>  
  
<search condition> ::=  
    { [ NOT ] <predicate> | ( <search_condition> ) }   
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition> ) } ]   
[ ,...n ]   
  
<predicate> ::=   
    { expression { = | < > | ! = | > | > = | ! > | < | < = | ! < } expression   
    | string_expression [ NOT ] LIKE string_expression   
  [ ESCAPE 'escape_character' ]   
    | expression [ NOT ] BETWEEN expression AND expression   
    | expression IS [ NOT ] NULL   
    | CONTAINS   
  ( { column | * } , '< contains_search_condition >' )   
    | FREETEXT ( { column | * } , 'freetext_string' )   
    | expression [ NOT ] IN ( subquery | expression [ ,...n ] )   
    | expression { = | < > | ! = | > | > = | ! > | < | < = | ! < }   
  { ALL | SOME | ANY} ( subquery )   
    | EXISTS ( subquery ) }   
  
<output_clause>::=  
{  
    [ OUTPUT <dml_select_list> INTO { @table_variable | output_table }  
        [ (column_list) ] ]  
    [ OUTPUT <dml_select_list> ]  
}  
  
<dml_select_list>::=  
    { <column_name> | scalar_expression }   
        [ [AS] column_alias_identifier ] [ ,...n ]  
  
<column_name> ::=  
    { DELETED | INSERTED | from_table_name } . { * | column_name }  
    | $action  
```  
  
## <a name="arguments"></a>引數  
 WITH \<common_table_expression>  
 指定在 MERGE 陳述式範圍內定義的暫存具名結果集或檢視表，也稱為通用資料表運算式。 結果集是從簡單查詢衍生而來，由 MERGE 陳述式參考。 如需詳細資訊，請參閱 [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)。  
  
 TOP ( *expression* ) [ PERCENT ]  
 指定受到影響的資料列數目或百分比。 *expression* 可以是一個數字，也可以是資料列的百分比。 TOP 運算式中參考的資料列並不會依任何順序排列。 如需詳細資訊，請參閱 [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md)。  
  
 當整個來源資料表和整個目標資料表聯結在一起，而且不符合插入、更新或刪除動作的聯結資料列移除之後，才會套用 TOP 子句。 TOP 子句會進一步將聯結的資料列數減少為指定的值，而且插入、更新或刪除動作會依照未排序的方式套用到剩餘的聯結資料列。 也就是說，將資料列散發到 WHEN 子句中定義的動作時，沒有任何特定順序。 例如，指定 TOP (10) 會影響 10 個資料列；在這些資料列中，可能會更新 7 個及插入 3 個，或者可能會刪除 1 個、更新 5 個及插入 4 個，依此類推。  
  
 因為 MERGE 陳述式會針對來源和目標資料表執行完整資料表掃描，所以當使用 TOP 子句，藉由建立多個批次來修改大型資料表時，I/O 效能可能會受到影響。 在此狀況中，請務必確保所有後續批次都是以新的資料列為目標。  
  
 *database_name*  
 這是 *target_table* 所在的資料庫名稱。  
  
 *schema_name*  
 這是 *target_table* 所屬的結構描述名稱。  
  
 *target_table*  
 這是資料表或檢視表，\<table_source> 的資料列會根據 \<clause_search_condition>，對此資料表或檢視進行比對。 *target_table* 是 MERGE 陳述式的 WHEN 子句所指定之任何插入、更新或刪除作業的目標。  
  
 如果 *target_table* 是檢視，則對其進行的任何動作都必須滿足更新檢視的條件。 如需詳細資訊，請參閱[透過檢視修改資料](../../relational-databases/views/modify-data-through-a-view.md)。  
  
 *target_table* 不能是遠端資料表。 *target_table* 不能有任何定義的規則。  
  
 [ AS ] *table_alias*  
 這是用於參考資料表的替代名稱。  
  
 USING \<table_source>  
 指定根據 \<merge_search condition>，與 *target_table* 的資料列進行比對的資料來源。 此項比對的結果會指定 MERGE 陳述式的 WHEN 子句所採取的動作。 \<table_source> 可以是遠端資料表或存取遠端資料表的衍生資料表。 
  
 \<table_source> 可以是使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] [資料表值建構函式](../../t-sql/queries/table-value-constructor-transact-sql.md)的衍生資料表，藉由指定多個資料列來建構資料表。  
  
 如需有關此子句語法和引數的詳細資訊，請參閱 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)。  
  
 ON \<merge_search_condition>  
 指定條件，在這些條件下，\<table_source> 會與 *target_table* 聯結以決定其相符之處。 
  
> [!CAUTION]  
>  請務必只從目標資料表指定用於比對用途的資料行； 也就是說，從目標資料表中指定要與來源資料表的對應資料行進行比較的資料行。 請勿嘗試在 ON 子句中篩選出目標資料表的資料列 (例如指定 `AND NOT target_table.column_x = value`) 來改善查詢效能。 這樣做可能會傳回非預期且不正確的結果。  
  
 WHEN MATCHED THEN \<merge_matched>  
 指定所有符合 \<table_source> ON \<merge_search_condition> 傳回的資料列且滿足任何其他搜尋條件的 *target_table* 資料列，都會根據 \<merge_matched> 子句更新或刪除。  
  
 MERGE 陳述式最多可以具有兩個 WHEN MATCHED 子句。 如果指定兩個子句，則第一個子句必須附帶 AND \<search_condition> 子句。 對於任何給定資料列，只有第一個 WHEN MATCHED 子句未套用時，才會套用第二個 WHEN MATCHED 子句。 如果有兩個 WHEN MATCHED 子句，則一個必須指定 UPDATE 動作，另一個則必須指定 DELETE 動作。 如果在 \<merge_matched> 子句中指定 UPDATE，而且根據 \<merge_search_condition>，有一個以上的 \<table_source> 資料列符合 *target_table* 的資料列，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回錯誤。 MERGE 陳述式無法更新同一資料列一次以上或更新及刪除同一資料列。  
  
 WHEN NOT MATCHED [ BY TARGET ] THEN \<merge_not_matched>  
 指定由 \<table_source> ON \<merge_search_condition> 傳回的每一資料列若不符合 *target_table* 的資料列但卻滿足其他的搜尋條件 (若存在)，就會在 *target_table* 中插入一個資料列。 插入的值是由 \<merge_not_matched> 子句決定。 MERGE 陳述式只能具有一個 WHEN NOT MATCHED 子句。  
  
 WHEN NOT MATCHED BY SOURCE THEN \<merge_matched>  
 指定所有不符合 \<table_source> ON \<merge_search_condition> 傳回的資料列，卻能滿足任何其他搜尋條件的 *target_table* 資料列，都會根據 \<merge_matched> 子句更新或刪除。  
  
 MERGE 陳述式最多可以具有兩個 WHEN NOT MATCHED BY SOURCE 子句。 如果指定兩個子句，則第一個子句必須附帶 AND \<clause_search_condition> 子句。 對於任何給定資料列，只有第一個 WHEN NOT MATCHED BY SOURCE 子句未套用時，才會套用第二個 WHEN NOT MATCHED BY SOURCE 子句。 如果有兩個 WHEN NOT MATCHED BY SOURCE 子句，則一個必須指定 UPDATE 動作，另一個則必須指定 DELETE 動作。 只有目標資料表中的資料行才可以在 \<clause_search_condition> 中參考。  
  
 當 \<table_source> 未傳回任何資料列時，就無法存取來源資料表的資料行。 如果 \<merge_matched> 子句所指定的更新或刪除動作參考了來源資料表的資料行，就會傳回錯誤 207 (資料行名稱無效)。 例如，子句 `WHEN NOT MATCHED BY SOURCE THEN UPDATE SET TargetTable.Col1 = SourceTable.Col1` 可能會導致陳述式失敗，因為無法存取來源資料表的 `Col1`。  
  
 AND \<clause_search_condition>  
 指定任何有效的搜尋條件。 如需詳細資訊，請參閱[搜尋條件 &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md)。  
  
 \<table_hint_limited>  
 指定針對每個由 MERGE 陳述式所執行的插入、更新或刪除動作，套用到目標資料表的一個或多個資料表提示。 WITH 關鍵字和括號都是必要的。  
  
 不允許使用 NOLOCK 和 READUNCOMMITTED。 如需有關資料表提示的詳細資訊，請參閱[資料表提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)。  
  
 指定 INSERT 陳述式目標資料表之 TABLOCK 提示的效果，與指定 TABLOCKX 提示相同。 獨佔鎖定是在資料表上取得的。 有指定 FORCESEEK 時，該提示會套用到與來源資料表聯結之目標資料表的隱含執行個體。  
  
> [!CAUTION]  
>  使用 WHEN NOT MATCHED [ BY TARGET ] THEN INSERT 指定 READPAST 可能會導致違反 UNIQUE 條件約束的 INSERT 作業。  
  
 INDEX ( index_val [ ,...n ] )  
 在目標資料表上指定一個或多個索引的名稱或識別碼，以用於與來源資料表執行隱含聯結。 如需詳細資訊，請參閱[資料表提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)。  
  
 \<output_clause>  
 針對 *target_table* 中每個更新、插入或刪除的資料列傳回一個資料列 (不依特定順序)。 您可以在輸出子句中指定 **$action**。 **$action** 是 **nvarchar(10)** 類型的資料行，會針對每一個資料列傳回以下三個值的其中一個：'INSERT'、'UPDATE' 或 'DELETE' (根據該資料列上執行的動作而定)。 如需有關此子句引數的詳細資訊，請參閱 [OUTPUT 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md)。  
  
 OPTION ( \<query_hint> [ ,...n ] )  
 指定利用最佳化工具提示來自訂 Database Engine 處理陳述式的方式。 如需詳細資訊，請參閱[查詢提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)。  
  
 \<merge_matched>  
 指定所有不符合 \<table_source> ON \<merge_search_condition> 傳回的資料列、但卻滿足任何其他搜尋條件的 *target_table* 資料列，所會套用的更新或刪除動作。  
  
 UPDATE SET \<set_clause>  
 指定要在目標資料表中更新的資料行或變數名稱清單，以及用於更新這些名稱的值。  
  
 如需有關此子句引數的詳細資訊，請參閱 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)。 不允許將變數設定為與資料行相同的值。  
  
 Delete  
 指定符合 *target_table* 資料列的資料列會遭到刪除。  
  
 \<merge_not_matched>  
 指定要插入目標資料表的值。  
  
 (*column_list*)  
 這是要插入資料的一個或多個目標資料表資料行的清單。 必須將資料行指定為單一部分名稱，否則 MERGE 陳述式會失敗。 *column_list* 必須括在括弧中，並以逗號分隔。  
  
 VALUES ( *values_list*)  
 這是以逗號分隔的常數、變數或運算式清單，這些項目會傳回要插入目標資料表的值。 運算式不能包含 EXECUTE 陳述式。  
  
 DEFAULT VALUES  
 強制插入的資料列包含定義給每個資料行的預設值。  
  
 如需此子句的詳細資訊，請參閱 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)。  
  
 \<search condition>  
 指定用來指定 \<merge_search_condition> 或 \<clause_search_condition> 的搜尋條件。 如需有關此子句之引數的詳細資訊，請參閱[搜尋條件 &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md)。  
  
## <a name="remarks"></a>Remarks  
 必須至少指定三個 MATCHED 子句中的一個，但可依任何順序指定這些子句。 在同一個 MATCHED 子句中，不能更新變數一次以上。  
  
 在目標資料表上由 MERGE 陳述式所指定的任何插入、更新或刪除動作，都受限於資料表上定義的任何條件約束，包括任何串聯式參考完整性條件約束。 如果在目標資料表上將任何唯一索引的 IGNORE_DUP_KEY 設定為 ON，則 MERGE 會忽略此設定。  
  
 MERGE 陳述式需要使用分號 (;) 做為陳述式結束字元。 若 MERGE 陳述式執行時缺少該結束字元，就會引發錯誤 10713。  
  
 如果用在 MERGE 之後，[@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md) 會將插入、更新和刪除的資料列總數傳回用戶端。  
  
 當資料庫相容性層級設定為 100 或更高時，MERGE 是完全保留的關鍵字。 雖然 MERGE 陳述式也可以在 90 和 100 資料庫相容性層級底下使用，但是當資料庫相容性層級設定為 90 時，此關鍵字並不會完全保留。  
  
 使用佇列更新複寫時，不應該使用 **MERGE** 陳述式。 **MERGE** 與佇列更新觸發程序不相容。 請將 **MERGE** 陳述式取代成 Insert 或 Update 陳述式。  
  
## <a name="trigger-implementation"></a>觸發程序實作  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會針對 MERGE 陳述式中指定的每個插入、更新或刪除動作，引發目標資料表上定義的對應 AFTER 觸發程序，但並不能保證哪一個動作會最先或最後引發觸發程序。 為相同動作所定義的觸發程序會接受您指定的順序。 如需有關設定觸發程序引發順序的詳細資訊，請參閱[指定第一個及最後一個觸發程序](../../relational-databases/triggers/specify-first-and-last-triggers.md)。  
  
 如果針對 MERGE 陳述式所執行的插入、更新或刪除動作在目標資料表上定義啟用的 INSTEAD OF 觸發程序，則 MERGE 陳述式中指定的所有動作在目標資料表上都必須啟用 INSTEAD OF 觸發程序。  
  
 如果在 *target_table* 上定義了任何 INSTEAD OF UPDATE 或 INSTEAD OF DELETE 觸發程序，則不會執行更新或刪除作業。 反而會引發觸發程序，並據此填入 **inserted** 和 **deleted** 資料表。  
  
 如果在 *target_table* 上定義任何 INSTEAD OF INSERT 觸發程序，則不會執行插入作業。 反而會引發觸發程序，並據此填入 **inserted** 資料表。  
  
## <a name="permissions"></a>Permissions  
 來源資料表需要 SELECT 權限，目標資料表則需要 INSERT、UPDATE 或 DELETE 權限。 如需詳細資訊，請參閱 [SELECT](../../t-sql/queries/select-transact-sql.md)、[INSERT](../../t-sql/statements/insert-transact-sql.md)、[UPDATE](../../t-sql/queries/update-transact-sql.md) 和 [DELETE](../../t-sql/statements/delete-transact-sql.md) 主題中的＜權限＞一節。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-merge-to-perform-insert-and-update-operations-on-a-table-in-a-single-statement"></a>A. 以單一陳述式使用 MERGE 在資料表上執行 INSERT 和 UPDATE 作業  
 如果符合的資料列存在，常見的狀況是在資料表中更新一個或多個資料行；如果符合的資料列不存在，則將資料當做新資料列插入。 這通常是透過將參數傳遞到包含適當 UPDATE 和 INSERT 陳述式的預存程序來完成。 您可以利用 MERGE 陳述式，在單一陳述式中同時執行兩個工作。 以下範例示範 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中同時包含 INSERT 陳述式和 UPDATE 陳述式的預存程序。 接著，程序會經過修改，以便使用單一 MERGE 陳述式來執行等同的作業。  
  
```  
CREATE PROCEDURE dbo.InsertUnitMeasure  
    @UnitMeasureCode nchar(3),  
    @Name nvarchar(25)  
AS   
BEGIN  
    SET NOCOUNT ON;  
-- Update the row if it exists.      
    UPDATE Production.UnitMeasure  
SET Name = @Name  
WHERE UnitMeasureCode = @UnitMeasureCode  
-- Insert the row if the UPDATE statement failed.  
IF (@@ROWCOUNT = 0 )  
BEGIN  
    INSERT INTO Production.UnitMeasure (UnitMeasureCode, Name)  
    VALUES (@UnitMeasureCode, @Name)  
END  
END;  
GO  
-- Test the procedure and return the results.  
EXEC InsertUnitMeasure @UnitMeasureCode = 'ABC', @Name = 'Test Value';  
SELECT UnitMeasureCode, Name FROM Production.UnitMeasure  
WHERE UnitMeasureCode = 'ABC';  
GO  
  
-- Rewrite the procedure to perform the same operations using the 
-- MERGE statement.  
-- Create a temporary table to hold the updated or inserted values 
-- from the OUTPUT clause.  
CREATE TABLE #MyTempTable  
    (ExistingCode nchar(3),  
     ExistingName nvarchar(50),  
     ExistingDate datetime,  
     ActionTaken nvarchar(10),  
     NewCode nchar(3),  
     NewName nvarchar(50),  
     NewDate datetime  
    );  
GO  
ALTER PROCEDURE dbo.InsertUnitMeasure  
    @UnitMeasureCode nchar(3),  
    @Name nvarchar(25)  
AS   
BEGIN  
    SET NOCOUNT ON;  
  
    MERGE Production.UnitMeasure AS target  
    USING (SELECT @UnitMeasureCode, @Name) AS source (UnitMeasureCode, Name)  
    ON (target.UnitMeasureCode = source.UnitMeasureCode)  
    WHEN MATCHED THEN   
        UPDATE SET Name = source.Name  
WHEN NOT MATCHED THEN  
    INSERT (UnitMeasureCode, Name)  
    VALUES (source.UnitMeasureCode, source.Name)  
    OUTPUT deleted.*, $action, inserted.* INTO #MyTempTable;  
END;  
GO  
-- Test the procedure and return the results.  
EXEC InsertUnitMeasure @UnitMeasureCode = 'ABC', @Name = 'New Test Value';  
EXEC InsertUnitMeasure @UnitMeasureCode = 'XYZ', @Name = 'Test Value';  
EXEC InsertUnitMeasure @UnitMeasureCode = 'ABC', @Name = 'Another Test Value';  
  
SELECT * FROM #MyTempTable;  
-- Cleanup   
DELETE FROM Production.UnitMeasure WHERE UnitMeasureCode IN ('ABC','XYZ');  
DROP TABLE #MyTempTable;  
GO  
```  
  
### <a name="b-using-merge-to-perform-update-and-delete-operations-on-a-table-in-a-single-statement"></a>B. 以單一陳述式使用 MERGE 在資料表上執行 UPDATE 和 DELETE 作業  
 下列範例使用 MERGE，根據在 `ProductInventory` 資料表中處理的順序，每日更新 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 範例資料庫中的 `SalesOrderDetail` 資料表。 `Quantity` 資料表中的 `ProductInventory` 資料行會藉著減去 `SalesOrderDetail` 資料表中每個產品每日所下的訂單數量來進行更新。 如果產品的訂單數量使產品的存貨降為 0 或 0 以下，該產品的資料列就會從 `ProductInventory` 資料表中刪除。  
  
```  
CREATE PROCEDURE Production.usp_UpdateInventory  
    @OrderDate datetime  
AS  
MERGE Production.ProductInventory AS target  
USING (SELECT ProductID, SUM(OrderQty) FROM Sales.SalesOrderDetail AS sod  
    JOIN Sales.SalesOrderHeader AS soh  
    ON sod.SalesOrderID = soh.SalesOrderID  
    AND soh.OrderDate = @OrderDate  
    GROUP BY ProductID) AS source (ProductID, OrderQty)  
ON (target.ProductID = source.ProductID)  
WHEN MATCHED AND target.Quantity - source.OrderQty <= 0  
    THEN DELETE  
WHEN MATCHED   
    THEN UPDATE SET target.Quantity = target.Quantity - source.OrderQty,   
                    target.ModifiedDate = GETDATE()  
OUTPUT $action, Inserted.ProductID, Inserted.Quantity, 
    Inserted.ModifiedDate, Deleted.ProductID,  
    Deleted.Quantity, Deleted.ModifiedDate;  
GO  
  
EXECUTE Production.usp_UpdateInventory '20030501'  
```  
  
### <a name="c-using-merge-to-perform-update-and-insert-operations-on-a-target-table-by-using-a-derived-source-table"></a>C. 使用 MERGE 在目標資料表上透過衍生式來源資料表執行 UPDATE 和 INSERT 作業  
 以下範例會使用 MERGE，藉由更新或插入資料列來修改 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中的 `SalesReason` 資料表。 當來源資料表中的 `NewName` 值符合目標資料表 (`Name`) 中 `SalesReason` 資料行內的值時，就會更新目標資料表中的 `ReasonType` 資料行。 當 `NewName` 的值不相符時，來源資料列會插入目標資料表中。 來源資料表是一種衍生資料表，可使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 資料表值建構函式針對來源資料表指定多個資料列。 如需有關在衍生資料表中使用資料表值建構函式的詳細資訊，請參閱[資料表值建構函式 &#40;Transact-SQL&#41;](../../t-sql/queries/table-value-constructor-transact-sql.md)。 這個範例也示範如何將 OUTPUT 子句的結果儲存在資料表變數中，然後摘要列出 MERGE 陳述式的結果，其方式是執行簡單的選取作業來傳回已插入和更新的資料列計數。  
  
```  
-- Create a temporary table variable to hold the output actions.  
DECLARE @SummaryOfChanges TABLE(Change VARCHAR(20));  
  
MERGE INTO Sales.SalesReason AS Target  
USING (VALUES ('Recommendation','Other'), ('Review', 'Marketing'), 
              ('Internet', 'Promotion'))  
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
  
### <a name="d-inserting-the-results-of-the-merge-statement-into-another-table"></a>D. 將 MERGE 陳述式的結果插入另一個資料表  
 下列範例將擷取從 MERGE 陳述式的 OUTPUT 子句中傳回的資料，並將該資料插入另一個資料表中。 MERGE 陳述式會根據在 `Quantity` 資料表中處理的順序，來更新 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中 `ProductInventory` 資料表的 `SalesOrderDetail` 資料行。 此範例會擷取已更新的資料列，並將其插入另一個資料表，該資料表是用於追蹤存貨變更。  
  
```  
CREATE TABLE Production.UpdatedInventory  
    (ProductID INT NOT NULL, LocationID int, NewQty int, PreviousQty int,  
     CONSTRAINT PK_Inventory PRIMARY KEY CLUSTERED (ProductID, LocationID));  
GO  
INSERT INTO Production.UpdatedInventory  
SELECT ProductID, LocationID, NewQty, PreviousQty   
FROM  
(    MERGE Production.ProductInventory AS pi  
     USING (SELECT ProductID, SUM(OrderQty)   
            FROM Sales.SalesOrderDetail AS sod  
            JOIN Sales.SalesOrderHeader AS soh  
            ON sod.SalesOrderID = soh.SalesOrderID  
            AND soh.OrderDate BETWEEN '20030701' AND '20030731'  
            GROUP BY ProductID) AS src (ProductID, OrderQty)  
     ON pi.ProductID = src.ProductID  
    WHEN MATCHED AND pi.Quantity - src.OrderQty >= 0   
        THEN UPDATE SET pi.Quantity = pi.Quantity - src.OrderQty  
    WHEN MATCHED AND pi.Quantity - src.OrderQty <= 0   
        THEN DELETE  
    OUTPUT $action, Inserted.ProductID, Inserted.LocationID, 
        Inserted.Quantity AS NewQty, Deleted.Quantity AS PreviousQty)  
 AS Changes (Action, ProductID, LocationID, NewQty, PreviousQty) 
 WHERE Action = 'UPDATE';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [OUTPUT 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md)   
 [Integration Services 套件中的 MERGE](../../integration-services/control-flow/merge-in-integration-services-packages.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [資料表值建構函式 &#40;Transact-SQL&#41;](../../t-sql/queries/table-value-constructor-transact-sql.md)  
  
  

