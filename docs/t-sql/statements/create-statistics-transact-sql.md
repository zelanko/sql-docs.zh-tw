---
title: "建立統計資料 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STATISTICS
- STATISTICS_TSQL
- CREATE STATISTICS
- CREATE_STATISTICS_TSQL
dev_langs: TSQL
helpviewer_keywords:
- query optimization statistics [SQL Server], creating
- indexed views [SQL Server], statistics
- FULLSCAN option
- CREATE STATISTICS statement
- filtered statistics [SQL Server]
- creating statistics [SQL Server]
- NORECOMPUTE clause
ms.assetid: b23e2f6b-076c-4e6d-9281-764bdb616ad2
caps.latest.revision: "105"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3e1f234dc76b6b231fc3f1d0f258937e70035a65
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="create-statistics-transact-sql"></a>CREATE STATISTICS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  建立查詢最佳化統計資料的資料表、 索引檢視表或將外部資料表的一個或多個資料行上。 對於大部分查詢而言，查詢最佳化工具已經產生高品質查詢計劃的必要統計資料。不過，在少數情況下，您必須使用 CREATE STATISTICS 來建立其他統計資料或修改查詢設計，以便改善查詢效能。  
  
 若要進一步了解，請參閱[統計資料](../../relational-databases/statistics/statistics.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Create statistics on an external table  
CREATE STATISTICS statistics_name   
ON { table_or_indexed_view_name } ( column [ ,...n ] )   
    [ WITH FULLSCAN ] ;  
  
-- Create statistics on a regular table or indexed view  
CREATE STATISTICS statistics_name   
ON { table_or_indexed_view_name } ( column [ ,...n ] )   
    [ WHERE <filter_predicate> ]  
    [ WITH   
        [ [ FULLSCAN   
            [ [ , ] PERSIST_SAMPLE_PERCENT = { ON | OFF } ]    
          | SAMPLE number { PERCENT | ROWS }   
            [ [ , ] PERSIST_SAMPLE_PERCENT = { ON | OFF } ]    
          | STATS_STREAM = stats_stream ] ]   
        [ [ , ] NORECOMPUTE ]   
        [ [ , ] INCREMENTAL = { ON | OFF } ]  
    ] ;  
  
<filter_predicate> ::=   
    <conjunct> [AND <conjunct>]  
  
<conjunct> ::=  
    <disjunct> | <comparison>  
  
<disjunct> ::=  
        column_name IN (constant ,…)  
  
<comparison> ::=  
        column_name <comparison_op> constant  
  
<comparison_op> ::=  
    IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !<  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE STATISTICS statistics_name   
    ON [ database_name . [schema_name ] . | schema_name. ] table_name   
    ( column_name  [ ,...n ] )   
    [ WHERE <filter_predicate> ]  
    [ WITH {  
           FULLSCAN   
           | SAMPLE number PERCENT   
      }  
    ]  
[;]  
  
<filter_predicate> ::=   
    <conjunct> [AND <conjunct>]  
  
<conjunct> ::=  
    <disjunct> | <comparison>  
  
<disjunct> ::=  
        column_name IN (constant ,…)  
  
<comparison> ::=  
        column_name <comparison_op> constant  
  
<comparison_op> ::=  
    IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !<  
```  
  
## <a name="arguments"></a>引數  
 *statistics_name*  
 這是要建立之統計資料的名稱。  
  
 *table_or_indexed_view_name*  
 這是資料表、 索引檢視表或在其上建立統計資料的外部資料表的名稱。 若要在另一個資料庫上建立統計資料，請指定限定的資料表名稱。  
  
 *資料行 [，… n]*  
 一或多個要包含資料行的統計資料。 資料行應該依優先順序從左到右。 第一個資料行用來建立長條圖。 所有資料行可用於跨資料行相互關聯統計資料稱為密度。  
  
 您可以指定任何可指定為索引鍵資料行的資料行，但下列例外狀況除外：  
  
-   **Xml**，全文檢索和 FILESTREAM 資料行不能指定。  
  
-   只有在 ARITHABORT 和 QUOTED_IDENTIFIER 資料庫設定為 ON 時，才能指定計算資料行。  
  
-   如果 CLR 使用者定義型別可支援二進位排序，您可以指定這個類型的資料行。 如果方法標示為具決定性，就能指定從使用者定義型別資料行中定義為方法引動過程的計算資料行。  
  
 其中\<filter_predicate > 指定用於選取要建立統計資料物件時加入的資料列子集運算式。 使用篩選述詞所建立的統計資料稱為篩選的統計資料。 篩選器述詞使用簡單比較邏輯，而且無法參考計算資料行、 UDT 資料行、 空間資料類型資料行或**hierarchyID**資料類型資料行。 比較運算子不允許使用 NULL 常值的比較。 請改用 IS NULL 和 IS NOT NULL 運算子。  
  
 以下是 Production.BillOfMaterials 資料表之篩選述詞的一些範例：  
  
 `WHERE StartDate > '20000101' AND EndDate <= '20000630'`  
  
 `WHERE ComponentID IN (533, 324, 753)`  
  
 `WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL`  
  
 如需有關篩選器述詞的詳細資訊，請參閱[Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)。  
  
 FULLSCAN  
 掃描所有資料列計算統計資料。 FULLSCAN 和 SAMPLE 100 PERCENT 的結果相同。 FULLSCAN 不能搭配 SAMPLE 選項一起使用。  
  
 當略過，SQL Server 建立統計資料，會使用取樣，並判斷，才能建立高品質查詢計劃的取樣大小  
  
 範例*數目*{%|資料列}  
 指定當查詢最佳化工具建立統計資料時，要在資料表或索引檢視表中使用的近似百分比或資料列數目。 Percent，*數目*可以介於 0 到 100 之間，然後針對資料列，*數目*可以介於 0 到資料列總數。 查詢最佳化工具所取樣的實際百分比或資料列數目可能會與指定的百分比或數目不符。 例如，查詢最佳化工具會掃描資料頁面上的所有資料列。  
  
 在特殊情況下，根據預設取樣的查詢計劃並非最佳化，此時 SAMPLE 便非常有用。 通常，查詢最佳化工具已經會依預設使用取樣並決定具有統計價值的取樣大小，因此不需要使用 SAMPLE 便可以建立高品質的查詢計劃。  
  
 SAMPLE 不能和 FULLSCAN 選項一起使用。 如果 SAMPLE 或 FULLSCAN 都未指定，查詢最佳化工具會依預設使用取樣資料並計算取樣大小。  
  
 我們建議您不要指定 0 PERCENT 或 0 ROWS。 將 PERCENT 或 ROWS 指定為 0 時，雖會建立統計資料物件，但是不會包含統計資料。  
 
 PERSIST_SAMPLE_PERCENT = {ON |OFF}  
 當**ON**，統計資料將會保留未明確指定取樣百分比的後續更新建立取樣百分比。 當**OFF**，統計資料取樣百分比便會重設預設取樣中未明確指定取樣百分比的後續更新。 預設值是**OFF**。 
 
 **適用於**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (開頭為[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1 CU4) 透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)](開頭為[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU1)。    
  
 STATS_STREAM  **=**  *stats_stream*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 NORECOMPUTE  
 停用自動統計資料更新選項 AUTO_STATISTICS_UPDATE *statistics_name*。 如果指定此選項，查詢最佳化工具將會完成任何進行中的統計資料更新*statistics_name*並停用未來的更新。  
  
 若要重新啟用統計資料更新，請移除與統計資料[DROP STATISTICS](../../t-sql/statements/drop-statistics-transact-sql.md) ，然後執行不含 NORECOMPUTE 選項的 建立統計資料。  
  
> [!WARNING]  
>  使用這個選項可能會產生次佳查詢計劃。 我們建議您盡量少用這個選項，而且只有合格的系統管理員可以使用。  
  
 如需有關 AUTO_STATISTICS_UPDATE 選項的詳細資訊，請參閱[ALTER DATABASE SET 選項 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md). 如需有關停用並重新啟用統計資料更新的詳細資訊，請參閱[統計資料](../../relational-databases/statistics/statistics.md)。  
  
 INCREMENTAL = { ON | OFF }  
 當**ON**，建立的統計資料是以每個分割區統計資料。 當**OFF**，統計資料會合併所有的磁碟分割。 預設值是**OFF**。  
  
 如果不支援依據每個分割區區的統計資料，則會產生錯誤。 針對下列統計資料類型，不支援累加統計資料：  
  
-   建立統計資料時，所使用的索引未與基底資料表進行分割區對齊。  
  
-   在 AlwaysOn 可讀取次要資料庫上建立的統計資料。  
  
-   在唯讀資料庫上建立的統計資料。  
  
-   在篩選的索引上建立的統計資料。  
  
-   在檢視上建立的統計資料。  
  
-   在內部資料表上建立的統計資料。  
  
-   使用空間索引或 XML 索引建立的統計資料。  
  
**適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
## <a name="permissions"></a>Permissions  
 需要這些權限之一：  
  
-   ALTER TABLE  
  
-   使用者是資料表擁有者  
  
-   中的成員資格**db_ddladmin**固定的資料庫角色  
  
## <a name="general-remarks"></a>一般備註  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以使用 tempdb 來排序之前建立統計資料取樣的資料列。  
  
### <a name="statistics-for-external-tables"></a>外部資料表的統計資料  
 建立外部資料表的統計資料時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]外部資料表匯入暫存[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表，並接著會建立統計資料。 如範例的統計資料，匯入取樣資料列。 如果您有大型的外部資料表，它會使用預設取樣來代替完整掃描選項更快。  
  
### <a name="statistics-with-a-filtered-condition"></a>統計資料的篩選條件  
 對於從定義完善的資料子集中選取的查詢而言，篩選的統計資料可以改善查詢效能。 篩選的統計資料會在 WHERE 子句中使用篩選述詞來選取統計資料中所含的資料子集。  
  
### <a name="when-to-use-create-statistics"></a>使用 CREATE STATISTICS 的時機  
 使用 CREATE STATISTICS 之時機的詳細資訊，請參閱[統計資料](../../relational-databases/statistics/statistics.md)。  
  
### <a name="referencing-dependencies-for-filtered-statistics"></a>篩選統計資料的參考相依性  
 [Sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)目錄檢視追蹤篩選的統計資料述詞做參考相依性中的每個資料行。 請在建立篩選統計資料之前先考慮要在資料表資料行上執行的作業，因為在篩選統計資料述詞中定義的資料表資料行是無法卸除、重新命名或變更定義的。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
*  外部資料表不支援更新統計資料。 若要更新統計資料的外部資料表，卸除並重新建立統計資料。  
*  您可以列出每個統計資料物件的最多 64 個資料行。
  
## <a name="examples"></a>範例  

### <a name="examples-use-the-adventureworks-database"></a>範例會使用 AdventureWorks 資料庫。  

### <a name="a-using-create-statistics-with-sample-number-percent"></a>A. 搭配 SAMPLE 數目 PERCENT 使用 CREATE STATISTICS  
 下列範例會建立 `ContactMail1` 統計資料，其方式是使用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫之 `BusinessEntityID` 資料表內，`EmailPromotion` 和 `Contact` 資料行的 5% 隨機取樣。  
  
```t-sql  
CREATE STATISTICS ContactMail1  
    ON Person.Person (BusinessEntityID, EmailPromotion)  
    WITH SAMPLE 5 PERCENT;  
```  
  
### <a name="b-using-create-statistics-with-fullscan-and-norecompute"></a>B. 搭配 FULLSCAN 和 NORECOMPUTE 使用 CREATE STATISTICS  
 下列範例會針對 `ContactMail2` 資料表的 `BusinessEntityID` 和 `EmailPromotion` 資料行中的所有資料列來建立 `Contact` 統計資料，且會停用統計資料的自動重新計算。  
  
```t-sql  
CREATE STATISTICS NamePurchase  
    ON AdventureWorks2012.Person.Person (BusinessEntityID, EmailPromotion)  
    WITH FULLSCAN, NORECOMPUTE;  
```  
  
### <a name="c-using-create-statistics-to-create-filtered-statistics"></a>C. 使用 CREATE STATISTICS 來建立篩選的統計資料  
 下列範例會建立篩選的統計資料 `ContactPromotion1`。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會取樣百分之 50 的資料，然後選取 `EmailPromotion` 等於 2 的所有資料列。  
  
```t-sql  
CREATE STATISTICS ContactPromotion1  
    ON Person.Person (BusinessEntityID, LastName, EmailPromotion)  
WHERE EmailPromotion = 2  
WITH SAMPLE 50 PERCENT;  
GO  
```  
  
### <a name="d-create-statistics-on-an-external-table"></a>D. 建立外部資料表的統計資料  
 您必須先將外部資料表，除了提供資料行清單上建立統計資料時的決策在於要取樣的資料列或掃描所有資料列建立統計資料。  
  
 因為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]匯入資料至暫存資料表建立統計資料，完整掃描選項的外部資料表將花更長時間。 在大型資料表，預設取樣方法通常已足夠。  
  
```t-sql  
--Create statistics on an external table and use default sampling.  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress);  
  
