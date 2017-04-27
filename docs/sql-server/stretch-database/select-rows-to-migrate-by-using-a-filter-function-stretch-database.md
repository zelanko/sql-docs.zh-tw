---
title: "使用篩選函數選取要移轉的資料列 (Stretch Database) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/27/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, predicates
- predicates for Stretch Database
- Stretch Database, inline table-valued functions
- inline table-valued functions for Stretch Database
ms.assetid: 090890ee-7620-4a08-8e15-d2fbc71dd12f
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 097d613e8732823d91d660f6e8a0c1f6d749fb39
ms.lasthandoff: 04/11/2017

---
# <a name="select-rows-to-migrate-by-using-a-filter-function-stretch-database"></a>使用篩選函數選取要移轉的資料列 (Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  若您將原始資料儲存在其他資料表中，您可以設定 Stretch Database 以移轉整個資料表。 若您的資料表同時包含作用及原始資料，則可以指定篩選器述詞，以選取要移轉的資料列。 篩選器述詞是內嵌資料表值函數。 本主題說明如何撰寫內嵌資料表值函數，以選取要遷移的資料列。  
  
> [!IMPORTANT]
> 若您提供執行狀況不佳的篩選函數，資料移轉也無法順利執行。 Stretch Database 使用 CROSS APPLY 運算子，將篩選函數套用至資料表。  
  
 若您未指定篩選函數，則會移轉整個資料表。  
  
 當您執行 [啟用資料庫的延展功能精靈] 時，可以移轉整個資料表，也可以在精靈中指定簡單的篩選函數。 如果您想要使用不同類型的篩選函數來選取要遷移的資料列，請執行下列其中一項操作。  
  
-   結束精靈，然後執行 ALTER TABLE 陳述式來啟用資料表的延展功能以及指定篩選函數。  
  
-   結束精靈之後，請執行 ALTER TABLE 陳述式來指定篩選函數。  
  
 本主題稍後會說明用於新增函數的 ALTER TABLE 語法。  
  
## <a name="basic-requirements-for-the-filter-function"></a>篩選函數的基本需求  
 Stretch Database 篩選器述詞需要的內嵌資料表值函數如同下列範例所示。  
  
```tsql  
CREATE FUNCTION dbo.fn_stretchpredicate(@column1 datatype1, @column2 datatype2 [, ...n])  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE <predicate>  
```  
  
 函數的參數必須是資料表中資料行的識別碼。  
  
 需要結構描述繫結，才能避免篩選函數所使用的資料行遭到卸除或改變。  
  
### <a name="return-value"></a>傳回值  
 若函數傳回非空白結果，資料列便符合遷移資格。 否則若函數未傳回結果，則資料列不適合進行遷移。  
  
### <a name="conditions"></a>條件  
 &lt;*predicate*&gt; 可包含一個條件，或使用 AND 邏輯運算子聯結多個條件。  
  
```  
<predicate> ::= <condition> [ AND <condition> ] [ ...n ]  
```  
  
 每個條件則可包含一個基本條件，或使用 OR 邏輯運算子聯結多個基本條件。  
  
```  
<condition> ::= <primitive_condition> [ OR <primitive_condition> ] [ ...n ]  
```  
  
### <a name="primitive-conditions"></a>基本條件  
 基本條件可執行下列其中一個比較。  
  
```  
<primitive_condition> ::=   
{  
<function_parameter> <comparison_operator> constant  
| <function_parameter> { IS NULL | IS NOT NULL }  
| <function_parameter> IN ( constant [ ,...n ] )  
}  
  
```  
  
-   比較函數參數與常數運算式。 例如， `@column1 < 1000`。  
  
     以下範例會檢查 *date* 資料行的值是否為 &lt; 1/1/2016。  
  
    ```tsql  
    CREATE FUNCTION dbo.fn_stretchpredicate(@column1 datetime)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 < CONVERT(datetime, '1/1/2016', 101)  
    GO  
  
    ALTER TABLE stretch_table_name SET ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(date),  
        MIGRATION_STATE = OUTBOUND  
    ) )  
  
    ```  
  
