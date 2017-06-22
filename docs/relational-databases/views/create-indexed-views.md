---
title: "建立索引檢視表 | Microsoft Docs"
ms.custom: 
ms.date: 05/27/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-views
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- indexed views [SQL Server], creating
- clustered indexes, views
- CREATE INDEX statement
- large_value_types_out_of_row option
- indexed views [SQL Server]
- views [SQL Server], indexed views
ms.assetid: f86dd29f-52dd-44a9-91ac-1eb305c1ca8d
caps.latest.revision: 79
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 24b4e22249ec7a175dc3ae239dea329c4d18208f
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="create-indexed-views"></a>建立索引檢視表
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中建立索引檢視表。 對檢視建立的第一個索引必須是唯一的叢集索引。 建好唯一的叢集索引後，才可以建立其他非叢集索引。 為檢視表建立唯一的叢集索引，可以提升查詢效能，因為檢視表儲存在資料庫中的方式與包含叢集索引之資料表的儲存方式一樣。 查詢最佳化工具可以利用索引檢視表來加快查詢執行的速度。 不必在查詢中參考此檢視表，最佳化工具仍會考慮以該檢視表做為替代方式。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
 以下是建立索引檢視表所需要的步驟，這些步驟對於能否順利完成索引檢視表的實作是很重要的：  
  
1.  確認檢視表中所要參考之所有現有資料表的 SET 選項是正確的。  
  
2.  先確認工作階段之 SET 選項的設定是正確的，再建立任何資料表和檢視表。  
  
3.  確認檢視表定義具決定性。  
  
4.  利用 WITH SCHEMABINDING 選項來建立檢視表。  
  
5.  在檢視表上建立唯一的叢集索引。  
  
###  <a name="Restrictions"></a> 需要索引檢視表的 SET 選項  
 如果在查詢執行時有不同的使用中 SET 選項，則評估相同的運算式可能會在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中產生不同的結果。 例如，將 SET 選項 CONCAT_NULL_YIELDS_NULL 設為 ON 之後，運算式 **'**abc**'** + NULL 會傳回 NULL 值。 不過，將 CONCAT_NULL_YIEDS_NULL 設為 OFF 之後，相同的運算式則會產生 **'**abc**'**。  
  
 若要確定檢視表可以正確地維護並傳回一致的結果，索引檢視表需要數個 SET 選項的固定值。 發生下列狀況時，必須將下表中的 SET 選項設為 [必要值] 欄中所顯示的值：  
  
-   建立檢視表和檢視表的後續索引。  
  
-   建立資料表時檢視中所參考的基底資料表。  
  
-   有在任何參與索引檢視表的資料表上執行的任何插入、更新或刪除作業。 這項需求包括大量複製、複寫及分散式查詢等作業。  
  
-   查詢最佳化工具會利用索引檢視表來產生查詢計劃。  
  
    |SET 選項|必要值|預設伺服器值|預設值<br /><br /> OLE DB 與 ODBC 值|預設值<br /><br /> DB-Library 值|  
    |-----------------|--------------------|--------------------------|---------------------------------------|-----------------------------------|  
    |ANSI_NULLS|ON|ON|ON|OFF|  
    |ANSI_PADDING|ON|ON|ON|OFF|  
    |ANSI_WARNINGS*|ON|ON|ON|OFF|  
    |ARITHABORT|ON|ON|OFF|OFF|  
    |CONCAT_NULL_YIELDS_NULL|ON|ON|ON|OFF|  
    |NUMERIC_ROUNDABORT|OFF|OFF|OFF|OFF|  
    |QUOTED_IDENTIFIER|ON|ON|ON|OFF|  
  
     *將 ANSI_WARNINGS 設為 ON 會將 ARITHABORT 隱含地設為 ON。  
  
 如果您要使用 OLE DB 或 ODBC 伺服器連接，唯一必須修改的值是 ARITHABORT 設定。 必須在伺服器層級利用 **sp_configure** 來正確地設定所有 DB-Library 值，或者，必須從應用程式利用 SET 命令來正確地設定所有 DB-Library 值。  
  
> [!IMPORTANT]  
>  強烈建議您在伺服器之任何資料庫的計算資料行上建立第一個索引檢視表或索引之後，立即在伺服器範圍將 ARITHABORT 使用者選項設為 ON。  
  
