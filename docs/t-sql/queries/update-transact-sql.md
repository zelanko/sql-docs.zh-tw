---
title: "更新 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UPDATE_TSQL
- UPDATE
dev_langs: TSQL
helpviewer_keywords:
- DML [SQL Server], UPDATE statement
- data updates [SQL Server], UPDATE statement
- updating data [SQL Server]
- TOP clause, UPDATE
- OUTPUT clause
- large value data types
- data manipulation language [SQL Server], UPDATE statement
- user-defined types [SQL Server], modifying
- INSTEAD OF triggers
- modifying data [SQL Server], UPDATE statement
- data modifications [SQL Server], UPDATE statement
- large data, modifying
- .WRITE clause
- table modifications [SQL Server], UPDATE statement
- UDTs [SQL Server], modifying
- UPDATE statement [SQL Server], about UPDATE statement
- LOB data [SQL Server], modifying
- modifying LOB data
- UPDATE statement [SQL Server]
- FROM clause, UPDATE statement
- WHERE clause, UPDATE statement
ms.assetid: 40e63302-0c68-4593-af3e-6d190181fee7
caps.latest.revision: "91"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 1a739b230d39726367d54a64e7b2327f6a80f9ca
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/02/2018
---
# <a name="update-transact-sql"></a>UPDATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  變更 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 資料表或檢視表中現有的資料。 如需範例，請參閱[範例](#UpdateExamples)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
-- Syntax for SQL Server and Azure SQL Database  

[ WITH <common_table_expression> [...n] ]  
UPDATE   
    [ TOP ( expression ) [ PERCENT ] ]   
    { { table_alias | <object> | rowset_function_limited   
         [ WITH ( <Table_Hint_Limited> [ ...n ] ) ]  
      }  
      | @table_variable      
    }  
    SET  
        { column_name = { expression | DEFAULT | NULL }  
          | { udt_column_name.{ { property_name = expression  
                                | field_name = expression }  
                                | method_name ( argument [ ,...n ] )  
                              }  
          }  
          | column_name { .WRITE ( expression , @Offset , @Length ) }  
          | @variable = expression  
          | @variable = column = expression  
          | column_name { += | -= | *= | /= | %= | &= | ^= | |= } expression  
          | @variable { += | -= | *= | /= | %= | &= | ^= | |= } expression  
          | @variable = column { += | -= | *= | /= | %= | &= | ^= | |= } expression  
        } [ ,...n ]   
  
    [ <OUTPUT Clause> ]  
    [ FROM{ <table_source> } [ ,...n ] ]   
    [ WHERE { <search_condition>   
            | { [ CURRENT OF   
                  { { [ GLOBAL ] cursor_name }   
                      | cursor_variable_name   
                  }   
                ]  
              }  
            }   
    ]   
    [ OPTION ( <query_hint> [ ,...n ] ) ]  
[ ; ]  
  
<object> ::=  
{   
    [ server_name . database_name . schema_name .   
    | database_name .[ schema_name ] .   
    | schema_name .  
    ]  
    table_or_view_name}  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

