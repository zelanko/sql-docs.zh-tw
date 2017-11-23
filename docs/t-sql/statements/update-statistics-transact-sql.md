---
title: "UPDATE STATISTICS (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 11/20/2017
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
- UPDATE STATISTICS
- UPDATE_STATISTICS_TSQL
dev_langs: TSQL
helpviewer_keywords:
- updating statistics
- query optimization statistics [SQL Server], updating
- UPDATE STATISTICS statement
- statistical information [SQL Server], updating
ms.assetid: 919158f2-38d0-4f68-82ab-e1633bd0d308
caps.latest.revision: "74"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 96ace864a1cff7724451b521db4b184323db6d8e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="update-statistics-transact-sql"></a>UPDATE STATISTICS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對資料表或索引檢視表更新查詢最佳化統計資料。 根據預設，查詢最佳化工具已經更新統計資料來改善查詢計劃; 視在某些情況下您可以使用 UPDATE STATISTICS 或預存程序來改善查詢效能[sp_updatestats](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)更新統計資料更新頻率高於預設更新頻率。  
  
 更新統計資料可確保查詢使用最新的統計資料進行編譯。 不過，更新統計資料會導致查詢重新編譯。 我們建議您不要太頻繁地更新統計資料，因為改善查詢計劃與重新編譯查詢所花費的時間之間具有效能權衡取捨。 特定的權衡取捨完全取決於您的應用程式。 UPDATE STATISTICS 可以使用 tempdb 來排序資料列的範例，以便建立統計資料。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
