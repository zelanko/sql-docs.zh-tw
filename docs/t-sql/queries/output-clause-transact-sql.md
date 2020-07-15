---
title: OUTPUT 子句 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/14/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OUTPUT_TSQL
- OUTPUT
dev_langs:
- TSQL
helpviewer_keywords:
- displaying updated rows
- INSERT statement [SQL Server], OUTPUT clause
- outputs [SQL Server]
- OUTPUT clause
- row additions [SQL Server], OUTPUT clause
- viewing updated rows
- row deletions [SQL Server], OUTPUT clause
- viewing deleted rows
- DELETE statement [SQL Server], OUTPUT clause
- row updates [SQL Server]
- displaying inserted rows
- viewing inserted rows
- displaying deleted rows
- UPDATE statement [SQL Server], OUTPUT clause
ms.assetid: 41b9962c-0c71-4227-80a0-08fdc19f5fe4
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 4b4eb7bcfc5711d041a354f4187e506ee130a0ea
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85706030"
---
# <a name="output-clause-transact-sql"></a>OUTPUT 子句 (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  從 INSERT、UPDATE、DELETE 或 MERGE 陳述式所影響的每個資料列傳回資訊，或傳回以 INSERT、UPDATE、DELETE 或 MERGE 陳述式所影響的每個資料列為基礎的運算式。 這些結果可以傳回給負責處理的應用程式，以便用在確認訊息、封存或其他這類應用程式需求等用途上。 這些結果也可以插入資料表或資料表變數中。 此外，您也可以在巢狀 INSERT、UPDATE、DELETE 或 MERGE 陳述式中擷取 OUTPUT 子句的結果，並將這些結果插入目標資料表或檢視中。  
  