UPDATE [ database_name . [ schema_name ] . | schema_name . ] table_name   
SET { column_name = { expression | NULL } } [ ,...n ]  
[ FROM from_clause ]  
[ WHERE <search_condition> ]   
[ OPTION ( LABEL = label_name ) ]  
[;]  
```  
  
## <a name="arguments"></a>引數  
 與\<common_table_expression >  
 指定定義在 UPDATE 陳述式範圍內的暫存具名結果集或檢視表，也稱為通用資料表運算式 (CTE)。 CTE 結果集是從簡單查詢衍生而來，由 UPDATE 陳述式來加以參考。  
  
 另外，一般資料表運算式也可以搭配 SELECT、INSERT、DELETE 和 CREATE VIEW 等陳述式來使用。 如需詳細資訊，請參閱[common_table_expression &#40; 與TRANSACT-SQL &#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 TOP **(** *運算式***)** [百分比]  
 指定的數字或更新資料列的百分比。 *expression* 可以是一個數字，也可以是資料列的百分比。  
  
 搭配 INSERT、UPDATE 或 DELETE 使用的 TOP 運算式所參考的資料列並不依照任何順序來排列。  
  
 括號分隔*運算式*在前必須在 INSERT、 UPDATE 和 DELETE 陳述式中。 如需詳細資訊，請參閱[TOP &#40;TRANSACT-SQL &#41;](../../t-sql/queries/top-transact-sql.md).  
  
 *table_alias*  
 在 FROM 子句中指定的別名，代表要更新資料列的資料表或檢視表。  
  
 *伺服器名稱*  
 是伺服器的名稱 (利用連結的伺服器名稱或[OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md)函數當做伺服器名稱) 的資料表或檢視所在。 如果*server_name*指定，則*database_name*和*schema_name*所需。  
  
 *database_name*  
 這是資料庫的名稱。  
  
 *schema_name*  
 這是資料表或檢視表所屬的結構描述名稱。  
  
 *table_or view_name*  
 這是要更新資料列之資料表或檢視表的名稱。 所參考的檢視*table_or_view_name*必須能夠更新，而且參考檢視的 FROM 子句中的一個基底資料表。 如需可更新檢視的詳細資訊，請參閱[CREATE VIEW &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-view-transact-sql.md).  
  
 *rowset_function_limited*  
 可能是[OPENQUERY](../../t-sql/functions/openquery-transact-sql.md)或[OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)函式，提供者功能而定。  
  
 與**(** \<Table_Hint_Limited > **)**  
 指定目標資料表允許使用的一個或多個資料表提示。 WITH 關鍵字和括號都是必要的。 不允許使用 NOLOCK 和 READUNCOMMITTED。 如需有關資料表提示的資訊，請參閱[資料表提示 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 @*table_variable*  
 指定[資料表](../../t-sql/data-types/table-transact-sql.md)變數當做資料表來源。  
  
 SET  
 指定要更新的資料行或變數名稱清單。  
  
 *column_name*  
 這是包含要變更之資料的資料行。 *column_name*必須存在於*table_or view_name*。 無法更新識別欄位。  
  
 *expression*  
 這是傳回單一值的變數、常值、運算式或子選取陳述式 (括在括號內)。 所傳回的值*運算式*會取代中的現有值*column_name*或 *@variable* 。  
  
> [!NOTE]  
>  參考 Unicode 字元資料類型時**nchar**， **nvarchar**，和**ntext**，'expression' 前面應該要有大寫字母 ' N '。 如果沒有指定 'N'，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將字串轉換成對應至資料庫預設定序或資料行的字碼頁。 在此字碼頁中找不到的任何字元都會遺失。  
  
 DEFAULT  
 指定資料行所定義的預設值要取代資料行中現有的值。 如果資料行沒有預設值，且定義成允許空值，您可以利用這個方式，將資料行改成 NULL。  
  
 { **+=** | **-=** | **\*=** | **/=** | **%=** | **&=** | **^=** | **|=** }  
 複合指派運算子：  
 + = 加入並指派  
 -= 減去並指派  
 * = 乘以並指派  
 / = 除以並指派  
 %= 模除並指派  
 & = 位元 AND 並指派  
 ^ = 位元 XOR 並指派  
 | = 位元 OR 並指派  
  
 *udt_column_name*  
 這是使用者自訂類型資料行。  
  
 *property_name* | *field_name*  
 這是使用者自訂類型的公用屬性或公用資料成員。  
  
 *method_name* **(** *引數*[ **，**...*n*] **)**  
 非靜態公用 mutator 方法*udt_column_name*接受一或多個引數。  
  
 **.**寫入**(***運算式***，***@Offset***，** *@Length***)**  
 指定值的區段*column_name*要修改。 *運算式*取代 *@Length* 單位從開始 *@Offset* 的*column_name*。 只有資料行的**varchar （max)**， **nvarchar （max)**，或**varbinary （max)**可以使用這個子句來指定。 *column_name*不能是 NULL，也不限定資料表名稱或資料表別名。  
  
 *運算式*是複製到的值*column_name*。 *運算式*必須評估成或能夠隱含地轉換成*column_name*型別。 如果*運算式*設為 NULL，  *@Length* 會被忽略中的值和*column_name*會截斷在指定 *@Offset*.  
  
 *@Offset*是起始點的值中*column_name*速率*運算式*寫入。 *@Offset*是以零為起始的序數位置，是**bigint**，且不能為負數。 如果 *@Offset* 是 NULL，更新作業將附加*運算式*結尾的現有*column_name*值和 *@Length*會被忽略。 如果@Offset大於的長度*column_name*值[!INCLUDE[ssDE](../../includes/ssde-md.md)]會傳回錯誤。 如果 *@Offset* 加上 *@Length* 超過資料行中的基礎值的結尾，就會刪除到最後一個字元的值。 如果 *@Offset* 再加上 LEN (*運算式*) 大於基礎宣告的大小，則會引發錯誤。  
  
 *@Length*資料行，從啟動中的區段長度 *@Offset* ，也就是取代*運算式*。 *@Length*是**bigint**且不能為負數。 如果 *@Length* 是 NULL，更新作業會移除所有資料從 *@Offset* 結尾*column_name*值。  
  
 如需詳細資訊，請參閱＜備註＞。  
  
 **@***變數*  
 宣告的變數設為所傳回的值*運算式*。  
  
 設定 **@** *變數* = *資料行* = *運算式*設定至相同的變數為資料行的值。 這有別於 SET  **@** *變數* = *資料行*，*資料行* =  *運算式*，它會設定變數來更新之前的資料行的值。  
  
 \<OUTPUT_Clause >  
 在 UPDATE 作業中，傳回更新資料或以更新資料為基礎的運算式。 任何目標是遠端資料表或檢視表的 DML 陳述式都不支援 OUTPUT 子句。 如需詳細資訊，請參閱[OUTPUT 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/output-clause-transact-sql.md).  
  
 從\<t >  
 指定利用資料表、檢視表或衍生資料表來源來提供更新作業的準則。 如需詳細資訊，請參閱 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)。  
  
 如果更新的物件與 FROM 子句中的物件相同，且只有一個參考指向 FROM 子句中的物件，就不一定要指定物件別名。 如果更新的物件在 FROM 子句中重複出現，就正好只有一個指向這個物件的參考不能指定資料表別名。 所有其他指向 FROM 子句中之物件的參考，都必須包括物件別名。  
  
 含有 INSTEAD OF UPDATE 觸發程序的檢視表不能是含有 FROM 子句之 UPDATE 的目標。  
  
> [!NOTE]  
>  FROM 子句中 OPENDATASOURCE、OPENQUERY 或 OPENROWSET 的任何呼叫都會與當做更新目標使用之這些函數的任何呼叫進行個別且獨立的評估，即使完全相同的引數套用至這兩種呼叫也一樣。 尤其，針對其中一個呼叫結果所套用的篩選或聯結條件對於另一個呼叫的結果沒有作用。  
  
 WHERE  
 指定用來限制更新資料列的條件。 根據所用的 WHERE 子句形式，更新有兩種形式：  
  
-   搜尋更新會指定用來限定要刪除之資料列的搜尋條件。  
  
-   定位更新利用 CURRENT OF 子句來指定資料指標。 更新作業發生在資料指標目前的位置上。  
  
\<s >  
 指定要更新之資料列的相符條件。 搜尋條件也可以是聯結的基礎條件。 搜尋條件中所能包括的述詞數目沒有限制。 如需有關述詞和搜尋條件的詳細資訊，請參閱[搜尋條件 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
CURRENT OF  
 指定在指定資料指標目前的位置執行更新。  
  
 利用 WHERE CURRENT OF 子句來進行的定位更新，會在資料指標目前位置更新單一資料列。 這可以更精確比利用 WHERE 搜尋更新\<s > 子句來限定要更新的資料列。 當搜尋條件並未唯一識別單一資料列時，搜尋更新會修改多個資料列。  
  
GLOBAL  
 指定*cursor_name*參考全域資料指標。  
  
*cursor_name*  
 這是應該從中提取的開啟資料指標名稱。 如果全域和本機資料指標名稱*cursor_name*存在，這個引數是指全域資料指標，如果 GLOBAL 時指定，否則，它會參考本機資料指標。 這個資料指標必須允許更新。  
  
*cursor_variable_name*  
 這是資料指標變數的名稱。 *cursor_variable_name*必須參考允許更新的資料指標。  
  
選項**(** \<query_hint > [ **，**...*n* ] **)**  
 指定利用最佳化工具提示來自訂 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 處理陳述式的方式。 如需詳細資訊，請參閱[查詢提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)。  
  
## <a name="best-practices"></a>最佳作法  
 使用 @@ROWCOUNT函式傳回的數目插入用戶端應用程式的資料列。 如需詳細資訊，請參閱[@@ROWCOUNT &#40;TRANSACT-SQL &#41;](../../t-sql/functions/rowcount-transact-sql.md).  
  
 UPDATE 陳述式可以利用變數名稱來顯示受影響的舊值和新值，但這只適用於 UPDATE 陳述式會影響單一記錄的情況。 如果 UPDATE 陳述式會影響多筆記錄，以傳回每一筆記錄，舊的和新值使用[OUTPUT 子句](../../t-sql/queries/output-clause-transact-sql.md)。  
  
 指定 FROM 子句來提供更新作業的準則時，請特別小心。 如果 UPDATE 陳述式包括 FROM 子句，且這個 FROM 子句的指定方式並非每個更新的資料行項目都只能使用一個值，也就是說，如果 UPDATE 陳述式不具決定性，UPDATE 陳述式的結果便未定義。 例如，在下列指令碼的 UPDATE 陳述式中，`Table1` 中的兩個資料列都符合 UPDATE 陳述式中之 FROM 子句的識別資格；但並未定義 `Table1` 中的哪個資料列用來更新 `Table2.` 中的資料列。  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ('dbo.Table1', 'U') IS NOT NULL  
    DROP TABLE dbo.Table1;  
GO  
IF OBJECT_ID ('dbo.Table2', 'U') IS NOT NULL  
    DROP TABLE dbo.Table2;  
GO  
CREATE TABLE dbo.Table1   
    (ColA int NOT NULL, ColB decimal(10,3) NOT NULL);  
GO  
CREATE TABLE dbo.Table2   
    (ColA int PRIMARY KEY NOT NULL, ColB decimal(10,3) NOT NULL);  
GO  
INSERT INTO dbo.Table1 VALUES(1, 10.0), (1, 20.0);  
INSERT INTO dbo.Table2 VALUES(1, 0.0);  
GO  
UPDATE dbo.Table2   
SET dbo.Table2.ColB = dbo.Table2.ColB + dbo.Table1.ColB  
FROM dbo.Table2   
    INNER JOIN dbo.Table1   
    ON (dbo.Table2.ColA = dbo.Table1.ColA);  
GO  
SELECT ColA, ColB   
FROM dbo.Table2;  
```  
  
 當組合 FROM 和 WHERE CURRENT OF 子句時，也會出現相同的問題。 在下列範例中，`Table2` 中的兩個資料列都符合 `FROM` 陳述式中的 `UPDATE` 子句識別資格。 利用 `Table2` 中的哪個資料列來更新 `Table1` 中的資料列，並未定義。  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ('dbo.Table1', 'U') IS NOT NULL  
    DROP TABLE dbo.Table1;  