-   將 IS NULL 或 IS NOT NULL 運算子套用至函數參數。  
  
-   使用 IN 運算子比較函數參數與常數值清單。  
  
     以下範例會檢查 *shipment_status*  資料行的值是否為 `IN (N'Completed', N'Returned', N'Cancelled')`。  
  
    ```tsql  
    CREATE FUNCTION dbo.fn_stretchpredicate(@column1 nvarchar(15))  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 IN (N'Completed', N'Returned', N'Cancelled')  
    GO  
  
    ALTER TABLE table1 SET ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(shipment_status),  
        MIGRATION_STATE = OUTBOUND  
    ) )  
  
    ```  
  
### <a name="comparison-operators"></a>比較運算子  
 下列為支援的比較運算子。  
  
 `<, <=, >, >=, =, <>, !=, !<, !>`  
  
```  
<comparison_operator> ::= { < | <= | > | >= | = | <> | != | !< | !> }  
```  
  
### <a name="constant-expressions"></a>常數運算式  
 您在篩選函數中使用的常數可以是任何確定性的運算式，其可在定義函數時接受評估。 常數運算式可包含下列項目。  
  
-   常值。 例如， `N’abc’, 123`。  
  
-   代數運算式。 例如， `123 + 456`。  
  
-   確定性函數。 例如， `SQRT(900)`。  
  
-   使用 CAST 或 CONVERT 的確定性轉換。 例如， `CONVERT(datetime, '1/1/2016', 101)`。  
  
### <a name="other-expressions"></a>其他運算式  
 在使用對等 AND 及 OR 運算式取代 BETWEEN 及 NOT BETWEEN 運算子後，若產生的函數符合此處所述的規則，您就可以使用 BETWEEN 及 NOT BETWEEN 運算子。  
  
 您無法使用子查詢或非確定性的函數，例如 RAND() 或 GETDATE()。  
  
## <a name="add-a-filter-function-to-a-table"></a>將篩選函數加入資料表  
 執行 **ALTER TABLE** 陳述式，以將篩選函數加入資料表中，並將現有內嵌資料表值函數指定為 **FILTER_PREDICATE** 參數的值。 例如：  
  
```tsql  
ALTER TABLE stretch_table_name SET ( REMOTE_DATA_ARCHIVE = ON (  
    FILTER_PREDICATE = dbo.fn_stretchpredicate(column1, column2),  
    MIGRATION_STATE = <desired_migration_state>  
) )  
  
```  
  
 當您將函數繫結至資料表作為述詞後，下列描述即成立。  
  
-   下一次資料移轉時，只會遷移函數傳回非空白值的資料列。  
  
-   函數所使用的資料行是結構描述繫結。 只要資料表仍使用函數作為其篩選器述詞，您就無法變更這些資料行。  
  
 只要資料表仍使用函數作為其篩選器述詞，您就無法卸除內嵌資料表值函數。 

> [!TIP]
> 若要改善篩選函數的效能，請在函數使用的資料行上建立索引。

 ### <a name="passing-column-names-to-the-filter-function"></a>將資料行名稱傳遞給篩選函數
 
 當您指派篩選函數給資料表時，請使用一段式名稱來指定傳遞給篩選函數的資料行名稱。 如果您在傳遞資料行名稱時指定的是三段式名稱，後續針對已啟用延展功能之資料表的查詢將會失敗。

例如，如果您指定三段式資料行名稱 (如以下範例所示)，陳述式將會執行成功，但後續針對資料表的查詢將會失敗。

```tsql
ALTER TABLE SensorTelemetry 
  SET ( REMOTE_DATA_ARCHIVE = ON (
    FILTER_PREDICATE=dbo.fn_stretchpredicate(dbo.SensorTelemetry.ScanDate),
    MIGRATION_STATE = OUTBOUND )
  )
```

