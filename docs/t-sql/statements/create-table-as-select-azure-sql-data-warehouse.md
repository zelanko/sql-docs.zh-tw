---
title: "建立 TABLE AS SELECT （Azure SQL 資料倉儲） |Microsoft 文件"
ms.custom: 
ms.date: 10/07/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.service: sql-data-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d1e08f88-64ef-4001-8a66-372249df2533
caps.latest.revision: 40
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2f95f9bc6975593f2536848e2bb3a2b346eca538
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-table-as-select-azure-sql-data-warehouse"></a>建立 TABLE AS SELECT （Azure SQL 資料倉儲）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

建立資料表 AS 選取 (CTAS) 是其中一項最重要的 T-SQL 功能。 這是建立新的資料表根據 SELECT 陳述式的輸出完全平行化的作業。 CTAS 是建立一份資料表最簡單且最快的方法。   
 
 例如，使用到的 CTAS:  
  
-   重新建立具有不同的雜湊散發資料行的資料表。
-   當進行複寫時，重新建立資料表。   
-   只是某些資料表中的資料行上建立資料行存放區索引。  
-   查詢或匯入的外部資料。  

> [!NOTE]  
> 因為 CTAS 會增加建立資料表的功能，本主題嘗試不重複的 CREATE TABLE 主題。 相反地，它描述的 CTAS 和 CREATE TABLE 陳述式之間的差異。 建立資料表的詳細資訊，請參閱[CREATE TABLE （Azure SQL 資料倉儲）](https://msdn.microsoft.com/library/mt203953/)陳述式。 
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
<a name="syntax-bk"></a>

## <a name="syntax"></a>語法   

```  
CREATE TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    [ ( column_name [ ,...n ] ) ]  
    WITH ( 
      <distribution_option> -- required
      [ , <table_option> [ ,...n ] ]    
    )  
    AS <select_statement>   
[;]  

<distribution_option> ::=
    { 
        DISTRIBUTION = HASH ( distribution_column_name ) 
      | DISTRIBUTION = ROUND_ROBIN 
      | DISTRIBUTION = REPLICATE
    }   

<table_option> ::= 
    {   
        CLUSTERED COLUMNSTORE INDEX --default for SQL Data Warehouse 
      | HEAP --default for Parallel Data Warehouse   
      | CLUSTERED INDEX ( { index_column_name [ ASC | DESC ] } [ ,...n ] ) --default is ASC 
    }  
    | PARTITION ( partition_column_name RANGE [ LEFT | RIGHT ] --default is LEFT  
        FOR VALUES ( [ boundary_value [,...n] ] ) ) 
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT select_criteria  

```  

<a name="arguments-bk"></a>
  
## <a name="arguments"></a>引數  
如需詳細資訊，請參閱[引數 > 一節](https://msdn.microsoft.com/library/mt203953/#Arguments)在 CREATE TABLE 中。  

<a name="column-options-bk"></a>

### <a name="column-options"></a>資料行選項
`column_name` [ ,...`n` ]   
 不允許資料行名稱[資料行選項](https://msdn.microsoft.com/library/mt203953/#ColumnOptions)在 CREATE TABLE 中所述。  相反地，您可以提供選擇性的新資料表的一個或多個資料行名稱清單。 新的資料表中的資料行，將使用您指定的名稱。 當您指定資料行名稱時，資料行清單中的資料行數目必須符合 select 結果中的資料行數目。 如果您未指定任何資料行名稱，新的目標資料表會在 select 陳述式結果使用的資料行名稱。 
  
 您無法指定任何其他資料行選項，例如資料類型、 定序或 null 屬性。 每個屬性衍生自的結果`SELECT`陳述式。 不過，您可以使用 SELECT 陳述式來變更屬性。 如需範例，請參閱[變更資料行的屬性使用 CTAS](#ctas-change-column-attributes-bk)。   

<a name="table-distribution-options-bk"></a>

### <a name="table-distribution-options"></a>資料表分佈選項

`DISTRIBUTION` = `HASH`( *distribution_column_name* ) |ROUND_ROBIN |複寫      
CTAS 陳述式需要散發選項，而且沒有預設值。 這是不同於建立資料表具有預設值。 

如需詳細資訊，以及了解如何選擇最佳散發資料行，請參閱[資料表分佈選項](https://msdn.microsoft.com/library/mt203953/#TableDistributionOptions)> 一節中建立的資料表。 

<a name="table-partition-options-bk"></a>

### <a name="table-partition-options"></a>資料表資料分割選項
CTAS 陳述式會建立非資料分割的資料表根據預設，即使已分割來源資料表。 若要建立資料分割的資料表與 CTAS 陳述式，您必須指定資料分割選項。 

如需詳細資訊，請參閱[資料表資料分割選項](https://msdn.microsoft.com/library/mt203953/#TablePartitionOptions)> 一節中建立的資料表。

<a name="select-options-bk"></a>

### <a name="select-options"></a>選取的選項
Select 陳述式是 CTAS 與建立資料表之間的基本差異。  

 `WITH`*common_table_expression*  
 指定稱為通用資料表運算式 (CTE) 的暫存具名結果集。 如需詳細資訊，請參閱[common_table_expression &#40; 與TRANSACT-SQL &#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 `SELECT`*select_criteria*  
 新的 SELECT 陳述式的結果資料表中填入。 *select_criteria*是判斷哪些資料来複製到新資料表的 SELECT 陳述式的主體。 SELECT 陳述式的相關資訊，請參閱[SELECT &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-transact-sql.md).  
  
<a name="permissions-bk"></a>  
  
## <a name="permissions"></a>Permissions  
需要 CTAS`SELECT`中所參考的任何物件的權限*select_criteria*。

若要建立資料表的權限，請參閱[權限](https://msdn.microsoft.com/library/mt203953/#Permissions)在 CREATE TABLE 中。 
  
<a name="general-remarks-bk"></a>
  
## <a name="general-remarks"></a>一般備註
如需詳細資訊，請參閱[< 一般備註](https://msdn.microsoft.com/library/mt203953/#GeneralRemarks)在 CREATE TABLE 中。

<a name="limitations-bk"></a>

## <a name="limitations-and-restrictions"></a>限制事項  
Azure SQL 資料倉儲會目前尚不支援自動建立，或自動更新統計資料。  若要從查詢取得最佳效能，請務必執行 CTAS 之後，資料會發生任何大量變更後，所有資料表的所有資料行上建立統計資料。 如需詳細資訊，請參閱 [CREATE STATISTICS (TRANSACT-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)。

[SET ROWCOUNT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-rowcount-transact-sql.md) CTAS 上沒有作用。 若要達成類似的行為，使用[TOP &#40;TRANSACT-SQL &#41;](../../t-sql/queries/top-transact-sql.md).  
 
如需詳細資訊，請參閱[限制事項](https://msdn.microsoft.com/library/mt203953/#LimitationsRestrictions)在 CREATE TABLE 中。

<a name="locking-behavior-bk"></a>
  
## <a name="locking-behavior"></a>鎖定行為  
 如需詳細資訊，請參閱[鎖定行為](https://msdn.microsoft.com/library/mt203953/#LockingBehavior)在 CREATE TABLE 中。
 
<a name="performance-bk"></a>
 
 ## <a name="performance"></a>效能 

若是雜湊散發的資料表，您可以使用 CTAS 選擇不同的散發資料行，以達到更佳的效能，聯結和彙總。 如果選擇不同的散發資料行不您的目標，則必須獲得最佳的 CTAS 效能如果您指定相同的散發資料行，因為這樣可避免重新散發資料列。 

如果您用來建立資料表 CTAS，而且效能並不是因素，您可以指定`ROUND_ROBIN`若要避免上散發資料行所決定。

若要避免在後續查詢中的資料移動，您可以指定`REPLICATE`代價是會增加儲存載入每個計算節點上資料表的完整複本。  


<a name="examples-copy-table-bk"></a>

## <a name="examples-for-copying-a-table"></a>將資料表複製的範例

<a name="ctas-copy-table-bk"></a>

### <a name="a-use-ctas-to-copy-a-table"></a>A. 使用 CTAS 複製資料表 
適用於： Azure SQL 資料倉儲和 Parallel Data Warehouse

其中一個最常見的使用可能`CTAS`，因此您可以變更 DDL 會建立一份資料表。 如果您最初建立做為資料表，例如`ROUND_ROBIN`，而且現在想將它變更為資料表資料行，分散式`CTAS`是如何變更散發資料行。 `CTAS`也可以用來變更資料分割、 索引或資料行的類型。

假設您建立這個資料表使用的預設發佈類型`ROUND_ROBIN`分散式由於沒有散發資料行中指定`CREATE TABLE`。

```sql
CREATE TABLE FactInternetSales
(
    ProductKey int NOT NULL,
    OrderDateKey int NOT NULL,
    DueDateKey int NOT NULL,
    ShipDateKey int NOT NULL,
    CustomerKey int NOT NULL,
    PromotionKey int NOT NULL,
    CurrencyKey int NOT NULL,
    SalesTerritoryKey int NOT NULL,
    SalesOrderNumber nvarchar(20) NOT NULL,
    SalesOrderLineNumber tinyint NOT NULL,
    RevisionNumber tinyint NOT NULL,
    OrderQuantity smallint NOT NULL,
    UnitPrice money NOT NULL,
    ExtendedAmount money NOT NULL,
    UnitPriceDiscountPct float NOT NULL,
    DiscountAmount float NOT NULL,
    ProductStandardCost money NOT NULL,
    TotalProductCost money NOT NULL,
    SalesAmount money NOT NULL,
    TaxAmt money NOT NULL,
    Freight money NOT NULL,
    CarrierTrackingNumber nvarchar(25),
    CustomerPONumber nvarchar(25)
);
```

現在您想要建立這個資料表的新副本具有叢集資料行存放區索引，以便您可以利用叢集資料行存放區資料表的效能。 您也想要發佈此資料表在 ProductKey，因為您會預期這個資料行上的聯結，並想要避免資料移動期間 ProductKey 上聯結。 最後您也想要加入上 OrderDateKey 資料分割，使卸除舊的資料分割，您可以快速地刪除舊的資料。 以下是會將舊資料表複製到新資料表的 CTAS 陳述式。

```sql
CREATE TABLE FactInternetSales_new
WITH
(
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = HASH(ProductKey),
    PARTITION
    (
        OrderDateKey RANGE RIGHT FOR VALUES
        (
        20000101,20010101,20020101,20030101,20040101,20050101,20060101,20070101,20080101,20090101,
        20100101,20110101,20120101,20130101,20140101,20150101,20160101,20170101,20180101,20190101,
        20200101,20210101,20220101,20230101,20240101,20250101,20260101,20270101,20280101,20290101
        )
    )
)
AS SELECT * FROM FactInternetSales;
```

最後您也可以重新命名資料表交換在新的資料表，然後再卸除舊的資料表。

```sql
RENAME OBJECT FactInternetSales TO FactInternetSales_old;
RENAME OBJECT FactInternetSales_new TO FactInternetSales;

DROP TABLE FactInternetSales_old;
```

<a name="examples-column-bk"></a>

## <a name="examples-for-column-options"></a>資料行選項範例

<a name="ctas-change-column-attributes-bk"></a>

### <a name="b-use-ctas-to-change-column-attributes"></a>B. 若要變更的資料行屬性使用 CTAS 
適用於： Azure SQL 資料倉儲和 Parallel Data Warehouse

這個範例會使用 CTAS 變更資料類型、 null 屬性和 DimCustomer2 資料表中的數個資料行的定序。  
  
```  
-- Original table 
CREATE TABLE [dbo].[DimCustomer2] (  
    [CustomerKey] int NOT NULL,  
    [GeographyKey] int NULL,  
    [CustomerAlternateKey] nvarchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL  
)  
WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = HASH([CustomerKey]));  
  
-- CTAS example to change data types, nullability, and column collations  
CREATE TABLE test  
WITH (HEAP, DISTRIBUTION = ROUND_ROBIN)  
AS  
SELECT  
    CustomerKey AS CustomerKeyNoChange,  
    CustomerKey*1 AS CustomerKeyChangeNullable,  
    CAST(CustomerKey AS DECIMAL(10,2)) AS CustomerKeyChangeDataTypeNullable,  
    ISNULL(CAST(CustomerKey AS DECIMAL(10,2)),0) AS CustomerKeyChangeDataTypeNotNullable,  
    GeographyKey AS GeographyKeyNoChange,  
    ISNULL(GeographyKey,0) AS GeographyKeyChangeNotNullable,  
    CustomerAlternateKey AS CustomerAlternateKeyNoChange,  
    CASE WHEN CustomerAlternateKey = CustomerAlternateKey 
        THEN CustomerAlternateKey END AS CustomerAlternateKeyNullable,  
    CustomerAlternateKey COLLATE Latin1_General_CS_AS_KS_WS AS CustomerAlternateKeyChangeCollation  
FROM [dbo].[DimCustomer2]  
  
-- Resulting table 
CREATE TABLE [dbo].[test] (
    [CustomerKeyNoChange] int NOT NULL, 
    [CustomerKeyChangeNullable] int NULL, 
    [CustomerKeyChangeDataTypeNullable] decimal(10, 2) NULL, 
    [CustomerKeyChangeDataTypeNotNullable] decimal(10, 2) NOT NULL, 
    [GeographyKeyNoChange] int NULL, 
    [GeographyKeyChangeNotNullable] int NOT NULL, 
    [CustomerAlternateKeyNoChange] nvarchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL, 
    [CustomerAlternateKeyNullable] nvarchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NULL, 
    [CustomerAlternateKeyChangeCollation] nvarchar(15) COLLATE Latin1_General_CS_AS_KS_WS NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN);
```
 
最後一個步驟中，您可以使用[重新命名 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/rename-transact-sql.md)切換的資料表名稱。 這可讓 DimCustomer2 是新的資料表。

```
RENAME OBJECT DimCustomer2 TO DimCustomer2_old;
RENAME OBJECT test TO DimCustomer2;

DROP TABLE DimCustomer2_old;
```

<a name="examples-table-distribution-bk"></a>

## <a name="examples-for-table-distribution"></a>資料表發佈的範例

<a name="ctas-change-distribution-method-bk"></a>

### <a name="c-use-ctas-to-change-the-distribution-method-for-a-table"></a>C. 若要變更資料表的散發方法使用 CTAS
適用於： Azure SQL 資料倉儲和 Parallel Data Warehouse

這個簡單的範例示範如何變更資料表的散發方法。 若要顯示如何執行這項操作的機制，它對循環配置資源的雜湊散發的資料表，然後再變更循環配置資源資料表回分散式的雜湊。 最後的資料表符合原始資料表。 

在大部分情況下您不需要變更為循環配置資源資料表的雜湊散發的資料表。 通常，您可能需要變更分散式雜湊表的循環配置資源資料表。 例如，您可能一開始載入循環配置資源為新的資料表，並稍後將移至分散式雜湊資料表，以取得更佳的聯結效能。

這個範例會使用 AdventureWorksDW 範例資料庫。 若要載入 SQL 資料倉儲的版本，請參閱[範例資料載入 SQL 資料倉儲](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-load-sample-databases/)
 
```
-- DimSalesTerritory is hash-distributed.
-- Copy it to a round-robin table.
CREATE TABLE [dbo].[myTable]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = ROUND_ROBIN  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]; 

-- Switch table names

RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[myTable] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];

```  
接下來，將它變更回分散式雜湊表。

```
-- You just made DimSalesTerritory a round-robin table.
-- Change it back to the original hash-distributed table. 
CREATE TABLE [dbo].[myTable]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = HASH(SalesTerritoryKey) 
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]; 

-- Switch table names

RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[myTable] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```
 
<a name="ctas-change-to-replicated-bk"></a>

### <a name="d-use-ctas-to-convert-a-table-to-a-replicated-table"></a>D. 將資料表轉換成複寫的資料表使用 CTAS  
適用於： Azure SQL 資料倉儲和 Parallel Data Warehouse 

此範例適用於將循環配置資源或雜湊散發資料表轉換為複寫的資料表。 此特定範例會變更發佈類型進一步的上一個方法。  因為 DimSalesTerritory 維度，而且可能較小的資料表，您可以選擇重新建立資料表，當進行複寫時若要加入其他資料表時，避免資料移動。 

```
-- DimSalesTerritory is hash-distributed.
-- Copy it to a replicated table.
CREATE TABLE [dbo].[myTable]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE 
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]; 

-- Switch table names

RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[myTable] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```
 
### <a name="e-use-ctas-to-create-a-table-with-fewer-columns"></a>E. 若要建立具有較少的資料行的資料表使用 CTAS
適用於： Azure SQL 資料倉儲和 Parallel Data Warehouse 

下列範例會建立名為的循環配置資源分散式的資料表`myTable (c, ln)`。 新的資料表中僅有兩個資料行。 它會使用資料行別名 SELECT 陳述式中的資料行名稱。  
  
```  
CREATE TABLE myTable  
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = ROUND_ROBIN  
  )  
AS SELECT CustomerKey AS c, LastName AS ln  
    FROM dimCustomer;  
  
```  

<a name="examples-query-hints-bk"></a>

## <a name="examples-for-query-hints"></a>如需查詢提示的範例

<a name="ctas-query-hint-bk"></a>

### <a name="f-use-a-query-hint-with-create-table-as-select-ctas"></a>F. 使用查詢提示使用 CREATE TABLE AS 選取 (CTAS)  
適用於： Azure SQL 資料倉儲和 Parallel Data Warehouse
  
此查詢會顯示與 CTAS 陳述式中使用查詢的聯結提示的基本語法。 提交查詢之後，[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]產生查詢計畫，針對每個個別的發佈時，適用於雜湊聯結策略。 如需有關雜湊聯結查詢提示的詳細資訊，請參閱[OPTION 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/option-clause-transact-sql.md).  
  
```  
CREATE TABLE dbo.FactInternetSalesNew  
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = ROUND_ROBIN   
  )  
AS SELECT T1.* FROM dbo.FactInternetSales T1 JOIN dbo.DimCustomer T2  
ON ( T1.CustomerKey = T2.CustomerKey )  
OPTION ( HASH JOIN );  
```  

<a name="examples-external-tables"></a>

## <a name="examples-for-external-tables"></a>外部資料表的範例

<a name="ctas-azure-blob-storage-bk"></a>

### <a name="g-use-ctas-to-import-data-from-azure-blob-storage"></a>G. 使用 CTAS 從 Azure Blob 儲存體匯入資料  
適用於： Azure SQL 資料倉儲和 Parallel Data Warehouse  

若要匯入資料，從外部資料表，只要使用 CREATE TABLE AS SELECT 從外部資料表中選取。 從外部資料表至選取的資料語法[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]從一般資料表中選取資料的語法相同。  
  
 下列範例會定義外部資料表的 Azure blob 儲存體帳戶中的資料。 然後使用 CREATE TABLE AS SELECT 從外部資料表選取。 這從 Azure blob 儲存體文字分隔檔案匯入資料，並將資料儲存至新[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]資料表。  
  
```  
--Use your own processes to create the text-delimited files on Azure blob storage.  
--Create the external table called ClickStream.  
CREATE EXTERNAL TABLE ClickStreamExt (   
    url varchar(50),  
    event_date date,  
    user_IP varchar(50)  
)  
WITH (  
    LOCATION='/logs/clickstream/2015/',  
    DATA_SOURCE = MyAzureStorage,  
    FILE_FORMAT = TextFileFormat)  
;  
  
--Use CREATE TABLE AS SELECT to import the Azure blob storage data into a new   
--SQL Data Warehouse table called ClickStreamData  
CREATE TABLE ClickStreamData   
WITH  
  (  
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = HASH (user_IP)  
  )  
AS SELECT * FROM ClickStreamExt  
;  
```  

<a name="ctas-import-Hadoop-bk"></a>
  
### <a name="h-use-ctas-to-import-hadoop-data-from-an-external-table"></a>H. 使用 CTAS Hadoop 資料匯入從外部資料表  
適用於：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
若要匯入資料，從外部資料表，只要使用 CREATE TABLE AS SELECT 從外部資料表中選取。 從外部資料表至選取的資料語法[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]從一般資料表中選取資料的語法相同。  
  
 下列範例會定義在 Hadoop 叢集上的外部資料表。 然後使用 CREATE TABLE AS SELECT 從外部資料表選取。 這會將資料從 Hadoop 文字分隔檔案匯入，並將資料儲存至新[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]資料表。  
  
```  
-- Create the external table called ClickStream.  
CREATE EXTERNAL TABLE ClickStreamExt (   
    url varchar(50),  
    event_date date,  
    user_IP varchar(50)  
)  
WITH (  
    LOCATION = 'hdfs://MyHadoop:5000/tpch1GB/employee.tbl',  
    FORMAT_OPTIONS ( FIELD_TERMINATOR = '|')  
)  
;  
  
-- Use your own processes to create the Hadoop text-delimited files 
-- on the Hadoop Cluster.  
  
-- Use CREATE TABLE AS SELECT to import the Hadoop data into a new 
-- table called ClickStreamPDW  
CREATE TABLE ClickStreamPDW   
WITH  
  (  
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = HASH (user_IP)  
  )  
AS SELECT * FROM ClickStreamExt  
;   
```  
 
<a name="examples-workarounds-bk"></a>
 
## <a name="examples-using-ctas-to-replace-sql-server-code"></a>使用 CTAS 取代 SQL Server 程式碼範例

若要暫時解決一些不支援的功能使用 CTAS。 除了可以在資料倉儲上執行您的程式碼，重新撰寫現有程式碼以使用 CTAS 通常效能改善。 這是設計的它完全平行化的結果。 

> [!NOTE]
> 嘗試將"CTAS 第一次 」。 如果您認為您可以解決問題，使用`CTAS`然後，通常是最佳方法，即使您要撰寫更多資料，因此。
>

<a name="ctas-replace-select-into-bk"></a>

### <a name="i-use-ctas-instead-of-selectinto"></a>I. 使用 CTAS 來取代 SELECT...到  
適用於： Azure SQL 資料倉儲和 Parallel Data Warehouse

SQL Server 程式碼通常會使用 SELECT...INTO 來擴展資料表的 SELECT 陳述式的結果。 這是範例的 SQL Server SELECT...陳述式。

```sql
SELECT *
INTO    #tmp_fct
FROM    [dbo].[FactInternetSales]
```

在 SQL 資料倉儲和平行處理資料倉儲中不支援此語法。 這個範例示範如何重新寫入先前 SELECT...為 CTAS 陳述式的陳述式。 您可以選擇任何 CTAS 語法所述的分佈選項。 這個範例會使用 ROUND_ROBIN 發佈方法。

```sql
CREATE TABLE #tmp_fct
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
;
```

<a name="ctas-replace-implicit-joins-bk"></a>

### <a name="j-use-ctas-and-implicit-joins-to-replace-ansi-joins-in-the-from-clause-of-an-update-statement"></a>J. 使用 CTAS 和隱含聯結來取代在 ANSI 聯結`FROM`子句`UPDATE`陳述式  
適用於： Azure SQL 資料倉儲和 Parallel Data Warehouse  

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

```sql
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

ANSI 因為不支援 SQL 資料倉儲中的聯結`FROM`子句`UPDATE`陳述式中，無法使用透過此 SQL Server 程式碼，而不需要稍微變更它。

您可以使用多種`CTAS`和隱含聯結來取代此程式碼：

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

<a name="ctas-replace-ansi-joins-bk"></a>

### <a name="k-use-ctas-to-specify-which-data-to-keep-instead-of-using-ansi-joins-in-the-from-clause-of-a-delete-statement"></a>K. 若要指定哪些資料要保留而不是使用 ANSI 聯結 DELETE 陳述式的 FROM 子句中使用 CTAS  
適用於： Azure SQL 資料倉儲和 Parallel Data Warehouse  

有時候刪除資料的最佳方法是使用`CTAS`。 而不只刪除資料中，選取您想要保留的資料。 這尤其適合`DELETE`使用的 ansi 聯結語法，因為 SQL 資料倉儲不支援 ANSI 聯結中的陳述式`FROM`子句`DELETE`陳述式。

已轉換的 DELETE 陳述式的範例是如下所示：

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish to keep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        TO DimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert TO DimProduct;
```

<a name="ctas-simplify-merge-bk"></a>

### <a name="l-use-ctas-to-simplify-merge-statements"></a>L. 使用 CTAS 簡化 merge 陳述式  
適用於： Azure SQL 資料倉儲和 Parallel Data Warehouse  

Merge 陳述式可以取代，至少在部分中，使用`CTAS`。 您可以合併`INSERT`和`UPDATE`為單一陳述式。 關閉第二個陳述式中要刪除的記錄。

舉例來說，`UPSERT`如下所示：

```sql
CREATE TABLE dbo.[DimProduct_upsert]
WITH
(   DISTRIBUTION = HASH([ProductKey])
,   CLUSTERED INDEX ([ProductKey])
)
AS
-- New rows and new versions of rows
SELECT      s.[ProductKey]
,           s.[EnglishProductName]
,           s.[Color]
FROM      dbo.[stg_DimProduct] AS s
UNION ALL  
-- Keep rows that are not being touched
SELECT      p.[ProductKey]
,           p.[EnglishProductName]
,           p.[Color]
FROM      dbo.[DimProduct] AS p
WHERE NOT EXISTS
(   SELECT  *
    FROM    [dbo].[stg_DimProduct] s
    WHERE   s.[ProductKey] = p.[ProductKey]
)
;

RENAME OBJECT dbo.[DimProduct]          TO [DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  TO [DimProduct];

```

<a name="ctas-data-type-and-nullability-bk"></a>

### <a name="m-explicitly-state-data-type-and-nullability-of-output"></a>M. 明確資料類型和 null 屬性的輸出  
適用於： Azure SQL 資料倉儲和 Parallel Data Warehouse  

在 SQL Server 程式碼移轉到 SQL 資料倉儲時，您可能會發現您橫跨這種類型的程式碼撰寫模式：

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE result
(result DECIMAL(7,2) NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN)

INSERT INTO result
SELECT @d*@f
;
```

Instinctively 您可能會認為您應該將這段程式碼移轉至 CTAS，而系統會將正確。 不過，沒有隱藏的問題。

下列程式碼不會產生相同的結果：

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455
;

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT @d*@f as result
;
```

請注意，資料行"result"向前執行運算式的資料類型和 null 屬性值。 這可能會導致難以察覺的變異數在值中如果您不小心。

請嘗試下列做為範例：

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

儲存結果的值不相同。 當結果資料行中保存的值用在其他運算式中錯誤變得更為顯著。

![CREATE TABLE AS SELECT 結果](../../t-sql/statements/media/create-table-as-select-results.png)

這是特別重要的資料移轉。 即使第二個查詢是更精確的說是有問題。 資料是不同相較於來源系統而，會導致問題的移轉中的完整性。 這是罕見情況下，其中 「 錯誤 」 的答案都是實際適合 ！

我們會了解這兩個結果之間差異的原因是向隱含類型轉換。 第一個範例中的資料表定義資料行定義。 插入資料列時，就會發生隱含類型轉換。 在第二個範例中沒有任何隱含類型轉換為此運算式會定義資料行資料類型。 另請注意，第二個範例中的資料行已定義為 Null 的資料行而在第一個範例中還沒有。 資料表中的第一個範例資料行 null 屬性建立時已明確定義。 在第二個範例，它已保留為運算式，以及依預設這會導致 NULL 定義。  

若要解決這些問題則必須明確設定的型別轉換和中的 null 屬性`SELECT`部分`CTAS`陳述式。 您無法建立資料表組件中設定這些屬性。

下列範例會示範如何修正程式碼：

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

請注意下列事項：
- CAST 或 CONVERT 可能已經使用
- ISNULL 用來強制不 COALESCE 的 null 屬性
- ISNULL 是最外層的函式
- ISNULL 的第二個部分是常數，也就是 0

> [!NOTE]
> 如要正確地設定它的 null 屬性是很重要的使用`ISNULL`而非`COALESCE`。 `COALESCE`不具決定性的函式，因此運算式的結果將會永遠是 Null。 `ISNULL`有不同。 它是具決定性。 因此時的第二部分`ISNULL`函式是常數或常值，則產生的值將會是 NOT NULL。

這個提示不只適合用於確保您的計算的完整性。 它也是很重要的資料表資料分割切換。 假設您有此資料表定義為您的事實：

```sql
CREATE TABLE [dbo].[Sales]
(
    [date]      INT     NOT NULL
,   [product]   INT     NOT NULL
,   [store]     INT     NOT NULL
,   [quantity]  INT     NOT NULL
,   [price]     MONEY   NOT NULL
,   [amount]    MONEY   NOT NULL
)
WITH
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

不過，[值] 欄位是計算的運算式，它不是來源資料的一部分。

若要建立資料分割資料集可能會想要執行這項操作：

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   [quantity]*[price]  AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create')
;
```

會執行最適合的查詢。 問題在於當您嘗試執行資料分割切換。 資料表定義不相符。 必須修改才能符合 CTAS 的資料表定義。

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   ISNULL(CAST([quantity]*[price] AS MONEY),0) AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create');
```

您可以因此看到類型一致性和維護上 CTAS 的 null 屬性屬性是很好的工程最佳作法。 它有助於維護您的計算的完整性，並且也可確保資料分割切換，就可能。
 
## <a name="see-also"></a>另請參閱  
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [建立外部 TABLE AS SELECT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [建立資料表 &#40;Azure SQL 資料倉儲 &#41;](../../t-sql/statements/create-table-azure-sql-data-warehouse.md) [卸除資料表 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [卸除的外部資料表 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-external-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER EXTERNAL TABLE &#40;TRANSACT-SQL &#41;](http://msdn.microsoft.com/library/4ae1b23c-67f6-41d0-b614-7a8de914d145)  
  
  