GO  
IF OBJECT_ID ('dbo.Table2', 'U') IS NOT NULL  
    DROP TABLE dbo.Table2;  
GO  
CREATE TABLE dbo.Table1  
    (c1 int PRIMARY KEY NOT NULL, c2 int NOT NULL);  
GO  
CREATE TABLE dbo.Table2  
    (d1 int PRIMARY KEY NOT NULL, d2 int NOT NULL);  
GO  
INSERT INTO dbo.Table1 VALUES (1, 10);  
INSERT INTO dbo.Table2 VALUES (1, 20), (2, 30);  
GO  
DECLARE abc CURSOR LOCAL FOR  
    SELECT c1, c2   
    FROM dbo.Table1;  
OPEN abc;  
FETCH abc;  
UPDATE dbo.Table1   
SET c2 = c2 + d2   
FROM dbo.Table2   
WHERE CURRENT OF abc;  
GO  
SELECT c1, c2 FROM dbo.Table1;  
GO  
```  
  
## <a name="compatibility-support"></a>相容性支援  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的未來版本將移除套用到 UPDATE 或 DELETE 陳述式目標資料表的 FROM 子句中 READUNCOMMITTED 和 NOLOCK 提示的使用支援。 請避免在新的開發工作中使用此內容中的這些提示，並規劃修改目前在使用這些提示的應用程式。  
  
## <a name="data-types"></a>資料型別  
 所有**char**和**nchar**資料行是向右填補到定義的長度。  
  
 如果 ANSI_PADDING 設為 OFF 時，所有尾端空白會從插入的資料移除**varchar**和**nvarchar**資料行，除非在只含有空格的字串。 這些字串會截斷成空字串。 如果 ANSI_PADDING 設為 ON，便會插入尾端空格。 Microsoft SQL Server ODBC 驅動程式和 OLE DB Provider for SQL Server 提供者會自動設定每項連接的 ANSI_PADDING ON。 您可以在 ODBC 資料來源中設定這個項目，也可以設定連接屬性來設定這個項目。 如需詳細資訊，請參閱 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)。  
  
### <a name="updating-text-ntext-and-image-columns"></a>更新 text、ntext 和 image 資料行  
 修改**文字**， **ntext**，或**映像**更新具有資料行初始化資料行、 將有效的文字指標指派給它，並配置至少一個資料頁面上，除非正在更新資料行具有 NULL。  
  
 若要取代或修改大型區塊的**文字**， **ntext**，或**映像**資料，請使用[WRITETEXT](../../t-sql/queries/writetext-transact-sql.md)或[UPDATETEXT](../../t-sql/queries/updatetext-transact-sql.md)而不是 UPDATE 陳述式。  
  
 如果 UPDATE 陳述式無法變更多個資料列時發生更新叢集索引鍵和其一或多個**文字**， **ntext**，或**映像**資料行、 部分更新這些資料行是以完整取代值的執行。  
  
> [!IMPORTANT]  
>  **Ntext**，**文字**，和**映像**的未來版本將移除的資料型別[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 請避免在新的開發工作中使用這些資料類型，並規劃修改目前在使用這些資料類型的應用程式。 請改用 [nvarchar(max)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)、 [varchar(max)](../../t-sql/data-types/char-and-varchar-transact-sql.md)和 [varbinary(max)](../../t-sql/data-types/binary-and-varbinary-transact-sql.md) 。  
  
### <a name="updating-large-value-data-types"></a>更新大數值資料類型  
 使用**。**寫入 (*運算式***，**  *@Offset*  **，***@Length*) 子句執行的部分或完整更新**varchar （max)**， **nvarchar （max)**，和**varbinary （max)**資料型別。 例如，部分更新**varchar （max)**資料行可能會刪除或修改資料行的前 200 個字元，而完整的更新會刪除或修改資料行中的所有資料。 **.**WRITE 如果資料庫復原模式設為大量記錄或簡單就會進行最低限度記錄，插入或附加新資料更新。 當更新現有的值時，不會使用最低限度記錄。 如需詳細資訊，請參閱 [交易記錄 &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)。  
  
 當 UPDATE 陳述式造成下列情況時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會將部分更新轉換成完整更新：  
-   變更資料分割檢視或資料表的索引鍵資料行。  
-   修改多個資料列，同時也將不是唯一的叢集索引之索引鍵更新成非常數值。  
  
您無法使用**。**WRITE 子句來更新 NULL 資料行，或設定值*column_name*為 NULL。  
  
*@Offset*和 *@Length* 以位元組為單位指定**varbinary**和**varchar**資料類型以字元來**nvarchar**資料型別。 雙位元組字集 (DBCS) 定序會計算適當的位移。  
  
若要有最佳效能，建議您以 8040 個位元組倍數的片段大小來插入或更新資料。  
  
如果修改的資料行**。**寫入子句中參考 OUTPUT 子句，將資料行的完整值可以是中的影像之前**刪除。***column_name*或後的置資料影像中**插入。***column_name*，傳回資料表變數中的指定資料行。 請參閱以下的範例 R。  
  
若要達到相同的功能**。**撰寫和其他字元或二進位資料類型，請使用[東西 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/stuff-transact-sql.md).  
  
### <a name="updating-user-defined-type-columns"></a>更新使用者定義型別資料行  
 您可以利用下列方式之一來完成使用者定義型別資料行值的更新：  
  
-   只要使用者定義型別支援從這個類型進行隱含或明確的轉換，便在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料類型中提供一個值。 下列範例會顯示如何從字串進行明確的轉換，以便在使用者定義型別 `Point` 的資料行中更新值。  
  
    ```sql  
    UPDATE Cities  
    SET Location = CONVERT(Point, '12.3:46.2')  
    WHERE Name = 'Anchorage';  
    ```  
  
-   叫用使用者定義型別的方法 (標示為 mutator) 來執行更新。 下列範例會叫用名稱為 `Point` 的 `SetXY` 類型之 mutator 方法。 這會更新類型執行個體的狀態。  
  
    ```sql  
    UPDATE Cities  
    SET Location.SetXY(23.5, 23.5)  
    WHERE Name = 'Anchorage';  
    ```  
  
    > [!NOTE]  
    >  如果在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Null 值上呼叫了 mutator 方法，或是 mutator 方法所產生的新值是 Null，[!INCLUDE[tsql](../../includes/tsql-md.md)] 就會傳回錯誤。  
  
-   修改使用者定義型別的登錄屬性值或公用資料成員值。 提供值的運算式必須可隱含地轉換成屬性的類型。 下列範例會修改使用者定義型別 `X` 的 `Point` 屬性值。  
  
    ```sql  
    UPDATE Cities  
    SET Location.X = 23.5  
    WHERE Name = 'Anchorage';  
    ```  
  
     若要修改相同使用者定義型別資料行的不同屬性，請發出多個 UPDATE 陳述式，或呼叫該類型的 mutator 方法。  
  
### <a name="updating-filestream-data"></a>更新 FILESTREAM 資料  
 您可以使用 UPDATE 陳述式，將 FILESTREAM 欄位更新為 Null 值、空白值，或是相當少量的內嵌資料。 但是，使用 Win32 介面，將大量資料當做資料流處理成檔案時，會比較有效率。 當您更新 FILESTREAM 欄位時，您會修改檔案系統中的基礎 BLOB 資料。 當 FILESTREAM 欄位設定為 NULL 時，與此欄位有關聯的 BLOB 資料會遭到刪除。 您無法使用。Write （) 來執行 FILESTREAM 資料的部分更新。 如需詳細資訊，請參閱 [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)。  
  
## <a name="error-handling"></a>錯誤處理  
 如果資料列的更新違反條件約束或規則、違反資料行的 NULL 設定，或新值是不相容的資料類型，便會取消陳述式、傳回錯誤，而且不會更新任何記錄。  
  
 當 UPDATE 陳述式在運算式評估期間發生算術錯誤 (溢位、除以零或區域錯誤) 時，便不會進行更新。 批次的其餘部分也不會執行，且會傳回錯誤訊息。  
  
 如果參與叢集索引的一個或多個資料行的更新使叢集索引和資料列的大小超出 8,060 個位元組，更新就會失敗，而且會傳回錯誤訊息。  
  
## <a name="interoperability"></a>互通性  
 只有當所修改的資料表是一個資料表變數時，才能在使用者定義函數的主體中使用 UPDATE 陳述式。  
  
 當定義資料表之 UPDATE 動作的 INSTEAD OF 觸發程序時，會執行觸發程序，而不是 UPDATE 陳述式。 舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只支援 UPDATE 及其他資料修改陳述式所定義的 AFTER 觸發程序。 在直接或間接參考定義了 INSTEAD OF 觸發程序的檢視表之 UPDATE 陳述式中，不能指定 FROM 子句。 而不是觸發程序的相關資訊，請參閱[CREATE TRIGGER &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 在直接或間接參考定義了 INSTEAD OF 觸發程序之檢視表的 UPDATE 陳述式中，不能指定 FROM 子句。 而不是觸發程序的相關資訊，請參閱[CREATE TRIGGER &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
 當通用資料表運算式 (CTE) 是 UPDATE 陳述式的目標時，陳述式中所有 CTE 的參考都必須相符。 例如，如果 CTE 被指派 FROM 子句中的別名，此別名就必須用於 CTE 的所有其他參考。 因為 CTE 沒有物件識別碼，可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用來辨識物件與其別名之間的隱含關聯性，所以需要使用不模稜兩可的 CTE 參考。 如果沒有這個關聯性，查詢計畫可能會產生無法預期的聯結行為和不想要的查詢結果。 下列範例將示範當 CTE 是更新作業的目標物件時，指定 CTE 的正確與不正確方法。  
  
```sql  
USE tempdb;  
GO  
-- UPDATE statement with CTE references that are correctly matched.  
DECLARE @x TABLE (ID int, Value int);  
DECLARE @y TABLE (ID int, Value int);  
INSERT @x VALUES (1, 10), (2, 20);  
INSERT @y VALUES (1, 100),(2, 200);  
  