> [!NOTE]  
>  具有 OUTPUT 子句的 UPDATE、INSERT 或 DELETE 陳述式會將資料列傳回用戶端，即使當陳述式遇到錯誤且回復時，也是如此。 如果當您執行此陳述式時發生任何錯誤，就不應該使用此結果。  
  
 **用於：**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [INSERT](../../t-sql/statements/insert-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 [MERGE](../../t-sql/statements/merge-transact-sql.md)  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
  
<OUTPUT_CLAUSE> ::=  
{  
    [ OUTPUT <dml_select_list> INTO { @table_variable | output_table } [ ( column_list ) ] ]  
    [ OUTPUT <dml_select_list> ]  
}  
<dml_select_list> ::=  
{ <column_name> | scalar_expression } [ [AS] column_alias_identifier ]  
    [ ,...n ]  
  
<column_name> ::=  
{ DELETED | INSERTED | from_table_name } . { * | column_name }  
    | $action  
```  
  
## <a name="arguments"></a>引數  
 \@*table_variable*  
 指定 **table** 變數以將傳回的資料列插入其中，而不傳回給呼叫端。 \@*table_variable* 必須在 INSERT、UPDATE、DELETE 或 MERGE 陳述式之前宣告。  
  
 如果未指定 *column_list*，**table** 變數的資料行數就必須與 OUTPUT 結果集的資料行數相同。 識別和計算資料行例外，它們必須被略過。 如果指定 *column_list*，任何省略的資料行都必須允許 Null 值或已具有指派的預設值。  
  
 如需有關使用 **table** 變數的詳細資訊，請參閱 [table &#40;Transact-SQL&#41;](../../t-sql/data-types/table-transact-sql.md)。  
  
 *output_table*  
 指定資料表，讓傳回的資料列插入其中，而不要傳回給呼叫端。 *output_table* 可以是暫存資料表。  
  
 如果未指定 *column_list*，資料表的資料行數就必須與 OUTPUT 結果集的資料行數相同。 識別和計算資料行例外。 它們必須被略過。 如果指定 *column_list*，任何省略的資料行都必須允許 Null 值或已具有指派的預設值。  
  
 *output_table* 無法：  
  
-   啟用它所定義的觸發程序。  
  
-   參與 FOREIGN KEY 條件約束的任何一端。  
  
-   有 CHECK 條件約束或啟用的規則。  
  
*column_list*  
 這是一份 INTO 子句目標資料表的資料行名稱選用清單。 它類似於 [INSERT](../../t-sql/statements/insert-transact-sql.md) 陳述式中所允許使用的資料行清單。  
  
 *scalar_expression*  
 這是會評估得出單一值的符號和運算子的任何組合。 *scalar_expression* 中不允許使用彙總函數。  
  
 任何指向修改的資料表中之資料行的參考，都必須用 INSERTED 或 DELETED 前置詞來限定。  
  
 *column_alias_identifier*  
 這是用來參考資料行名稱的替代名稱。  
  
 DELETED  
 這是一個資料行前置詞，用來指定更新或刪除作業所刪除的值。 前置詞是 DELETED 的資料行反映 UPDATE、DELETE 或 MERGE 陳述式完成之前的值。  
  
 DELETED 不能用來搭配使用 INSERT 陳述式中的 OUTPUT 子句。  
  
 INSERTED  
 這是一個資料行前置詞，用來指定插入或更新作業所加入的值。 前置詞是 INSERTED 的資料行反映 UPDATE、INSERT 或 MERGE 陳述式完成之後、觸發程序執行之前的值。  
  
 INSERTED 不能用來搭配使用 DELETE 陳述式中的 OUTPUT 子句。  
  
 *from_table_name*  
 這是一個資料行前置詞，用來指定在指定要更新或刪除的資料列時所用的 DELETE、UPDATE 或 MERGE 陳述式之 FROM 子句所包括的資料表。  
  
 如果 FROM 子句也指定了所修改的資料表，任何指向這份資料表中之資料行的參考，都必須用 INSERTED 或 DELETED 前置詞來限定。  
  
 \*  
 指定刪除、插入或更新動作所影響的所有資料行，都依照它們在資料表中的順序傳回。  
  
 例如，下列 DELETE 陳述式中的 `OUTPUT DELETED.*` 會傳回從 `ShoppingCartItem` 資料表中刪除的所有資料行：  
  
```  
DELETE Sales.ShoppingCartItem  
    OUTPUT DELETED.*;  
```  
  
 *column_name*  
 這是一個明確的資料行參考。 指向正經修改之資料表的任何參考，都必須由 INSERTED 或 DELETED 前置詞來適當地加以限定，例如：INSERTED **.** _column\_name_。  
  
 $action  
 僅適用於 MERGE 陳述式。 在 MERGE 陳述式的 OUTPUT 子句中指定類型為 **navchar(10)** 的資料行，傳回每個資料列下列三個值中的其中一個：'INSERT'、'UPDATE' 或 'DELETE'，根據在該資料列執行的動作而定。  
  
## <a name="remarks"></a>備註  
 您可在單一 INSERT、UPDATE、DELETE 或 MERGE 陳述式中，定義 OUTPUT \<dml_select_list> 子句和 OUTPUT \<dml_select_list> INTO { **\@** _table\_variable_ | _output\_table_ } 子句。  
  
> [!NOTE]  
>  除非另有指定，否則，指向 OUTPUT 子句的參考會同時參考 OUTPUT 子句和 OUTPUT INTO 子句。  
  
 在 INSERT 或 UPDATE 作業之後擷取識別或計算資料行值時，OUTPUT 子句可能很有用。  
  
 當 \<dml_select_list> 包括計算資料行時，輸出資料表或資料表變數中對應的資料行並不是計算資料行。 新資料行中的值是執行陳述式時所計算的值。  
  
 資料表套用變更的順序以及資料列插入輸出資料表或資料表變數的順序，並無法保證能夠對應。  
  
 如果是在 UPDATE 陳述式中修改參數或變數，OUTPUT 子句一律會傳回執行陳述式之前的參數或變數值，而不是修改的值。  
  
 您可以搭配位於使用 WHERE CURRENT OF 語法的資料指標之 UPDATE 或 DELETE 陳述式來使用 OUTPUT。  
  
 下列陳述式不支援 OUTPUT 子句：  
  
-   參考本機資料分割檢視、分散式資料分割檢視或遠端資料表的 DML 陳述式。  
  
-   包含 EXECUTE 陳述式的 INSERT 陳述式。  
  
-   當資料庫相容性層級設定為 100 時，OUTPUT 子句中不允許使用全文檢索述詞。  
  
-   OUTPUT INTO 子句不能用來插入檢視表或資料列集函數中。  
  
-   如果使用者定義函數包含的 OUTPUT INTO 子句中有資料表當做其目標，就無法建立此函數。  
  
 若要避免不具決定性的行為，OUTPUT 子句不能包含下列參考：  
  
-   執行使用者或系統資料存取或假設會執行這類存取的子查詢或使用者定義函數。 會假設使用者定義函數可執行資料存取 (如果這些函數未繫結結構描述)。  
  
-   當檢視表或嵌入資料表值函式中的資料行是由下列其中一種方法所定義時：  
  
    -   子查詢。  
  
    -   執行使用者或系統資料存取的使用者定義函數，或假設會執行這類存取的使用者定義函數。  
  
    -   包含使用者定義函數的計算資料行，而該函數會在其定義中執行使用者或系統資料存取。  
  
     當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 OUTPUT 子句中偵測到這類資料行時，就會引發錯誤 4186。   
  
## <a name="inserting-data-returned-from-an-output-clause-into-a-table"></a>將從 OUTPUT 子句傳回的資料插入至資料表  
 當您要擷取巢狀 INSERT、UPDATE、DELETE 或 MERGE 陳述式中 OUTPUT 子句的結果，並且將這些結果插入目標資料表時，請記住下列資訊：  
  
-   整個作業是不可部分完成的。 不是 INSERT 陳述式和包含 OUTPUT 子句的巢狀 DML 陳述式都可以執行，就是整個陳述式都失敗。  
  
-   下列限制適用於外部 INSERT 陳述式的目標：  
  
    -   此目標不得為遠端資料表、檢視或通用資料表運算式。  
  
    -   此目標不得具有 FOREIGN KEY 條件約束，或由 FOREIGN KEY 條件約束所參考。  
  
    -   不得針對此目標定義觸發程序。  
  
    -   此目標不得參與合併式複寫或是異動複寫的可更新訂閱。  
  
-   下列限制適用於巢狀 DML 陳述式：  
  
    -   此目標不得為遠端資料表或資料分割檢視。  
  
    -   來源本身不可包含 \<dml_table_source> 子句。  
  
-   OUTPUT INTO 子句不支援含有 \<dml_table_source> 子句的 INSERT 陳述式。  
  
-   \@\@ROWCOUNT 只會傳回外部 INSERT 陳述式所插入的資料列。  
  
-   \@\@IDENTITY、SCOPE_IDENTITY 和 IDENT_CURRENT 只會傳回巢狀 DML 陳述式所產生的識別值，而不會傳回外部 INSERT 陳述式所產生的識別值。  
  
-   查詢通知會將此陳述式視為單一實體，而且所建立的任何訊息類型都將成為巢狀 DML 的類型，即使重大變更來自外部 INSERT 陳述式本身也一樣。  
  
-   在 \<dml_table_source> 子句中，SELECT 和 WHERE 子句不可包含子查詢、彙總函式、次序函數、全文檢索述詞、執行資料存取的使用者定義函數或 TEXTPTR 函數。  

## <a name="parallelism"></a>平行處理原則
 會將結果傳回給用戶端的 OUTPUT 子句一律是使用序列計劃。

在相容性層級設定為 130 或更高的資料庫環境中，如果 INSERT...SELECT 作業針對 SELECT 陳述式使用 WITH (TABLOCK) 提示，同時也使用 OUTPUT...INTO 來插入至暫存資料表或使用者資料表，則視子樹成本而定，INSERT...SELECT 的目標資料表將會適用平行處理原則。  OUTPUT INTO 子句中參考的目標資料表將不適用平行處理原則。 
 
## <a name="triggers"></a>觸發程序  
 從 OUTPUT 傳回的資料行會反映在 INSERT、UPDATE 或 DELETE 陳述式完成之後執行觸發程序之前的資料。  
  
 如果是 INSTEAD OF 觸發程序，便會依照實際發生 INSERT、UPDATE 或 DELETE 的情況來產生傳回的結果，即使觸發程序作業結果並沒有進行任何修改也是如此。 如果在觸發程序主體內使用包括 OUTPUT 子句的陳述式，就必須利用資料表別名來參考觸發程序 inserted 和 deleted 資料表，以避免與 OUTPUT 相關聯的 INSERTED 的 DELETED 資料表有重複的資料行參考。  
  
 如果指定了 OUTPUT 子句，但並未同時指定 INTO 關鍵字，DML 作業的目標便不能針對給定的 DML 動作來定義任何已啟用的觸發程序。 例如，如果在 UPDATE 陳述式中定義 OUTPUT 子句，目標資料表便不能有任何已啟用的 UPDATE 觸發程序。  
  
 如果設定了 sp_configure 選項 disallow results from triggers，當從觸發程序內叫用不含 INTO 子句的 OUTPUT 子句時，它會使陳述式失敗。  
  
## <a name="data-types"></a>資料類型  
 OUTPUT 子句支援大型物件資料類型：**nvarchar(max)** 、**varchar(max)** 、**varbinary(max)** 、**text**、**ntext**、**image** 及 **xml**。 當您在 UPDATE 陳述式中使用 .WRITE 子句來修改 **nvarchar(max)** 、**varchar(max)** 或 **varbinary(max)** 資料行時，如果參考了值完整的先後影像，便會傳回這些影像。 在 OUTPUT 子句之 **text**、**ntext** 或 **image** 資料行的運算式中，不能出現 TEXTPTR( ) 函數。  
  
## <a name="queues"></a>佇列  
 您可以在利用資料表做為佇列的應用程式中使用 OUTPUT，也可以利用它來存放中繼結果集。 也就是說，應用程式會不斷新增或移除資料表的資料列。 下列範例會利用 DELETE 陳述式中的 OUTPUT 子句，將刪除的資料列傳回發出呼叫的應用程式。  
  
```  
USE AdventureWorks2012;  
GO  
DELETE TOP(1) dbo.DatabaseLog WITH (READPAST)  
OUTPUT deleted.*  
WHERE DatabaseLogID = 7;  
GO  
  
```  
  
 這個範例會以單一動作從用作佇列的資料表中移除資料列，再將刪除的值傳回負責處理的應用程式。 另外，也可能實作其他語意，如利用資料表來實作堆疊。 不過，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並無法保證使用 OUTPUT 子句的 DML 陳述式處理和傳回資料列的順序。 應用程式負責決定是否併入適當的 WHERE 子句來保證所需要的語意，或了解當多個資料列可能符合 DML 作業的資格時，並無法保證順序。 下列範例會使用子查詢，且假設唯一性是 `DatabaseLogID` 資料行的特性，以便實作所需要的排序語意。  
  
```  
USE tempdb;  
GO  
CREATE TABLE dbo.table1  
(  
    id INT,  
    employee VARCHAR(32)  
);  
GO  
  
INSERT INTO dbo.table1 VALUES   
      (1, 'Fred')  
     ,(2, 'Tom')  
     ,(3, 'Sally')  
     ,(4, 'Alice');  
GO  
  
DECLARE @MyTableVar TABLE  
(  
    id INT,  
    employee VARCHAR(32)  
);  
  
PRINT 'table1, before delete'   
SELECT * FROM dbo.table1;  
  
DELETE FROM dbo.table1  
OUTPUT DELETED.* INTO @MyTableVar  
WHERE id = 4 OR id = 2;  
  
PRINT 'table1, after delete'  
SELECT * FROM dbo.table1;  
  
PRINT '@MyTableVar, after delete'  
SELECT * FROM @MyTableVar;  
  
DROP TABLE dbo.table1;  
  
--Results  
--table1, before delete  
--id          employee  
------------- ------------------------------  
--1           Fred  
--2           Tom  
--3           Sally  
--4           Alice  
--  
--table1, after delete  
--id          employee  
------------- ------------------------------  
--1           Fred  
--3           Sally  
--@MyTableVar, after delete  
--id          employee  
------------- ------------------------------  
--2           Tom  
--4           Alice  
  
```  
  
> [!NOTE]  
>  如果您的狀況允許多個應用程式執行單一資料表的破壞性讀取，請在 UPDATE 和 DELETE 陳述式中使用 READPAST 資料表提示。 這可以防止當另一個應用程式已在讀取資料表中第一個符合的記錄時，所可能出現的鎖定問題。  
  
## <a name="permissions"></a>權限  
 在透過 \<dml_select_list> 擷取或在 \<scalar_expression> 中使用的所有資料行上，必須要有 SELECT 權限。  
  
 在 \<output_table> 中指定的所有資料表上，必須要有 INSERT 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-output-into-with-a-simple-insert-statement"></a>A. 使用 OUTPUT INTO 搭配簡單的 INSERT 陳述式  
 下列範例會將資料列插入至 `ScrapReason` 資料表中，然後使用 `OUTPUT` 子句將陳述式的結果傳回給 `@MyTableVar``table` 變數。 由於 `ScrapReasonID` 資料行定義了 IDENTITY 屬性，因此，`INSERT` 陳述式並未指定這個資料行的值。 不過請注意，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 針對這個資料行所產生的值，會在 `OUTPUT` 資料行之 `inserted.ScrapReasonID` 子句中傳回。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table( NewScrapReasonID smallint,  
                           Name varchar(50),  
                           ModifiedDate datetime);  
INSERT Production.ScrapReason  
    OUTPUT INSERTED.ScrapReasonID, INSERTED.Name, INSERTED.ModifiedDate  
        INTO @MyTableVar  
VALUES (N'Operator error', GETDATE());  
  
--Display the result set of the table variable.  
SELECT NewScrapReasonID, Name, ModifiedDate FROM @MyTableVar;  
--Display the result set of the table.  
SELECT ScrapReasonID, Name, ModifiedDate   
FROM Production.ScrapReason;  
GO  
  
```  
  
### <a name="b-using-output-with-a-delete-statement"></a>B. 使用 OUTPUT 搭配 DELETE 陳述式  
 下列範例會刪除 `ShoppingCartItem` 資料表中的所有資料列。 `OUTPUT deleted.*` 子句指定將 `DELETE` 陳述式的結果，也就是已刪除之資料列中的所有資料行，傳回給發出呼叫的應用程式。 後面的 `SELECT` 陳述式會驗證 `ShoppingCartItem` 資料表刪除作業的結果。  
  
```  
USE AdventureWorks2012;  
GO  
DELETE Sales.ShoppingCartItem  
OUTPUT DELETED.*   
WHERE ShoppingCartID = 20621;  
  
--Verify the rows in the table matching the WHERE clause have been deleted.  
SELECT COUNT(*) AS [Rows in Table] FROM Sales.ShoppingCartItem WHERE ShoppingCartID = 20621;  
GO  
  
```  
  
### <a name="c-using-output-into-with-an-update-statement"></a>C. 使用 OUTPUT INTO 搭配 UPDATE 陳述式  
 下列範例會將 `VacationHours` 資料表前 10 個資料列的 `Employee` 資料行更新 25%。 `OUTPUT` 子句會將在 `deleted.VacationHours` 資料行中套用 `UPDATE` 陳述式之前便已存在的 `VacationHours` 值，以及 `inserted.VacationHours` 資料行中更新的值傳回給 `@MyTableVar` 資料表變數。  
  
 之後的兩個 `SELECT` 陳述式會傳回 `@MyTableVar` 中的值，以及 `Employee` 資料表中更新作業的結果。  
  
```  
USE AdventureWorks2012;  
GO  
  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    OldVacationHours int,  
    NewVacationHours int,  
    ModifiedDate datetime);  
  
UPDATE TOP (10) HumanResources.Employee  
SET VacationHours = VacationHours * 1.25,  
    ModifiedDate = GETDATE()   
OUTPUT inserted.BusinessEntityID,  
       deleted.VacationHours,  
       inserted.VacationHours,  
       inserted.ModifiedDate  
INTO @MyTableVar;  
  
--Display the result set of the table variable.  
SELECT EmpID, OldVacationHours, NewVacationHours, ModifiedDate  
FROM @MyTableVar;  
GO  
--Display the result set of the table.  
SELECT TOP (10) BusinessEntityID, VacationHours, ModifiedDate  
FROM HumanResources.Employee;  
GO  
  
```  
  
### <a name="d-using-output-into-to-return-an-expression"></a>D. 使用 OUTPUT INTO 來傳回運算式  
 下列範例是以範例 C 為基礎所建立，它在 `OUTPUT` 子句中定義一個運算式，當做更新的 `VacationHours` 值和套用更新之前的 `VacationHours` 值之間的差異。 此運算式的值會傳回給 `VacationHoursDifference` 資料行中的 `@MyTableVar``table` 變數。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    OldVacationHours int,  
    NewVacationHours int,  
    VacationHoursDifference int,  
    ModifiedDate datetime);  
  