--Create statistics on an external table and scan all the rows  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress) WITH FULLSCAN;  
```  

### <a name="e-using-create-statistics-with-fullscan-and-persistsamplepercent"></a>E. 使用 CREATE STATISTICS 搭配 FULLSCAN 和 PERSIST_SAMPLE_PERCENT  
 下列範例會建立`ContactMail2`統計資料的所有資料列`BusinessEntityID`和`EmailPromotion`的資料行`Contact`資料表，並設定所有的後續更新執行不明確地指定取樣百分之 100 取樣百分比百分比。  
  
```t-sql  
CREATE STATISTICS NamePurchase  
    ON AdventureWorks2012.Person.Person (BusinessEntityID, EmailPromotion)  
    WITH FULLSCAN, PERSIST_SAMPLE_PERCENT = ON;  
```  
  
### <a name="examples-using-adventureworksdw-database"></a>使用 AdventureWorksDW 資料庫的範例。 
  
### <a name="f-create-statistics-on-two-columns"></a>F. 在兩個資料行上建立統計資料  
 下列範例會建立`CustomerStats1`統計資料，根據`CustomerKey`和`EmailAddress`的資料行`DimCustomer`資料表。 根據具有統計價值的取樣中的資料列建立統計資料`Customer`資料表。  
  
```t-sql  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress);  
```  
  
### <a name="g-create-statistics-by-using-a-full-scan"></a>G. 使用完整掃描來建立統計資料  
 下列範例會建立`CustomerStatsFullScan`統計資料，根據掃描中的資料列的所有`DimCustomer`資料表。  
  
```t-sql  
CREATE STATISTICS CustomerStatsFullScan 
ON DimCustomer (CustomerKey, EmailAddress) WITH FULLSCAN;  
```  
  
### <a name="h-create-statistics-by-specifying-the-sample-percentage"></a>H. 藉由指定取樣百分比建立統計資料  
 下列範例會建立`CustomerStatsSampleScan`統計資料，根據掃描中的資料列的 50%`DimCustomer`資料表。  
  
```t-sql  
CREATE STATISTICS CustomerStatsSampleScan 
ON DimCustomer (CustomerKey, EmailAddress) WITH SAMPLE 50 PERCENT;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [統計資料](../../relational-databases/statistics/statistics.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [sys.stats_columns &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)  
  
  