WITH cte AS (SELECT * FROM @x)  
UPDATE x -- cte is referenced by the alias.  
SET Value = y.Value  
FROM cte AS x  -- cte is assigned an alias.  
INNER JOIN @y AS y ON y.ID = x.ID;  
SELECT * FROM @x;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 ID     Value  
 ------ -----  
 1      100  
 2      200  
 (2 row(s) affected)  
```  

具有不正確地比對的 CTE 參考的 UPDATE 陳述式。  
```sql  
USE tempdb;  
GO  
DECLARE @x TABLE (ID int, Value int);  
DECLARE @y TABLE (ID int, Value int);  
INSERT @x VALUES (1, 10), (2, 20);  
INSERT @y VALUES (1, 100),(2, 200);  
  
WITH cte AS (SELECT * FROM @x)  
UPDATE cte   -- cte is not referenced by the alias.  
SET Value = y.Value  
FROM cte AS x  -- cte is assigned an alias.  
INNER JOIN @y AS y ON y.ID = x.ID;   
SELECT * FROM @x;   
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
ID     Value  
------ -----  
1      100  
2      100  
(2 row(s) affected)  
```  

## <a name="locking-behavior"></a>鎖定行為  
 UPDATE 陳述式永遠都會取得它所修改之資料表的獨佔 (X) 鎖定，並保留該鎖定直到交易完成為止。 使用獨佔鎖定時，任何其他交易都無法修改資料。 您可以指定資料表提示，透過指定其他鎖定方法來覆寫 UPDATE 陳述式持續時間的這個預設行為，但是，我們建議僅將提示做為由資深開發人員及資料庫管理員採取的最後手段。 如需詳細資訊，請參閱[資料表提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)。  
  
## <a name="logging-behavior"></a>記錄行為  
 記錄 UPDATE 陳述式。不過，部分更新大數值資料類型使用**。**WRITE 子句會使用最低限度記錄。 如需詳細資訊，請參閱前面＜資料類型＞一節中的＜更新大數值資料類型＞。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 需要目標資料表的 UPDATE 權限。 也是必要如果 UPDATE 陳述式包含 WHERE 子句，或是正在更新之資料表的 SELECT 權限*運算式*集中子句，請使用資料表中的資料行。  
  
 更新成員的權限預設**sysadmin**固定伺服器角色、 **db_owner**和**db_datawriter**固定資料庫角色，以及資料表擁有者。 成員**sysadmin**， **db_owner**，和**db_securityadmin**角色，以及資料表擁有者可以將權限移轉給其他使用者。  
  
##  <a name="UpdateExamples"></a> 範例  
  
|類別目錄|代表性語法元素|  
|--------------|------------------------------|  
|[基本語法](#BasicSyntax)|UPDATE|  
|[限制更新的資料列](#LimitingValues)|WHERE • TOP • WITH 通用資料表運算式 • WHERE CURRENT OF|  
|[設定資料行值](#ColumnValues)|計算值 • 複合運算子 • 預設值 • 子查詢|  
|[指定標準資料表以外的目標物件](#TargetObjects)|檢視表 • 資料表變數 • 資料表別名|  
|[更新的資料是從其他資料表的資料](#OtherTables)|FROM|  
|[更新遠端資料表中的資料列](#RemoteTables)|連結的伺服器 • OPENQUERY • OPENDATASOURCE|  
|[更新大型物件資料類型](#LOBValues)|.寫入 • OPENROWSET|  
|[更新使用者定義型別](#UDTs)|使用者定義型別|  
|[使用提示來覆寫查詢最佳化工具的預設行為](#TableHints)|資料表提示 • 查詢提示|  
|[擷取 UPDATE 陳述式的結果](#CaptureResults)|OUTPUT 子句|  
|[在其他陳述式中使用 UPDATE](#Other)|預存程序 • TRY…CATCH|  
  
###  <a name="BasicSyntax"></a>基本語法  
 本節的範例會使用所需的最少語法來示範 UPDATE 陳述式的基本功能。  
  
#### <a name="a-using-a-simple-update-statement"></a>A. 使用簡單的 UPDATE 陳述式  
 下列範例會更新 `Person.Address` 資料表中所有資料列的單一資料行。  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Person.Address  
SET ModifiedDate = GETDATE();  
```  
  
#### <a name="b-updating-multiple-columns"></a>B. 更新多個資料行  
 下列範例會更新 `Bonus` 資料表中所有資料列的 `CommissionPct`、`SalesQuota` 和 `SalesPerson` 資料行值。  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Sales.SalesPerson  
SET Bonus = 6000, CommissionPct = .10, SalesQuota = NULL;  
GO  
```  
  
###  <a name="LimitingValues"></a>限制更新的資料列  
 本節的範例將示範可讓您用來限制 UPDATE 陳述式所影響之資料列數目的方式。  
  
#### <a name="c-using-the-where-clause"></a>C. 使用 WHERE 子句  
 下列範例會利用 WHERE 子句來指定要更新的資料列。 此陳述式會針對 `Color` 資料行的現有值為 'Red' 而且 `Production.Product` 資料行值以 'Road-250' 為開頭的所有資料列，更新 `Color` 資料表之 `Name` 資料行的值。  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.Product  
SET Color = N'Metallic Red'  
WHERE Name LIKE N'Road-250%' AND Color = N'Red';  
GO  
```  
  