### <a name="deterministic-views"></a>具決定性的檢視  
 索引檢視表的定義必須具決定性。 如果選取清單及 WHERE 和 GROUP BY 子句中的所有運算式都具決定性，則檢視表也具決定性。 每當利用一組特定的輸入值來評估具決定性的運算式時，具決定性的運算式一律傳回相同的結果。 只有具決定性的函數可以參與具決定性的運算式。 例如，DATEADD 函數具決定性，因為它會針對它的三個參數之任何一組給定的引數值一律傳回相同的結果。 GETDATE 不具決定性，因為它一律被相同的引數叫用，但是，每當它被執行時，它所傳回的值都會變更。  
  
 若要判斷檢視表資料行是否具決定性，請使用 **COLUMNPROPERTY** 函數的 [IsDeterministic](../../t-sql/functions/columnproperty-transact-sql.md) 屬性。 若要判斷含有結構描述繫結之檢視表中的具決定性資料行是否為精確資料行，請利用 COLUMNPROPERTY 函數的 **IsPrecise** 屬性。 如果是 TRUE，COLUMNPROPERTY 會傳回 1；如果是 FALSE，則傳回 0；如果輸入無效，則傳回 NULL。 這表示這個資料行不具決定性或不是精確資料行。  
  
 即使運算式具決定性，如果它包含浮點運算式，確切的結果仍取決於處理器架構或微碼的版本而定。 若要確保資料完整性，這類運算式在參與時可以只做為索引檢視表的非索引鍵資料行。 未含浮點運算式之具決定性的運算式稱為精確運算式。 只有精確之具決定性的運算式可以參與索引鍵資料行和索引檢視表的 WHERE 或 GROUP BY 子句。  
  
> [!NOTE]  
>  不支援在暫時查詢 (使用 **FOR SYSTEM_TIME** 子句的查詢) 上方的索引檢視表  
  
### <a name="additional-requirements"></a>其他需求  
 除了 SET 選項和具決定性函數的需求以外，下列需求也必須符合：  
  
-   執行 CREATE INDEX 的使用者必須是檢視表的擁有者。  
  
-   當您建立索引時，IGNORE_DUP_KEY 選項必須設定為 OFF (預設值)。  
  
-   在檢視定義中，兩部分名稱 *schema***.***tablename* 必須參考資料表。  
  
-   檢視中所參考的使用者自訂函數，必須使用 WITH SCHEMABINDING 選項來建立。  
  
-   檢視中參考的任何使用者定義函數，必須以兩部分名稱參考 *schema***.***function*。  
  
-   使用者自訂函數的資料存取屬性必須是 NO SQL，而外部存取屬性必須是 NO。  
  
-   Common Language Runtime (CLR) 函數可以在檢視的選取清單中出現，但是不可以是叢集索引鍵定義的一部分。 CLR 函數不能出現在檢視的 WHERE 子句或檢視中之 JOIN 作業的 ON 子句。  
  
-   用於檢視定義中的 CLR 函數和 CLR 使用者定義型別的方法必須有下表所示的屬性。  
  
    |屬性|附註|  
    |--------------|----------|  
    |DETERMINISTIC = TRUE|必須明確宣告為 Microsoft .NET Framework 方法的屬性。|  
    |PRECISE = TRUE|必須明確宣告為 .NET Framework 方法的屬性。|  
    |DATA ACCESS = NO SQL|將 DataAccess 屬性設定為 DataAccessKind.None 以及將 SystemDataAccess 屬性設定為 SystemDataAccessKind.None 決定。|  
    |EXTERNAL ACCESS = NO|對 CLR 常式，此屬性預設為 NO。|  
  
-   必須利用 WITH SCHEMABINDING 選項來建立檢視表。  
  
-   檢視必須只參考與檢視位於相同資料庫中的基底資料表。 檢視不可參考其他檢視。  
  
-   檢視定義中的 SELECT 陳述式不得包含下列 Transact-SQL 元素：  
  
    ||||  
    |-|-|-|  
    |COUNT|ROWSET 函數 (OPENDATASOURCE、OPENQUERY、OPENROWSET 和 OPENXML)|OUTER 聯結 (LEFT、RIGHT 或 FULL)|  
    |衍生資料表 (藉由在 FROM 子句中指定 SELECT 陳述式定義)|自我聯結|使用 SELECT \* 或 SELECT *table_name** 指定資料行。|  
    |DISTINCT|STDEV、STDEVP、VAR、VARP 或 AVG|通用資料表運算式 (CTE)|  
    |**float**\*、 **text**、 **ntext**、 **image**、 **XML**、 or **filestream** 資料行|子查詢|OVER 子句，其中包含次序或彙總視窗函數|  
    |全文檢索述詞 (CONTAIN、FREETEXT)|SUM 函數，參考可為 Null 值的運算式|ORDER BY|  
    |CLR 使用者定義彙總函式|頂端|CUBE、ROLLUP 或 GROUPING SETS 運算子|  
    |MIN、MAX|UNION、EXCEPT 或 INTERSECT 運算子|TABLESAMPLE|  
    |資料表變數|OUTER APPLY 或 CROSS APPLY|PIVOT、UNPIVOT|  
    |疏鬆資料行集合|內嵌或多重陳述式資料表值函式|OFFSET|  
    |CHECKSUM_AGG|||  
  
     \*索引檢視表可以包含 **float** 資料行；不過，這類資料行不能併入叢集索引鍵中。  
  