UPDATE TOP (10) HumanResources.Employee  
SET VacationHours = VacationHours * 1.25,  
    ModifiedDate = GETDATE()  
OUTPUT inserted.BusinessEntityID,  
       deleted.VacationHours,  
       inserted.VacationHours,  
       inserted.VacationHours - deleted.VacationHours,  
       inserted.ModifiedDate  
INTO @MyTableVar;  
  
--Display the result set of the table variable.  
SELECT EmpID, OldVacationHours, NewVacationHours,   
    VacationHoursDifference, ModifiedDate  
FROM @MyTableVar;  
GO  
SELECT TOP (10) BusinessEntityID, VacationHours, ModifiedDate  
FROM HumanResources.Employee;  
GO  
  
```  
  
### <a name="e-using-output-into-with-from_table_name-in-an-update-statement"></a>E. 在 UPDATE 陳述式中，使用 OUTPUT INTO 搭配 from_table_name  
 下列範例會針對具有指定 `ProductID` 和 `ScrapReasonID` 的所有工單，更新 `WorkOrder` 資料表中的 `ScrapReasonID` 資料行。 `OUTPUT INTO` 子句會從更新的資料表 (`WorkOrder`) 傳回值，也會從 `Product` 傳回值。 `Product` 子句利用 `FROM` 資料表來指定要更新的資料列。 由於 `WorkOrder` 資料表定義了 `AFTER UPDATE` 觸發程序，因此，需要 `INTO` 關鍵字。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTestVar table (  
    OldScrapReasonID int NOT NULL,   
    NewScrapReasonID int NOT NULL,   
    WorkOrderID int NOT NULL,  
    ProductID int NOT NULL,  
    ProductName nvarchar(50)NOT NULL);  
  
UPDATE Production.WorkOrder  
SET ScrapReasonID = 4  
OUTPUT deleted.ScrapReasonID,  
       inserted.ScrapReasonID,   
       inserted.WorkOrderID,  
       inserted.ProductID,  
       p.Name  
    INTO @MyTestVar  
FROM Production.WorkOrder AS wo  
    INNER JOIN Production.Product AS p   
    ON wo.ProductID = p.ProductID   
    AND wo.ScrapReasonID= 16  
    AND p.ProductID = 733;  
  
SELECT OldScrapReasonID, NewScrapReasonID, WorkOrderID,   
    ProductID, ProductName   
FROM @MyTestVar;  
GO  
  
```  
  