請改為使用一段式資料行名稱來指定篩選函數，如以下範例所示。

```tsql
ALTER TABLE SensorTelemetry 
  SET ( REMOTE_DATA_ARCHIVE = ON  (
    FILTER_PREDICATE=dbo.fn_stretchpredicate(ScanDate),
    MIGRATION_STATE = OUTBOUND )
  )
```
  
## <a name="addafterwiz"></a>在執行精靈後新增篩選函數  
  
如果您想要使用無法在 [啟用資料庫的延展功能精靈] 中建立的函數，您可以在結束精靈後，執行 **ALTER TABLE** 陳述式來指定函數。 不過，您必須先停止已經在進行中的資料移轉並回復已移轉的資料，才能套用函數。 (如需為什麼必須這麼做的詳細資訊，請參閱 [取代現有的篩選函數](#replacePredicate)。)
  
1. 反轉移轉方向並回復已經移轉的資料。 這項作業開始之後，即無法將其取消。 您也會因輸出資料傳輸 (輸出) 而在 Azure 上產生費用。 如需詳細資訊，請參閱 [Azure 定價機制](https://azure.microsoft.com/pricing/details/data-transfers/)。  
  
    ```tsql  
    ALTER TABLE <table name>  
        SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = INBOUND ) ) ;   
    ```  
  
2. 等待移轉完成。 您可以在 SQL Server Management Studio 的 [延展資料庫監視器] 中或查詢 **sys.dm_db_rda_migration_status** 檢視，來查看狀態。 如需詳細資訊，請參閱[資料移轉的監視及疑難排解](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)或 [sys.dm_db_rda_migration_status](../../relational-databases/system-dynamic-management-views/stretch-database-sys-dm-db-rda-migration-status.md)。  
  
3. 建立您想要套用至資料表的篩選函數。  
  
4. 將函數加入資料表，然後重新啟動資料移轉來移轉到 Azure。  
  
    ```tsql  
    ALTER TABLE <table name>  
        SET ( REMOTE_DATA_ARCHIVE  
            (           
                FILTER_PREDICATE = <predicate>,  
                MIGRATION_STATE = OUTBOUND  
            )  
            );   
    ```  
  
## <a name="filter-rows-by-date"></a>依日期篩選資料列  
 下列範例會遷移資料列，其中 **date** 資料行包含早於 2016 年 1 月 1 日的值。  
  
```tsql  
-- Filter by date  
--  
CREATE FUNCTION dbo.fn_stretch_by_date(@date datetime2)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
       RETURN SELECT 1 AS is_eligible WHERE @date < CONVERT(datetime2, '1/1/2016', 101)  
GO  
  
```  
  
## <a name="filter-rows-by-the-value-in-a-status-column"></a>依狀態資料行中的值篩選資料列  
 下列範例會遷移資料列，其中 **status** 資料行包含其中一個指定的值。  
  
```tsql  
-- Filter by status column  
--  
CREATE FUNCTION dbo.fn_stretch_by_status(@status nvarchar(128))  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
       RETURN SELECT 1 AS is_eligible WHERE @status IN (N'Completed', N'Returned', N'Cancelled')  
GO  
  
```  
  
## <a name="filter-rows-by-using-a-sliding-window"></a>使用滑動視窗篩選資料列  
 若要使用滑動視窗篩選資料列，請牢記下列篩選函數的需求。  
  
-   函數必須為確定性函數。 因此您無法建立會隨著時間推移，而自動重新計算的滑動視窗函數。  
  
-   函數使用結構描述繫結。 因此您無法僅透過呼叫 **ALTER FUNCTION** 來移動滑動視窗，以每天「就地」更新函數。  
  
 遵循下列範例開始使用篩選函數，此範例會移遷資料列，其中 **systemEndTime** 資料行包含早於 2016 年 1 月 1 日的值。  
  
```tsql  
CREATE FUNCTION dbo.fn_StretchBySystemEndTime20160101(@systemEndTime datetime2)   
RETURNS TABLE   
WITH SCHEMABINDING    
AS    
RETURN SELECT 1 AS is_eligible   
  WHERE @systemEndTime < CONVERT(datetime2, '2016-01-01T00:00:00', 101) ;  
  
```  
  
 將篩選函數套用至資料表。  
  
```tsql  
ALTER TABLE <table name>   
SET (   
        REMOTE_DATA_ARCHIVE = ON   
                (   
                        FILTER_PREDICATE = dbo.fn_StretchBySystemEndTime20160101(SysEndTime)  
                                , MIGRATION_STATE = OUTBOUND   
                )  
        )   
;  
  
```  
  
 當您想更新滑動視窗時，請執行下列動作。  
  
1.  建立新的函數，以指定新的滑動視窗。 下列範例選取的日期早於 2016 年 1 月 2 日，而非 2016 年 1 月 1 日。  
  
2.  藉由呼叫 **ALTER TABLE**，以新的篩選函數取代先前的篩選函數，如下列範例所示。  
  
3.  您可以選擇呼叫 **DROP FUNCTION**，卸除您不再使用的篩選函數。 (範例中未顯示此步驟)。  
  
```tsql  
BEGIN TRAN  
GO  
        /*(1) Create new predicate function definition */  
        CREATE FUNCTION dbo.fn_StretchBySystemEndTime20160102(@systemEndTime datetime2)  
        RETURNS TABLE  
        WITH SCHEMABINDING   
        AS   
        RETURN SELECT 1 AS is_eligible  
               WHERE @systemEndTime < CONVERT(datetime2,'2016-01-02T00:00:00', 101)  
        GO  
  
        /*(2) Set the new function as the filter predicate */  
        ALTER TABLE <table name>  
        SET   
        (  
               REMOTE_DATA_ARCHIVE = ON  
               (  
                       FILTER_PREDICATE = dbo.fn_StretchBySystemEndTime20160102(SysEndTime),  
                       MIGRATION_STATE = OUTBOUND  
               )  
        )   
COMMIT ;  
  
```  
  
## <a name="more-examples-of-valid-filter-functions"></a>有效篩選函數的其他範例  
  
-   下列範例使用 AND 邏輯運算子將兩個基本條件結合。  
  
    ```tsql  
    CREATE FUNCTION dbo.fn_stretchpredicate((@column1 datetime, @column2 nvarchar(15))  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
      WHERE @column1 < N'20150101' AND @column2 IN (N'Completed', N'Returned', N'Cancelled')  
    GO  
  
    ALTER TABLE table1 SET ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(date, shipment_status),  
        MIGRATION_STATE = OUTBOUND  
    ) )  
  
    ```  
  
-   下列範例以 CONVERT 使用數個條件及一個確定性轉換。  
  
    ```tsql  
    CREATE FUNCTION dbo.fn_stretchpredicate_example1(@column1 datetime, @column2 int, @column3 nvarchar)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2015', 101) AND (@column2 < -100 OR @column2 > 100 OR @column2 IS NULL) AND @column3 IN (N'Completed', N'Returned', N'Cancelled')  
    GO  
  
    ```  
  
-   下列範例使用數學運算子及函數。  
  
    ```tsql  
    CREATE FUNCTION dbo.fn_stretchpredicate_example2(@column1 float)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 < SQRT(400) + 10  
    GO  
  
    ```  
  
-   下列範例使用 BETWEEN 及 NOT BETWEEN 運算子。 在使用對等 AND 及 OR 運算式取代 BETWEEN 及 NOT BETWEEN 運算子後，產生的函數符合此處所述的規則，所以使用方式有效。  
  
    ```tsql  
    CREATE FUNCTION dbo.fn_stretchpredicate_example3(@column1 int, @column2 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 BETWEEN 0 AND 100  
                AND (@column2 NOT BETWEEN 200 AND 300 OR @column1 = 50)  
    GO  
  
    ```  
  
     在使用對等 AND 及 OR 運算式取代 BETWEEN 及 NOT BETWEEN 運算子後，之前的函數即相當於下列函數。  
  
    ```tsql  
    CREATE FUNCTION dbo.fn_stretchpredicate_example4(@column1 int, @column2 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 >= 0 AND @column1 <= 100 AND (@column2 < 200 OR @column2 > 300 OR @column1 = 50)  
    GO  
  
    ```  
  
## <a name="examples-of-filter-functions-that-arent-valid"></a>無效篩選函數的範例  
  
-   因為下列函數包含非確定性轉換，所以無效。  
  
    ```tsql  
    CREATE FUNCTION dbo.fn_example5(@column1 datetime)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 < CONVERT(datetime, '1/1/2016')  
    GO  
  
    ```  
  
-   因為下列函數包含非確定性函數呼叫，所以無效。  
  
    ```tsql  
    CREATE FUNCTION dbo.fn_example6(@column1 datetime)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 < DATEADD(day, -60, GETDATE())  
    GO  
  
    ```  
  
-   因為下列函數包含子查詢，所以無效。  
  
    ```tsql  
    CREATE FUNCTION dbo.fn_example7(@column1 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 IN (SELECT SupplierID FROM Supplier WHERE Status = 'Defunct')  
    GO  
  
    ```  
  
-   因為必須在定義函數時，將使用代數運算子或內建函數的運算式評估為常數，所以下列函數無效。 代數運算式或函數呼叫中不能包括資料行參考。  
  
    ```tsql  
    CREATE FUNCTION dbo.fn_example8(@column1 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 % 2 =  0  
    GO  
  
    CREATE FUNCTION dbo.fn_example9(@column1 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE SQRT(@column1) = 30  
    GO  
  
    ```  
  
-   在使用對等 AND 運算式取代 BETWEEN 運算子後，因為下列函數違反此處所述的規則，所以無效。  
  
    ```tsql  
    CREATE FUNCTION dbo.fn_example10(@column1 int, @column2 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING  
    AS  
    RETURN  SELECT 1 AS is_eligible  
            WHERE (@column1 BETWEEN 1 AND 200 OR @column1 = 300) AND @column2 > 1000  
    GO  
  
    ```  
  
     在使用對等 AND 運算式取代 BETWEEN運算子後，之前的函數即相當於下列函數。 因為基本條件只能使用 OR 邏輯運算子，所以此函數無效。  
  
    ```tsql  
    CREATE FUNCTION dbo.fn_example11(@column1 int, @column2 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE (@column1 >= 1 AND @column1 <= 200 OR @column1 = 300) AND @column2 > 1000  
    GO  
  
    ```  
  
## <a name="how-stretch-database-applies-the-filter-function"></a>Stretch Database 如何套用篩選函數  
 Stretch Database 會使用 CROSS APPLY 運算子將篩選函數套用至資料表，並判斷合格的資料列。 例如：  
  
```tsql  
SELECT * FROM stretch_table_name CROSS APPLY fn_stretchpredicate(column1, column2)  
```  
  
 若函數為資料列傳回非空白結果，資料列便符合遷移資格。  
  
## <a name="replacePredicate"></a>取代現有的篩選函數  
 您可再次執行 **ALTER TABLE** 陳述式，並為 **FILTER_PREDICATE** 參數指定新的值，以取代先前指定的篩選函數。 例如：  
  
```tsql  
ALTER TABLE stretch_table_name SET ( REMOTE_DATA_ARCHIVE = ON (  
    FILTER_PREDICATE = dbo.fn_stretchpredicate2(column1, column2),  
    MIGRATION_STATE = <desired_migration_state>  
  
```  
  
 新的內嵌資料表值函數具有下列需求。  
  
-   新的函數限制不能多於先前的函數。  
  
-   舊函數中的所有運算子都必須存在於新的函數中。  
  
-   新的函數不能包含不存在於舊函數中的運算子。  
  
-   無法變更運算子引數的順序。  
  
-   只有屬於 `<, <=, >, >=`  比較的常數值，可透過減少函數限制的方式進行變更。  
  
### <a name="example-of-a-valid-replacement"></a>有效取代的範例  
 假設下列函數是目前的篩選函數。  
  
```tsql  
CREATE FUNCTION dbo.fn_stretchpredicate_old(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2016', 101)  
            AND (@column2 < -100 OR @column2 > 100)  
GO  
  
```  
  
 因為新的日期常數 (指定了較晚的截止日期)，使函數的限制變少，所以下列函數是有效取代。  
  
```tsql  
CREATE FUNCTION dbo.fn_stretchpredicate_new(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '2/1/2016', 101)  
            AND (@column2 < -50 OR @column2 > 50)  
GO  
  
```  
  
### <a name="examples-of-replacements-that-arent-valid"></a>無效取代的範例  
 因為新的日期常數 (指定了較早的截止日期) 並未使函數限制變少，所以下列函數不是有效取代。  
  
```tsql  
CREATE FUNCTION dbo.fn_notvalidreplacement_1(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2015', 101)  
            AND (@column2 < -100 OR @column2 > 100)  
GO  
  
```  
  
 因為已經移除其中一個比較運算子，所以下列函數不是有效取代。  
  
```tsql  
CREATE FUNCTION dbo.fn_notvalidreplacement_2(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2016', 101)  
            AND (@column2 < -50)  
GO  
  
```  
  
 因為已使用 AND 邏輯運算子加入新的條件，所以下列函數不是有效取代。  
  
```tsql  
CREATE FUNCTION dbo.fn_notvalidreplacement_3(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2016', 101)  
            AND (@column2 < -100 OR @column2 > 100)  
            AND (@column2 <> 0)  
GO  
  
```  
  
## <a name="remove-a-filter-function-from-a-table"></a>從資料表移除篩選函數  
 若要移轉整個資料表，而非只移轉選取的資料列，請將 **FILTER_PREDICATE**  設定為 null 來移除現有的函數。 例如：  
  
```tsql  
ALTER TABLE stretch_table_name SET ( REMOTE_DATA_ARCHIVE = ON (  
    FILTER_PREDICATE = NULL,  
    MIGRATION_STATE = <desired_migration_state>  
) )  
  
```  
  
 移除篩選函數後，則資料表中的所有資料列都適合進行移轉。 如此一來，您稍後便無法為相同的資料表指定篩選函數，除非您先回復所有 Azure 資料表的遠端資料。 此限制用以避免以下情況：當您提供已移轉至 Azure 的新篩選函數時，資料列不符合移轉資格。  
  
## <a name="check-the-filter-function-applied-to-a-table"></a>檢查篩選函數是否已套用至資料表  
 若要檢查篩選函數是否已套用至資料表，請開啟目錄檢視 **sys.remote_data_archive_tables** ，並檢查 **filter_predicate** 資料行的值。 若值為 null，則整個資料表都適合進行封存。 如需詳細資訊，請參閱 [sys.remote_data_archive_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-tables.md)。  
  
## <a name="security-notes-for-filter-functions"></a>篩選函數的安全性注意事項  
遭盜用的帳戶若具備 db_owner 權限，便能夠執行下列操作。  
  
-   建立並套用耗用大量伺服器資源或長期等待而導致阻斷服務的資料表值函數。  
  
-   建立並套用可能推斷出已明確拒絕使用者讀取之資料表內容的資料表值函數。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  