-   如果有 GROUP BY，VIEW 定義必須包含 COUNT_BIG(*)，且不能包含 HAVING。 GROUP BY 限制只適用於索引檢視表定義。 即使索引檢視表不符合這些 GROUP BY 限制，查詢還是可以在它的執行計畫中使用索引檢視表。  
  
-   如果檢視表定義包含 GROUP BY 子句，唯一叢集索引的索引鍵則只能參考 GROUP BY 子句中指定的資料行。  
  
###  <a name="Recommendations"></a> 建議  
 當您在索引檢視中參考 **datetime** 和 **smalldatetime** 字串常值時，我們建議您使用決定性的日期格式樣式，將常值明確轉換成您想要的日期類型。 如需具有決定性之日期格式樣式的清單，請參閱 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)。 牽涉到將字元字串隱含轉換成 **datetime** 或 **smalldatetime** 的運算式被視為非決定性的。 這是因為結果需視伺服器工作階段的 LANGUAGE 和 DATEFORMAT 設定而定。 例如，運算式 `CONVERT (datetime, '30 listopad 1996', 113)` 的結果需視 LANGUAGE 設定而定，因為字串 '`listopad`' 在不同的語言中表示不同的月份。 同樣地，在運算式 `DATEADD(mm,3,'2000-12-01')`中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會根據 DATEFORMAT 設定解譯字串 `'2000-12-01'` 。  
  
 非 Unicode 字元資料與定序之間的隱含轉換也是視為非決定性的。  
  
###  <a name="Considerations"></a> 考量  
 索引檢視表中資料行的 **large_value_types_out_of_row** 選項設定是繼承基底資料表中對應的資料行設定。 此值可透過 [sp_tableoption](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)設定。 由運算式形成的資料行其預設值為 0。 這表示大數值類型是以資料列的方式儲存。  
  
 可以在分割區資料表上建立索引檢視表，且索引檢視表本身也可以分割。  
  
 若要防止 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 使用索引檢視表，請在查詢上併入 OPTION (EXPAND VIEWS) 提示。 另外，如果列出的選項中有任何選項設定不正確，就會防止最佳化工具使用檢視表上的索引。 如需 OPTION (EXPAND VIEWS) 提示的詳細資訊，請參閱 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)。  
  
 卸除檢視時會卸除檢視的所有索引。 如果卸除叢集索引，也會卸除檢視的所有非叢集索引。 但會保留使用者在檢視所建立的統計。 每個非叢集索引則可以分別卸除。 卸除檢視的叢集索引會刪除儲存的結果集，使最佳化工具回到以標準檢視的方式處理檢視。  
  
 您可以停用資料表與檢視的索引。 停用資料表的叢集索引時，也會停用與資料表相關之檢視的索引。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 至少必須有資料庫中的 CREATE VIEW 權限，以及正在建立之檢視表所在之結構描述的 ALTER 權限。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-an-indexed-view"></a>建立索引檢視表  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 此範例會建立檢視表並在該檢視表上建立索引。 內含使用索引檢視的兩項查詢。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    --Set the options to support indexed views.  
    SET NUMERIC_ROUNDABORT OFF;  
    SET ANSI_PADDING, ANSI_WARNINGS, CONCAT_NULL_YIELDS_NULL, ARITHABORT,  
        QUOTED_IDENTIFIER, ANSI_NULLS ON;  
    GO  
    --Create view with schemabinding.  
    IF OBJECT_ID ('Sales.vOrders', 'view') IS NOT NULL  
    DROP VIEW Sales.vOrders ;  
    GO  
    CREATE VIEW Sales.vOrders  
    WITH SCHEMABINDING  
    AS  
        SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Revenue,  
            OrderDate, ProductID, COUNT_BIG(*) AS COUNT  
        FROM Sales.SalesOrderDetail AS od, Sales.SalesOrderHeader AS o  
        WHERE od.SalesOrderID = o.SalesOrderID  
        GROUP BY OrderDate, ProductID;  
    GO  
    --Create an index on the view.  
    CREATE UNIQUE CLUSTERED INDEX IDX_V1   
        ON Sales.vOrders (OrderDate, ProductID);  
    GO  
    --This query can use the indexed view even though the view is   
    --not specified in the FROM clause.  
    SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev,   
        OrderDate, ProductID  
    FROM Sales.SalesOrderDetail AS od  
        JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
            AND ProductID BETWEEN 700 and 800  
            AND OrderDate >= CONVERT(datetime,'05/01/2002',101)  
    GROUP BY OrderDate, ProductID  
    ORDER BY Rev DESC;  
    GO  
    --This query can use the above indexed view.  
    SELECT  OrderDate, SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev  
    FROM Sales.SalesOrderDetail AS od  
        JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
            AND DATEPART(mm,OrderDate)= 3  
            AND DATEPART(yy,OrderDate) = 2002  
    GROUP BY OrderDate  
    ORDER BY OrderDate ASC;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md)   
 [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)   
 [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)  
  
  