UPDATE STATISTICS table_or_indexed_view_name   
    [   
        {   
            { index_or_statistics__name }  
          | ( { index_or_statistics_name } [ ,...n ] )   
                }  
    ]   
    [    WITH   
        [  
            FULLSCAN   
              [ [ , ] PERSIST_SAMPLE_PERCENT = { ON | OFF } ]    
            | SAMPLE number { PERCENT | ROWS }   
              [ [ , ] PERSIST_SAMPLE_PERCENT = { ON | OFF } ]    
            | RESAMPLE   
              [ ON PARTITIONS ( { <partition_number> | <range> } [, …n] ) ]  
            | <update_stats_stream_option> [ ,...n ]  
        ]   
        [ [ , ] [ ALL | COLUMNS | INDEX ]   
        [ [ , ] NORECOMPUTE ]   
        [ [ , ] INCREMENTAL = { ON | OFF } ]  
    ] ;  
  
<update_stats_stream_option> ::=  
    [ STATS_STREAM = stats_stream ]  
    [ ROWCOUNT = numeric_constant ]  
    [ PAGECOUNT = numeric_contant ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
UPDATE STATISTICS schema_name . ] table_name   
    [ ( { statistics_name | index_name } ) ]  
    [ WITH   
       {  
              FULLSCAN   
            | SAMPLE number PERCENT   
            | RESAMPLE   
        }  
    ]  
[;]  
```  
  
## <a name="arguments"></a>引數  
 *table_or_indexed_view_name*  
 這是資料表或索引檢視表包含統計資料物件的名稱。  
  
 *index_or_statistics_name*  
 這是要更新統計資料之索引的名稱，或是要更新之統計資料的名稱。 如果*index_or_statistics_name*未指定，查詢最佳化工具會更新資料表或索引檢視表的所有統計資料。 這包括使用 CREATE STATISTICS 陳述式所建立的統計資料、開啟 AUTO_CREATE_STATISTICS 時所建立的單一資料行統計資料，以及針對索引所建立的統計資料。  
  
 如需有關 AUTO_CREATE_STATISTICS 的詳細資訊，請參閱[ALTER DATABASE SET 選項 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md). 若要檢視資料表或檢視表所有索引，您可以使用[sp_helpindex](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)。  
  
 FULLSCAN  
 掃描資料表或索引檢視表中的所有資料列，藉以計算統計資料。 FULLSCAN 和 SAMPLE 100 PERCENT 的結果相同。 FULLSCAN 不能搭配 SAMPLE 選項一起使用。  
  
 範例*數目*{%|資料列}  
 指定當查詢最佳化工具更新統計資料時，要在資料表或索引檢視表中使用的近似百分比或資料列數目。 Percent，*數目*可以介於 0 到 100 之間，然後針對資料列，*數目*可以介於 0 到資料列總數。 查詢最佳化工具所取樣的實際百分比或資料列數目可能會與指定的百分比或數目不符。 例如，查詢最佳化工具會掃描資料頁面上的所有資料列。  
  
 在特殊情況下，根據預設取樣的查詢計劃並非最佳化，此時 SAMPLE 便非常有用。 通常，查詢最佳化工具會依預設使用取樣並決定具有統計價值的取樣大小，因此不需要使用 SAMPLE 便可以建立高品質的查詢計劃。 
 
從開始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，取樣的資料來建立統計資料是以平行方式，當您使用相容性層級 130 改善的效能統計資料集合時。 查詢最佳化工具會使用平行範例統計資料，每當資料表大小超過某個臨界值。 
   
 SAMPLE 不能和 FULLSCAN 選項一起使用。 如果 SAMPLE 或 FULLSCAN 都未指定，查詢最佳化工具會依預設使用取樣資料並計算取樣大小。  
  
 我們建議您不要指定 0 PERCENT 或 0 ROWS。 將 PERCENT 或 ROWS 指定為 0 時，雖會更新統計資料物件，但是不會包含統計資料。  
  
 針對大部分的工作負載，完整掃描不必要的且預設取樣足夠。  
不過，某些工作負載的差距資料分佈可能需要增加的取樣大小或甚至完整掃描。  
如需詳細資訊，請參閱[CSS SQL 擴大 Services 部落格](http://blogs.msdn.com/b/psssql/archive/2010/07/09/sampling-can-produce-less-accurate-statistics-if-the-data-is-not-evenly-distributed.aspx)。  
  
 RESAMPLE  
 使用最新的取樣率更新每一項統計資料。  
  
 使用 RESAMPLE 可產生完整資料表掃描。 例如，索引的統計資料會將完整資料表掃描用於其取樣率。 如果未指定任何取樣選項 (SAMPLE、FULLSCAN、RESAMPLE)，查詢最佳化工具依預設會取樣資料並計算取樣大小。  

PERSIST_SAMPLE_PERCENT = {ON |OFF}  
當**ON**，統計資料將會保留未明確指定取樣百分比的後續更新設定的取樣百分比。 當**OFF**，統計資料取樣百分比便會重設預設取樣中未明確指定取樣百分比的後續更新。 預設值是**OFF**。 
 
 > [!NOTE]
 > 若執行 AUTO_UPDATE_STATISTICS 時，它會使用保存的取樣百分比，如果有的話，或如果不使用預設取樣百分比。
 > 重新取樣行為不受此選項。
 
 > [!TIP] 
 > [DBCC SHOW_STATISTICS](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)和[sys.dm_db_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)公開選取統計資料的持續性的範例百分比值。
 
 **適用於**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (開頭為[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1 CU4) 透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)](開頭為[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU1)。  
 
 ON PARTITIONS ({ \<> |\<範圍 >}[，… n])] 會強制重新計算，並然後合併以建立全域統計 ON PARTITIONS 子句中指定之分割區區的分葉層級統計資料。 由於無法將使用不同取樣率建立的分割區區統計資料合併在一起，因此需要 WITH RESAMPLE。  
  
**適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 ALL | COLUMNS | INDEX  
 更新所有現有的統計資料、針對一或多個資料行所建立的統計資料，或是針對索引所建立的統計資料。 如果沒有指定任何選項，UPDATE STATISTICS 陳述式就會更新資料表或索引檢視表的所有統計資料。  
  
 NORECOMPUTE  
 針對指定的統計資料停用自動統計資料更新選項 AUTO_UPDATE_STATISTICS。 如果您指定了這個選項，查詢最佳化工具就會完成這項統計資料更新並停用未來的更新。  
  
 若要重新啟用 AUTO_UPDATE_STATISTICS 選項行為、 重新執行不含 NORECOMPUTE 選項的 UPDATE STATISTICS 或執行**sp_autostats**。  
  
> [!WARNING]  
>  使用這個選項可能會產生次佳查詢計劃。 我們建議您盡量少用這個選項，而且只有合格的系統管理員可以使用。  
  
 如需有關 AUTO_STATISTICS_UPDATE 選項的詳細資訊，請參閱[ALTER DATABASE SET 選項 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 INCREMENTAL = { ON | OFF }  
 當**ON**，根據分割區統計資料，都會重新建立統計資料。 當**OFF**，卸除統計資料樹狀結構和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]重新計算統計資料。 預設值是**OFF**。  
  
 如果不支援依據每個分割區區的統計資料，則會產生錯誤。 針對下列統計資料類型，不支援累加統計資料：  
  
-   建立統計資料時，所使用的索引未與基底資料表進行分割區對齊。  
  
-   在 AlwaysOn 可讀取次要資料庫上建立的統計資料。  
  
-   在唯讀資料庫上建立的統計資料。  
  
-   在篩選的索引上建立的統計資料。  
  
-   在檢視上建立的統計資料。  
  
-   在內部資料表上建立的統計資料。  
  
-   使用空間索引或 XML 索引建立的統計資料。  
  
**適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 \<update_stats_stream_option >[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="remarks"></a>備註  
  
## <a name="when-to-use-update-statistics"></a>使用 UPDATE STATISTICS 的時機  
 如需使用 UPDATE STATISTICS 的時機的詳細資訊，請參閱[統計資料](../../relational-databases/statistics/statistics.md)。  
  
## <a name="updating-all-statistics-with-spupdatestats"></a>使用 sp_updatestats 來更新所有統計資料  
 如需如何針對資料庫中所有使用者定義和內部資料表更新統計資料的詳細資訊，請參閱預存程序 [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)。 例如，下列命令會呼叫 sp_updatestats 來更新資料庫的所有統計資料。  
  
```t-sql  
EXEC sp_updatestats;  
```  
  
## <a name="determining-the-last-statistics-update"></a>判斷上次更新統計資料的時間  
 若要判斷上次更新統計資料的時間，請使用 [STATS_DATE](../../t-sql/functions/stats-date-transact-sql.md) 函數。  
  
## <a name="pdw--sql-data-warehouse"></a>PDW / SQL 資料倉儲  
 PDW 不支援下列語法 / SQL 資料倉儲  
  
```t-sql  
update statistics t1 (a,b);   
```  
  
```t-sql  
update statistics t1 (a) with sample 10 rows;  
```  
  
```t-sql  
update statistics t1 (a) with NORECOMPUTE;  
```  
  
```t-sql  
update statistics t1 (a) with INCREMENTAL=ON;  
```  
  
```t-sql  
update statistics t1 (a) with stats_stream = 0x01;  
```  
  
## <a name="permissions"></a>Permissions  
 需要資料表或檢視表的 ALTER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-update-all-statistics-on-a-table"></a>A. 更新資料表的所有統計資料  
 下列範例會更新所有索引的統計資料上`SalesOrderDetail`資料表。  
  
```t-sql  
USE AdventureWorks2012;  
GO  
UPDATE STATISTICS Sales.SalesOrderDetail;  
GO  
```  
  
### <a name="b-update-the-statistics-for-an-index"></a>B. 更新索引的統計資料  
 下列範例會針對 `AK_SalesOrderDetail_rowguid` 資料表的 `SalesOrderDetail` 索引更新統計資料。  
  
```t-sql  
USE AdventureWorks2012;  
GO  
UPDATE STATISTICS Sales.SalesOrderDetail AK_SalesOrderDetail_rowguid;  
GO  
```  
  
### <a name="c-update-statistics-by-using-50-percent-sampling"></a>C. 使用 50% 取樣來更新統計資料  
 下列範例會建立再更新 `Name` 資料表中 `ProductNumber` 和 `Product` 資料行的統計資料。  
  
```t-sql  
USE AdventureWorks2012;  
GO  
CREATE STATISTICS Products  
    ON Production.Product ([Name], ProductNumber)  
    WITH SAMPLE 50 PERCENT  
-- Time passes. The UPDATE STATISTICS statement is then executed.  
UPDATE STATISTICS Production.Product(Products)   
    WITH SAMPLE 50 PERCENT;  
```  
  
### <a name="d-update-statistics-by-using-fullscan-and-norecompute"></a>D. 使用 FULLSCAN 和 NORECOMPUTE 來更新統計資料  
 下列範例會更新 `Products` 資料表中的 `Product` 統計資料、強制執行 `Product` 資料表中所有資料列的完整掃描，並且關閉 `Products` 統計資料的自動統計資料更新。  
  
```t-sql  
USE AdventureWorks2012;  
GO  
UPDATE STATISTICS Production.Product(Products)  
    WITH FULLSCAN, NORECOMPUTE;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-update-statistics-on-a-table"></a>E. 更新資料表的統計資料  
 下列範例會更新`CustomerStats1`上的統計資料`Customer`資料表。  
  
```t-sql  
UPDATE STATISTICS Customer ( CustomerStats1 );  
```  
  
### <a name="f-update-statistics-by-using-a-full-scan"></a>F. 使用完整掃描來更新統計資料  
 下列範例會更新`CustomerStats1`統計資料，根據掃描中的資料列的所有`Customer`資料表。  
  
```t-sql  
UPDATE STATISTICS Customer (CustomerStats1) WITH FULLSCAN;  
```  
  
### <a name="g-update-all-statistics-on-a-table"></a>G. 更新資料表的所有統計資料  
 下列範例會更新所有統計資料上`Customer`資料表。  
  
```t-sql  
UPDATE STATISTICS Customer;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [統計資料](../../relational-databases/statistics/statistics.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_autostats &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)   
 [STATS_DATE &#40;TRANSACT-SQL &#41;](../../t-sql/functions/stats-date-transact-sql.md)  
 [sys.dm_db_stats_properties &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md) [sys.dm_db_stats_histogram &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) 
  