### <a name="f-using-output-into-with-from_table_name-in-a-delete-statement"></a>F. 在 DELETE 陳述式中，使用 OUTPUT INTO 搭配 from_table_name  
 下列範例根據 `ProductProductPhoto` 陳述式的 `FROM` 子句所定義的搜尋準則，來刪除 `DELETE` 資料表中的資料列。 `OUTPUT` 子句會傳回所刪除的資料表資料行 (`deleted.ProductID`、`deleted.ProductPhotoID`) 及 `Product` 資料表中的資料行。 `FROM` 子句利用這份資料表來指定要刪除的資料列。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table (  
    ProductID int NOT NULL,   
    ProductName nvarchar(50)NOT NULL,  
    ProductModelID int NOT NULL,   
    PhotoID int NOT NULL);  
  
DELETE Production.ProductProductPhoto  
OUTPUT DELETED.ProductID,  
       p.Name,  
       p.ProductModelID,  
       DELETED.ProductPhotoID  
    INTO @MyTableVar  
FROM Production.ProductProductPhoto AS ph  
JOIN Production.Product as p   
    ON ph.ProductID = p.ProductID   
    WHERE p.ProductModelID BETWEEN 120 and 130;  
  
--Display the results of the table variable.  
SELECT ProductID, ProductName, ProductModelID, PhotoID   
FROM @MyTableVar  
ORDER BY ProductModelID;  
GO  
  