#### <a name="d-using-the-top-clause"></a>D. 使用 TOP 子句  
 下列範例會使用 TOP 子句來限制在 UPDATE 陳述式中修改的資料列數目。 當 TOP (*n*) 子句與 UPDATE，則隨機選取的執行更新作業 '*n*' 個資料列。 下列範例會將 `VacationHours` 資料表中 10 個隨機資料列的 `Employee` 資料行更新 25%。  
  
```sql  
USE AdventureWorks2012;
GO
UPDATE TOP (10) HumanResources.Employee
SET VacationHours = VacationHours * 1.25 ;
GO  
```  
  
 如果您必須使用 TOP 依有意義的時間順序套用更新，就要在子選擇陳述式中同時使用 TOP 與 ORDER BY。 下例會更新最早雇用的前 10 名員工的休假時數。  
  
```sql  
UPDATE HumanResources.Employee  
SET VacationHours = VacationHours + 8  
FROM (SELECT TOP 10 BusinessEntityID FROM HumanResources.Employee  
     ORDER BY HireDate ASC) AS th  
WHERE HumanResources.Employee.BusinessEntityID = th.BusinessEntityID;  
GO  
```  
  
#### <a name="e-using-the-with-commontableexpression-clause"></a>E. 使用 WITH common_table_expression 子句  
 下列範例會更新直接或間接使用之所有組件和元件的 `PerAssemnblyQty` 值以建立 `ProductAssemblyID 800`。 通用資料表運算式會傳回一份階層式清單，其中包含直接用來建立 `ProductAssemblyID 800` 的組件、用來建立這些元件的組件等等。 只會修改通用資料表運算式所傳回的資料列。  
  
```sql  
USE AdventureWorks2012;  
GO  
WITH Parts(AssemblyID, ComponentID, PerAssemblyQty, EndDate, ComponentLevel) AS  
(  
    SELECT b.ProductAssemblyID, b.ComponentID, b.PerAssemblyQty,  
        b.EndDate, 0 AS ComponentLevel  
    FROM Production.BillOfMaterials AS b  
    WHERE b.ProductAssemblyID = 800  
          AND b.EndDate IS NULL  
    UNION ALL  
    SELECT bom.ProductAssemblyID, bom.ComponentID, p.PerAssemblyQty,  
        bom.EndDate, ComponentLevel + 1  
    FROM Production.BillOfMaterials AS bom   
        INNER JOIN Parts AS p  
        ON bom.ProductAssemblyID = p.ComponentID  
        AND bom.EndDate IS NULL  
)  
UPDATE Production.BillOfMaterials  
SET PerAssemblyQty = c.PerAssemblyQty * 2  
FROM Production.BillOfMaterials AS c  
JOIN Parts AS d ON c.ProductAssemblyID = d.AssemblyID  
WHERE d.ComponentLevel = 0;  
```  
  
#### <a name="f-using-the-where-current-of-clause"></a>F. 使用 WHERE CURRENT OF 子句  
 下列範例會使用 WHERE CURRENT OF 子句來單獨更新資料指標所在的資料列。 當資料指標是以聯結為基礎時，只會修改在 UPDATE 陳述式中指定的 `table_name`。 牽涉到資料指標的其他資料表都不會受到影響。  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE complex_cursor CURSOR FOR  
    SELECT a.BusinessEntityID  
    FROM HumanResources.EmployeePayHistory AS a  
    WHERE RateChangeDate <>   
         (SELECT MAX(RateChangeDate)  
          FROM HumanResources.EmployeePayHistory AS b  
          WHERE a.BusinessEntityID = b.BusinessEntityID) ;  
OPEN complex_cursor;  
FETCH FROM complex_cursor;  
UPDATE HumanResources.EmployeePayHistory  
SET PayFrequency = 2   
WHERE CURRENT OF complex_cursor;  
CLOSE complex_cursor;  
DEALLOCATE complex_cursor;  
GO  
```  
  
###  <a name="ColumnValues"></a>設定資料行值  
 本節的範例會示範如何使用計算值、子查詢和 DEFAULT 值來更新資料行。  
  
#### <a name="g-specifying-a-computed-value"></a>G. 指定計算值  
 下列範例會在 UPDATE 陳述式中使用計算值。 此範例會將 `ListPrice` 資料表中所有資料列的 `Product` 資料行值加倍。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
UPDATE Production.Product  
SET ListPrice = ListPrice * 2;  
GO  
```  
  
#### <a name="h-specifying-a-compound-operator"></a>H. 指定複合運算子  
 下列範例會使用 `@NewPrice` 變數來遞增所有紅色自行車的價格，其方式是將目前的價格增加 10。  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @NewPrice int = 10;  
UPDATE Production.Product  
SET ListPrice += @NewPrice  
WHERE Color = N'Red';  
GO  
```  
  
 下列範例會針對 `' - tool malfunction'` 介於 10 與 12 之間的資料列，使用複合運算子 +=，將 `Name` 資料附加至 `ScrapReasonID` 資料行中的現有值。  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.ScrapReason   
SET Name += ' - tool malfunction'  
WHERE ScrapReasonID BETWEEN 10 and 12;  
```  
  
#### <a name="i-specifying-a-subquery-in-the-set-clause"></a>I. 在 SET 子句中指定子查詢  
 下列範例會在 SET 子句中使用子查詢來決定用來更新資料行的值。 這個子查詢必須只傳回純量值 (也就是說，每個資料列單一值)。 此範例會修改 `SalesYTD` 資料表中的 `SalesPerson` 資料行，以便反映 `SalesOrderHeader` 資料表中最新的銷售記錄。 這個子查詢將彙總 `UPDATE` 陳述式中每位銷售人員的銷售額。  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Sales.SalesPerson  
SET SalesYTD = SalesYTD +   
    (SELECT SUM(so.SubTotal)   
     FROM Sales.SalesOrderHeader AS so  
     WHERE so.OrderDate = (SELECT MAX(OrderDate)  
                           FROM Sales.SalesOrderHeader AS so2  
                           WHERE so2.SalesPersonID = so.SalesPersonID)  
     AND Sales.SalesPerson.BusinessEntityID = so.SalesPersonID  
     GROUP BY so.SalesPersonID);  
GO  
```  
  
#### <a name="j-updating-rows-using-default-values"></a>J. 使用 DEFAULT 值更新資料列  
 下列範例會針對 `CostRate` 值大於 `CostRate` 的所有資料列，將 `20.00` 資料行設定為其預設值 (0.00)。  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.Location  
SET CostRate = DEFAULT  
WHERE CostRate > 20.00;  
```  
  
###  <a name="TargetObjects"></a>指定標準資料表以外的目標物件  
 本節的範例會示範如何透過指定檢視表、資料表別名或資料表變數，更新資料列。  
  
#### <a name="k-specifying-a-view-as-the-target-object"></a>K. 將檢視表指定為目標物件  
 下列範例會將檢視表指定為目標物件，藉以更新資料表中的資料列。 雖然檢視表定義會參考多個資料表，不過 UPDATE 陳述式仍然成功，因為它只會參考其中一個基礎資料表中的資料行。 如果同時指定了兩個資料表的資料行，UPDATE 陳述式就會失敗。 如需詳細資訊，請參閱[修改資料透過檢視](../../relational-databases/views/modify-data-through-a-view.md)。  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Person.vStateProvinceCountryRegion  