```  
  
### <a name="g-using-output-into-with-a-large-object-data-type"></a>G. 使用 OUTPUT INTO 搭配大型物件資料類型  
 下列範例會利用 `DocumentSummary` 子句，來更新 `nvarchar(max)` (`Production.Document` 資料表中的 `.WRITE` 資料行) 中的部分值。 `components` 一字藉由指定用來取代的文字、現有資料中要被取代之文字的起始位置 (位移)，以及要取代的字元數 (長度) 來取代為 `features` 一字。 此範例會使用 `OUTPUT` 子句，將 `DocumentSummary` 資料行的先後影像傳回給 `@MyTableVar``table` 變數。 請注意，它會傳回 `DocumentSummary` 資料行之完整的先後影像。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table (  
    SummaryBefore nvarchar(max),  
    SummaryAfter nvarchar(max));  
  
UPDATE Production.Document  
SET DocumentSummary .WRITE (N'features',28,10)  
OUTPUT deleted.DocumentSummary,   
       inserted.DocumentSummary   
    INTO @MyTableVar  
WHERE Title = N'Front Reflector Bracket Installation';  
  
SELECT SummaryBefore, SummaryAfter   
FROM @MyTableVar;  
GO  
  
```  
  
### <a name="h-using-output-in-an-instead-of-trigger"></a>H. 在 INSTEAD OF 觸發程序中使用 OUTPUT  
 下列範例會利用觸發程序中的 `OUTPUT` 子句來傳回觸發程序作業的結果。 首先在 `ScrapReason` 資料表上建立檢視，然後在此檢視上定義 `INSTEAD OF INSERT` 觸發程序，只讓使用者修改基底資料表的 `Name` 資料行。 由於 `ScrapReasonID` 資料行是基底資料表中的 `IDENTITY` 資料行，觸發程序會忽略使用者提供的值。 這使 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 能夠自動產生正確的值。 另外，使用者提供的 `ModifiedDate` 值會被忽略，且會設為目前的日期。 `OUTPUT` 子句會傳回實際插入 `ScrapReason` 資料表的值。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('dbo.vw_ScrapReason','V') IS NOT NULL  
    DROP VIEW dbo.vw_ScrapReason;  
GO  
CREATE VIEW dbo.vw_ScrapReason  
AS (SELECT ScrapReasonID, Name, ModifiedDate  
    FROM Production.ScrapReason);  
GO  
CREATE TRIGGER dbo.io_ScrapReason   
    ON dbo.vw_ScrapReason  
INSTEAD OF INSERT  
AS  
BEGIN  
--ScrapReasonID is not specified in the list of columns to be inserted   
--because it is an IDENTITY column.  
    INSERT INTO Production.ScrapReason (Name, ModifiedDate)  
        OUTPUT INSERTED.ScrapReasonID, INSERTED.Name,   
               INSERTED.ModifiedDate  
    SELECT Name, getdate()  
    FROM inserted;  
END  
GO  
INSERT vw_ScrapReason (ScrapReasonID, Name, ModifiedDate)  
VALUES (99, N'My scrap reason','20030404');  
GO  
  
```  
  
 以下是 2004 年 4 月 12 日 ('`2004-04-12'`) 所產生的結果集。 請注意，`ScrapReasonIDActual` 和 `ModifiedDate` 資料行反映了觸發程序作業所產生的值，而不是 `INSERT` 陳述式所提供的值。  
  
 ```
 ScrapReasonID  Name             ModifiedDate  
 -------------  ---------------- -----------------------  
 17             My scrap reason  2004-04-12 16:23:33.050
 ```  
  