SET CountryRegionName = 'United States of America'  
WHERE CountryRegionName = 'United States';  
```  
  
#### <a name="l-specifying-a-table-alias-as-the-target-object"></a>L. 將資料表別名指定為目標物件  
 下列範例會更新 `Production.ScrapReason` 資料表中的資料列。 在 FROM 子句中，指派給 `ScrapReason` 的資料表別名會指定為 UPDATE 子句中的目標物件。  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE sr  
SET sr.Name += ' - tool malfunction'  
FROM Production.ScrapReason AS sr  
JOIN Production.WorkOrder AS wo   
     ON sr.ScrapReasonID = wo.ScrapReasonID  
     AND wo.ScrappedQty > 300;  
```  
  
#### <a name="m-specifying-a-table-variable-as-the-target-object"></a>M. 將資料表變數指定為目標物件  
 下列範例會更新資料表變數中的資料列。  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Create the table variable.  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    NewVacationHours int,  
    ModifiedDate datetime);  
  
-- Populate the table variable with employee ID values from HumanResources.Employee.  
INSERT INTO @MyTableVar (EmpID)  
    SELECT BusinessEntityID FROM HumanResources.Employee;  
  
-- Update columns in the table variable.  
UPDATE @MyTableVar  
SET NewVacationHours = e.VacationHours + 20,  
    ModifiedDate = GETDATE()  
FROM HumanResources.Employee AS e   
WHERE e.BusinessEntityID = EmpID;  
  
-- Display the results of the UPDATE statement.  
SELECT EmpID, NewVacationHours, ModifiedDate FROM @MyTableVar  
ORDER BY EmpID;  
GO  
```  
  
###  <a name="OtherTables"></a>更新的資料是從其他資料表的資料  
 本節的範例會示範根據某個資料表之資訊更新另一個資料表之資料列的方法。  
  
#### <a name="n-using-the-update-statement-with-information-from-another-table"></a>N. 使用 UPDATE 陳述式搭配另一份資料表的資訊  
 下列範例會修改 `SalesYTD` 資料表中的 `SalesPerson` 資料行，以便反映 `SalesOrderHeader` 資料表中最新的銷售記錄。  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Sales.SalesPerson  
SET SalesYTD = SalesYTD + SubTotal  
FROM Sales.SalesPerson AS sp  
JOIN Sales.SalesOrderHeader AS so  
    ON sp.BusinessEntityID = so.SalesPersonID  
    AND so.OrderDate = (SELECT MAX(OrderDate)  
                        FROM Sales.SalesOrderHeader  
                        WHERE SalesPersonID = sp.BusinessEntityID);  
GO  
```  
  
 上一個範例假設指定的銷售人員在特定日期只有一項銷售記錄，而且更新是最新的。 如果指定的銷售人員同一天可以有多項銷售記錄，顯示的範例便無法正確運作。 範例會執行不會發生錯誤，但每個`SalesYTD`只有一個銷售，不論是在多少銷售實際發生在那一天更新值。 這是因為單一 UPDATE 陳述式永遠不會更新相同資料列兩次。  
  
 如果在同一天內，指定的銷售人員可以有多筆銷售額，則必須在 `UPDATE` 陳述式內彙總每一個銷售人員的所有銷售額，如下列範例所示：  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Sales.SalesPerson  
SET SalesYTD = SalesYTD +   
    (SELECT SUM(so.SubTotal)   
     FROM Sales.SalesOrderHeader AS so  
     WHERE so.OrderDate = (SELECT MAX(OrderDate)  
                           FROM Sales.SalesOrderHeader AS so2  
                           WHERE so2.SalesPersonID = so.SalesPersonID)  
     AND Sales.SalesPerson.BusinessEntityID = so.SalesPersonID  
     GROUP BY so.SalesPersonID);  
GO  
```  
  
###  <a name="RemoteTables"></a>更新遠端資料表中的資料列  
 本節中的範例將示範如何使用來更新遠端目標資料表中的資料列[連結的伺服器](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)或[資料列集函數](../../t-sql/functions/rowset-functions-transact-sql.md)來參考遠端資料表。  
  
#### <a name="o-updating-data-in-a-remote-table-by-using-a-linked-server"></a>O. 使用連結的伺服器來更新遠端資料表中的資料  
 下列範例會更新遠端伺服器上的資料表。 此範例一開始會使用建立遠端資料來源的連結[sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)。 然後會將連結的伺服器名稱 `MyLinkServer` 指定為 server.catalog.schema.object 格式之四部分物件名稱的一部分。 請注意，您必須針對 `@datasrc` 指定有效的伺服器名稱。  
  
```sql  
USE master;  
GO  
-- Create a link to the remote data source.   
-- Specify a valid server name for @datasrc as 'server_name' or 'server_nameinstance_name'.  
  
EXEC sp_addlinkedserver @server = N'MyLinkServer',  
    @srvproduct = N' ',  
    @provider = N'SQLNCLI10',   
    @datasrc = N'<server name>',  
    @catalog = N'AdventureWorks2012';  
GO  
USE AdventureWorks2012;  
GO  
-- Specify the remote data source using a four-part name   
-- in the form linked_server.catalog.schema.object.  
  
UPDATE MyLinkServer.AdventureWorks2012.HumanResources.Department  
SET GroupName = N'Public Relations'  
WHERE DepartmentID = 4;  
```  
  
#### <a name="p-updating-data-in-a-remote-table-by-using-the-openquery-function"></a>P. 使用 OPENQUERY 函數來更新遠端資料表中的資料  
 下列範例會更新遠端資料表中的資料列，藉由指定[OPENQUERY](../../t-sql/functions/openquery-transact-sql.md)資料列集函數。 上一個範例所建立之連結的伺服器名稱會用於這個範例。  
  
```sql  
UPDATE OPENQUERY (MyLinkServer, 'SELECT GroupName FROM HumanResources.Department WHERE DepartmentID = 4')   
SET GroupName = 'Sales and Marketing';  
```  
  
#### <a name="q-updating-data-in-a-remote-table-by-using-the-opendatasource-function"></a>Q. 使用 OPENDATASOURCE 函數來更新遠端資料表中的資料  
 下列範例將資料列插入遠端資料表藉由指定[OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md)資料列集函數。 使用格式指定有效的伺服器名稱的資料來源*server_name*或*\ 執行個體名稱*。 您可能必須針對特定分散式查詢設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 如需詳細資訊，請參閱[特定分散式查詢伺服器組態選項](../../database-engine/configure-windows/ad-hoc-distributed-queries-server-configuration-option.md)。  
  
```sql  
UPDATE OPENQUERY (MyLinkServer, 'SELECT GroupName FROM HumanResources.Department WHERE DepartmentID = 4')   
SET GroupName = 'Sales and Marketing';  
```  
  
###  <a name="LOBValues"></a>更新大型物件資料類型  
 本節的範例將示範更新以大型物件 (LOB) 資料類型定義之資料行值的方法。  
  
#### <a name="r-using-update-with-write-to-modify-data-in-an-nvarcharmax-column"></a>R. 使用 UPDATE 搭配 .WRITE 來修改 nvarchar(max) 資料行中的資料  
 下列範例會使用。WRITE 子句來更新中的部分值`DocumentSummary`、 **nvarchar （max)**中的資料行`Production.Document`資料表。 `components` 一字會藉由指定取代文字、現有資料中要取代之字的起始位置 (位移)，以及要取代的字元數 (長度) 來取代為 `features` 一字。 範例也利用 OUTPUT 子句傳回之前和之後的映像`DocumentSummary`欄`@MyTableVar`資料表變數。  
  
```sql  
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
  