### <a name="i-using-output-into-with-identity-and-computed-columns"></a>I. 使用 OUTPUT INTO 搭配識別和計算資料行  
 下列範例會建立 `EmployeeSales` 資料表，之後再利用含有 `INSERT` 陳述式的 `SELECT` 陳述式來擷取來源資料表中的資料，以插入幾個資料列。 `EmployeeSales` 資料表包含一個識別欄位 (`EmployeeID`) 和一個計算資料行 (`ProjectedSales`)。  
  
```  
USE AdventureWorks2012 ;  
GO  
IF OBJECT_ID ('dbo.EmployeeSales', 'U') IS NOT NULL  
    DROP TABLE dbo.EmployeeSales;  
GO  
CREATE TABLE dbo.EmployeeSales  
( EmployeeID   int IDENTITY (1,5)NOT NULL,  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  CurrentSales money NOT NULL,  
  ProjectedSales AS CurrentSales * 1.10   
);  
GO  
DECLARE @MyTableVar table(  
  EmployeeID   int NOT NULL,  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  CurrentSales money NOT NULL,  
  ProjectedSales money NOT NULL  
  );  
  
INSERT INTO dbo.EmployeeSales (LastName, FirstName, CurrentSales)  
  OUTPUT INSERTED.EmployeeID,
         INSERTED.LastName,   
         INSERTED.FirstName,   
         INSERTED.CurrentSales,
         INSERTED.ProjectedSales
  INTO @MyTableVar  
    SELECT c.LastName, c.FirstName, sp.SalesYTD  
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.BusinessEntityID LIKE '2%'  
    ORDER BY c.LastName, c.FirstName;  
  
SELECT EmployeeID, LastName, FirstName, CurrentSales, ProjectedSales  
FROM @MyTableVar;  
GO  
SELECT EmployeeID, LastName, FirstName, CurrentSales, ProjectedSales  
FROM dbo.EmployeeSales;  
GO  
  
```  
  