#### <a name="s-using-update-with-write-to-add-and-remove-data-in-an-nvarcharmax-column"></a>S. 使用 UPDATE 搭配 .WRITE，以新增和移除 nvarchar(max) 資料行中的資料  
 下列範例新增和移除的資料**nvarchar （max)**目前設為 NULL 值的資料行。 因為。撰寫子句不能用來修改 NULL 資料行，而資料行第一次擴展暫存資料。 之後，便利用 .WRITE 子句，將這項資料取代為正確的資料。 其他範例會將資料附加至資料行值的結尾，移除 (截斷) 資料行中的資料，最後會從資料行中移除部分資料。 SELECT 陳述式會顯示每個 UPDATE 陳述式所產生的資料修改。  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Replacing NULL value with temporary data.  
UPDATE Production.Document  
SET DocumentSummary = N'Replacing NULL value'  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
-- Replacing temporary data with the correct data. Setting @Length to NULL   
-- truncates all existing data from the @Offset position.  
UPDATE Production.Document  
SET DocumentSummary .WRITE(N'Carefully inspect and maintain the tires and crank arms.',0,NULL)  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
-- Appending additional data to the end of the column by setting   
-- @Offset to NULL.  
UPDATE Production.Document  
SET DocumentSummary .WRITE (N' Appending data to the end of the column.', NULL, 0)  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
-- Removing all data from @Offset to the end of the existing value by   
-- setting expression to NULL.   
UPDATE Production.Document  
SET DocumentSummary .WRITE (NULL, 56, 0)  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
-- Removing partial data beginning at position 9 and ending at   
-- position 21.  
UPDATE Production.Document  
SET DocumentSummary .WRITE ('',9, 12)  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
```  
  
#### <a name="t-using-update-with-openrowset-to-modify-a-varbinarymax-column"></a>T. 使用 UPDATE 搭配 OPENROWSET，以修改 varbinary(max) 資料行  
 下列範例會取代現有的映像儲存在**varbinary （max)**與新的映像的資料行。 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)函數搭配 BULK 選項使用的影像載入資料行。 這個範例假設指定的檔案路徑中，有名稱為 `Tires.jpg` 的檔案。  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.ProductPhoto  
SET ThumbNailPhoto = (  
    SELECT *  
    FROM OPENROWSET(BULK 'c:Tires.jpg', SINGLE_BLOB) AS x )  
WHERE ProductPhotoID = 1;  
GO  
```  
  
#### <a name="u-using-update-to-modify-filestream-data"></a>U. 使用 UPDATE 來修改 FILESTREAM 資料  
 下列範例會使用 UPDATE 陳述式來修改檔案系統檔案中的資料。 但是，我們不建議您使用這個方法，將大量資料串流處理成檔案。 請使用適當的 Win32 介面。 下列範例會以文字 `Xray 1`來取代檔案記錄中的所有文字。 如需詳細資訊，請參閱 [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)。  
  
```sql  
UPDATE Archive.dbo.Records  
SET [Chart] = CAST('Xray 1' as varbinary(max))  
WHERE [SerialNumber] = 2;  
```  
  
###  <a name="UDTs"></a>更新使用者定義型別  
 下列範例會修改 CLR 使用者定義型別 (UDT) 資料行中的值。 我們將示範三種方法。 如需使用者定義資料行的詳細資訊，請參閱[clr 使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)。  
  
#### <a name="v-using-a-system-data-type"></a>V. 使用系統資料類型  
 只要使用者定義型別支援從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料類型進行隱含或明確的轉換，您就可以在這個類型中提供一個值，藉以更新 UDT。 下列範例會顯示如何從字串進行明確的轉換，以便在使用者定義型別 `Point` 的資料行中更新值。  
  
```sql  
UPDATE dbo.Cities  
SET Location = CONVERT(Point, '12.3:46.2')  
WHERE Name = 'Anchorage';  
```  
  
#### <a name="w-invoking-a-method"></a>W 叫用方法  
 您可以叫用使用者定義型別的方法 (標示為 mutator) 來執行更新，藉以更新 UDT。 下列範例會叫用名稱為 `Point` 的 `SetXY` 類型之 mutator 方法。 這會更新類型執行個體的狀態。  
  
```sql  
UPDATE dbo.Cities  
SET Location.SetXY(23.5, 23.5)  
WHERE Name = 'Anchorage';  
```  
  
#### <a name="x-modifying-the-value-of-a-property-or-data-member"></a>X。 修改屬性或資料成員的值  
 您可以修改使用者定義型別的已註冊屬性值或公用資料成員值，藉以更新 UDT。 提供值的運算式必須可隱含地轉換成屬性的類型。 下列範例會修改使用者定義型別 `X` 的 `Point` 屬性值。  
  
```sql  
UPDATE dbo.Cities  
SET Location.X = 23.5  
WHERE Name = 'Anchorage';  
```  
  
###  <a name="TableHints"></a>使用提示來覆寫查詢最佳化工具的預設行為  
 本節的範例將示範如何使用資料表和查詢提示，在處理 UPDATE 陳述式時暫時覆寫查詢最佳化工具的預設行為。  
  
> [!CAUTION]  
>  由於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢最佳化工具通常會選取最好的查詢執行計畫，因此，我們建議資深的開發人員和資料庫管理員只將提示當做最後的解決辦法。  
  
#### <a name="y-specifying-a-table-hint"></a>Y。 指定資料表提示  
 下列範例會指定[資料表提示](../../t-sql/queries/hints-transact-sql-table.md)TABLOCK。 這個提示會指定在 `Production.Product` 資料表上採用共用鎖定，並且將鎖定保留到 UPDATE 陳述式結束為止。  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.Product  
WITH (TABLOCK)  
SET ListPrice = ListPrice * 1.10  
WHERE ProductNumber LIKE 'BK-%';  
GO  
```  
  
#### <a name="z-specifying-a-query-hint"></a>Z。 指定查詢提示  
 下列範例會指定[查詢提示](../../t-sql/queries/hints-transact-sql-query.md)`OPTIMIZE FOR (@variable)` UPDATE 陳述式中。 這個提示會指示查詢最佳化工具在查詢進行編譯和最佳化時，使用特定的區域變數值。 只有在查詢最佳化期間，才使用這個值，在查詢執行期間，不使用這個值。  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE PROCEDURE Production.uspProductUpdate  
@Product nvarchar(25)  
AS  
SET NOCOUNT ON;  
UPDATE Production.Product  
SET ListPrice = ListPrice * 1.10  
WHERE ProductNumber LIKE @Product  
OPTION (OPTIMIZE FOR (@Product = 'BK-%') );  
GO  
-- Execute the stored procedure   
EXEC Production.uspProductUpdate 'BK-%';  
```  
  
###  <a name="CaptureResults"></a>擷取 UPDATE 陳述式的結果  
 本節中的範例將示範如何使用[OUTPUT 子句](../../t-sql/queries/output-clause-transact-sql.md)傳回資訊，或是根據運算式，每個資料列所影響的 UPDATE 陳述式。 這些結果可以傳回給負責處理的應用程式，以便用在確認訊息、封存或其他這類應用程式需求等用途上。  
  
#### <a name="aa-using-update-with-the-output-clause"></a>AA。 使用 UPDATE 搭配 OUTPUT 子句  
 下列範例會將 `VacationHours` 資料表前 10 個資料列的 `Employee` 資料行更新 25%，並且將 `ModifiedDate` 資料行中的值設定為目前的日期。 `OUTPUT` 子句會將在 `VacationHours` 資料行中套用 `UPDATE` 陳述式之前便已存在的 `deleted.VacationHours` 值，以及 `inserted.VacationHours` 資料行中更新的值傳回給 `@MyTableVar` 資料表變數。  
  
 之後的兩個 `SELECT` 陳述式會傳回 `@MyTableVar` 中的值，以及 `Employee` 資料表中更新作業的結果。 如需使用 OUTPUT 子句的範例，請參閱[OUTPUT 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/output-clause-transact-sql.md).  
  
```sql  
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
  
###  <a name="Other"></a>在其他陳述式中使用 UPDATE  
 本節的範例將示範如何在其他陳述式中使用 UPDATE。  
  
#### <a name="ab-using-update-in-a-stored-procedure"></a>AB. 在預存程序中使用 UPDATE  
 下列範例會在預存程序中使用 UPDATE 陳述式。 此程序會採用一個輸入參數 `@NewHours` 和一個輸出參數 `@RowCount`。 `@NewHours`參數值用於 UPDATE 陳述式中更新資料行`VacationHours`資料表中`HumanResources.Employee`。 `@RowCount` 輸出參數是用來將受影響的資料列數目傳回給區域變數。 SET 子句中會使用 CASE 運算式，以條件方式判斷針對 `VacationHours` 所設定的值。 按照時數支付薪資給員工時 (`SalariedFlag` = 0)，`VacationHours` 會設定為目前的時數加上 `@NewHours` 中指定的值，否則 `VacationHours` 會設定為 `@NewHours` 中指定的值。  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE PROCEDURE HumanResources.Update_VacationHours  
@NewHours smallint  
AS   
SET NOCOUNT ON;  
UPDATE HumanResources.Employee  
SET VacationHours =   
    ( CASE  
         WHEN SalariedFlag = 0 THEN VacationHours + @NewHours  
         ELSE @NewHours  
       END  
    )  
WHERE CurrentFlag = 1;  
GO  
  
EXEC HumanResources.Update_VacationHours 40;  
```  
  
#### <a name="ac-using-update-in-a-trycatch-block"></a>AC。 在 TRY…CATCH 區塊中使用 UPDATE  
 下列範例會使用 UPDATE 陳述式中再試一次...CATCH 區塊來處理更新作業期間可能發生執行錯誤。  
  
```sql  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
  
BEGIN TRY  
    -- Intentionally generate a constraint violation error.  
    UPDATE HumanResources.Department  
    SET Name = N'MyNewName'  
    WHERE DepartmentID BETWEEN 1 AND 2;  
END TRY  
BEGIN CATCH  
    SELECT   
         ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_LINE() AS ErrorLine  
        ,ERROR_MESSAGE() AS ErrorMessage;  
  
    IF @@TRANCOUNT > 0  
        ROLLBACK TRANSACTION;  
END CATCH;  
  
IF @@TRANCOUNT > 0  
    COMMIT TRANSACTION;  
GO  
```  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="ad-using-a-simple-update-statement"></a>AD。 使用簡單的 UPDATE 陳述式  
 下列範例會顯示所有資料列，能夠如何影響當 WHERE 子句不是指定要更新的資料列 （或資料列）。  
  
 這個範例會更新中的值`EndDate`和`CurrentFlag`資料行中的所有資料列`DimEmployee`資料表。  
  
```sql  
-- Uses AdventureWorks  
  
UPDATE DimEmployee  
SET EndDate = '2010-12-31', CurrentFlag='False';  
```  
  
 您也可以在 UPDATE 陳述式中使用計算值。 以下範例會使 `ListPrice` 資料表中所有資料列內 `Product` 資料行的值變成兩倍。  
  
```sql  
-- Uses AdventureWorks  
  
UPDATE DimEmployee  
SET BaseRate = BaseRate * 2;  
```  
  
### <a name="ae-using-the-update-statement-with-a-where-clause"></a>AE。 使用 WHERE 子句使用 UPDATE 陳述式  
 下列範例會利用 WHERE 子句來指定要更新的資料列。  
  
```sql  
-- Uses AdventureWorks  
  
UPDATE DimEmployee  
SET FirstName = 'Gail'  
WHERE EmployeeKey = 500;  
```  
  
### <a name="af-using-the-update-statement-with-label"></a>AF。 使用 UPDATE 陳述式標籤  
 下列範例顯示 UPDATE 陳述式的標籤使用。  
  
```sql  
-- Uses AdventureWorks  
  
UPDATE DimProduct  
SET ProductSubcategoryKey = 2   
WHERE ProductKey = 313  
OPTION (LABEL = N'label1');  
```  
  
### <a name="ag-using-the-update-statement-with-information-from-another-table"></a>AG。 使用 UPDATE 陳述式搭配另一份資料表的資訊  
 這個範例會建立可儲存依年度的銷售總額的資料表。 它會更新 2004 年的銷售總額 FactInternetSales 資料表執行 SELECT 陳述式。  
  
```sql  
-- Uses AdventureWorks  
  
CREATE TABLE YearlyTotalSales (  
    YearlySalesAmount money NOT NULL,  
    Year smallint NOT NULL )  
WITH ( DISTRIBUTION = REPLICATE );  
  
INSERT INTO YearlyTotalSales VALUES (0, 2004);  
INSERT INTO YearlyTotalSales VALUES (0, 2005);  
INSERT INTO YearlyTotalSales VALUES (0, 2006);  
  
UPDATE YearlyTotalSales  
SET YearlySalesAmount=  
(SELECT SUM(SalesAmount) FROM FactInternetSales WHERE OrderDateKey >=20040000 AND OrderDateKey < 20050000)  
WHERE Year=2004;  
  
SELECT * FROM YearlyTotalSales;   
```  

### <a name="ah-ansi-join-replacement-for-update-statements"></a>AH。 ANSI 聯結取代 update 陳述式
您可能會發現有複雜聯結在一起使用 ANSI 聯結語法執行 UPDATE 或 DELETE 的兩個以上資料表的更新。  

假設您必須更新此資料表：  

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(   [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,   [CalendarYear]                  SMALLINT        NOT NULL
,   [TotalSalesAmount]              MONEY           NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;  
```

原始的查詢可能會有看起來像下面這樣：  

```
UPDATE  acs
SET     [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT  [EnglishProductCategoryName]
        ,       [CalendarYear]
        ,       SUM([SalesAmount])              AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]       AS s
        JOIN    [dbo].[DimDate]                 AS d    ON s.[OrderDateKey]             = d.[DateKey]
        JOIN    [dbo].[DimProduct]              AS p    ON s.[ProductKey]               = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]   AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]      AS c    ON u.[ProductCategoryKey]       = c.[ProductCategoryKey]
        WHERE   [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,       [CalendarYear]
        ) AS fis
ON  [acs].[EnglishProductCategoryName]  = [fis].[EnglishProductCategoryName]
AND [acs].[CalendarYear]                = [fis].[CalendarYear]
;  
```

因為[!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]不的支援 ANSI 聯結 UPDATE 陳述式的 FROM 子句中，您無法複製此程式碼，而不需要稍微變更它。  

您可以使用 CTAS 和隱含聯結的組合來取代此程式碼：  

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT  ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,       ISNULL(CAST([CalendarYear] AS SMALLINT),0)                      AS [CalendarYear]
,       ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                     AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]       AS s
JOIN    [dbo].[DimDate]                 AS d    ON s.[OrderDateKey]             = d.[DateKey]
JOIN    [dbo].[DimProduct]              AS p    ON s.[ProductKey]               = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]   AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]      AS c    ON u.[ProductCategoryKey]       = c.[ProductCategoryKey]
WHERE   [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,       [CalendarYear]
;

-- Use an implicit join to perform the update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop the interim table
DROP TABLE CTAS_acs
;
```
  
## <a name="see-also"></a>請參閱  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [資料指標 &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [文字和影像函數 &#40;TRANSACT-SQL &#41;](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)   
 [與 common_table_expression &#40;TRANSACT-SQL &#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)   
 [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  
  
  