### <a name="j-using-output-and-output-into-in-a-single-statement"></a>J. 在單一陳述式中使用 OUTPUT 和 OUTPUT INTO  
 下列範例根據 `ProductProductPhoto` 陳述式的 `FROM` 子句所定義的搜尋準則，來刪除 `DELETE` 資料表中的資料列。 `OUTPUT INTO` 子句會將所要刪除之資料表中的資料行 (`deleted.ProductID`、`deleted.ProductPhotoID`) 及 `Product` 資料表中的資料行傳回給 `@MyTableVar``table` 變數。 `Product` 子句利用 `FROM` 資料表來指定要刪除的資料列。 `OUTPUT` 子句會將 `deleted.ProductID`、`deleted.ProductPhotoID` 資料行及從 `ProductProductPhoto` 資料表中刪除資料列的日期和時間，傳回給發出呼叫的應用程式。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table (  
    ProductID int NOT NULL,   
    ProductName nvarchar(50)NOT NULL,  
    ProductModelID int NOT NULL,   
    PhotoID int NOT NULL);  
  
DELETE Production.ProductProductPhoto  
OUTPUT DELETED.ProductID,  
       p.Name,  
       p.ProductModelID,  
       DELETED.ProductPhotoID  
    INTO @MyTableVar  
OUTPUT DELETED.ProductID, DELETED.ProductPhotoID, GETDATE() AS DeletedDate   
FROM Production.ProductProductPhoto AS ph  
JOIN Production.Product as p   
    ON ph.ProductID = p.ProductID   
WHERE p.ProductID BETWEEN 800 and 810;  
  
--Display the results of the table variable.  
SELECT ProductID, ProductName, PhotoID, ProductModelID   
FROM @MyTableVar;  
GO  
  
```  
  
### <a name="k-inserting-data-returned-from-an-output-clause"></a>K. 插入從 OUTPUT 子句傳回的資料  
 下列範例將擷取從 `OUTPUT` 陳述式的 `MERGE` 子句中傳回的資料，並將該資料插入另一個資料表中。 `MERGE` 陳述式會根據在 `Quantity` 資料表中處理的順序，每天更新 `ProductInventory` 資料表的 `SalesOrderDetail` 資料行。 它也會刪除產品存貨降到 `0` 或以下的資料列。 此範例會擷取已刪除的資料列，並將其插入另一個資料表 `ZeroInventory`，該資料表會追蹤沒有存貨的產品。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Production.ZeroInventory', N'U') IS NOT NULL  
    DROP TABLE Production.ZeroInventory;  
GO  
--Create ZeroInventory table.  
CREATE TABLE Production.ZeroInventory (DeletedProductID int, RemovedOnDate DateTime);  
GO  
  
INSERT INTO Production.ZeroInventory (DeletedProductID, RemovedOnDate)  
SELECT ProductID, GETDATE()  
FROM  
(   MERGE Production.ProductInventory AS pi  
    USING (SELECT ProductID, SUM(OrderQty) FROM Sales.SalesOrderDetail AS sod  
           JOIN Sales.SalesOrderHeader AS soh  
           ON sod.SalesOrderID = soh.SalesOrderID  
           AND soh.OrderDate = '20070401'  
           GROUP BY ProductID) AS src (ProductID, OrderQty)  
    ON (pi.ProductID = src.ProductID)  
    WHEN MATCHED AND pi.Quantity - src.OrderQty <= 0  
        THEN DELETE  
    WHEN MATCHED  
        THEN UPDATE SET pi.Quantity = pi.Quantity - src.OrderQty  
    OUTPUT $action, deleted.ProductID) AS Changes (Action, ProductID)  
WHERE Action = 'DELETE';  
IF @@ROWCOUNT = 0  
PRINT 'Warning: No rows were inserted';  
GO  
SELECT DeletedProductID, RemovedOnDate FROM Production.ZeroInventory;  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [table &#40;Transact-SQL&#41;](../../t-sql/data-types/table-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
