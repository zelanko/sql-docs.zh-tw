---
title: CREATE EXTERNAL TABLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 6/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE_EXTERNAL_TABLE
- CREATE EXTERNAL TABLE
- PolyBase, T-SQL
dev_langs:
- TSQL
helpviewer_keywords:
- External
- External, table create
- PolyBase, external table
ms.assetid: 6a6fd8fe-73f5-4639-9908-2279031abdec
caps.latest.revision: 30
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f305bf60f682ee9da175191b785b73d5e363c7c5
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/04/2018
ms.locfileid: "37789599"
---
# <a name="create-external-table-transact-sql"></a>CREATE EXTERNAL TABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  建立針對 PolyBase 的外部資料表，或是彈性資料庫查詢。 語法會視案例而擁有顯著的差異。 針對 PolyBase 建立的外部資料表無法用於彈性資料庫查詢。  同樣地，針對彈性資料庫查詢建立的外部資料表也無法用於 PolyBase。 
  
> [!NOTE]  
>  只有在 SQL Server 2016 (或更新版本)、Azure SQL 資料倉儲，以及平行處理資料倉儲上才支援 PolyBase。 只有在 Azure SQL Database v12 或更新版本上才支援彈性資料庫查詢。  


- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用外部資料表來存取儲存在 Hadoop 叢集或 Azure Blob 儲存體中的資料，一個能參考儲存在 Hadoop 叢集或 Azure Blob 儲存體中資料的 PolyBase 外部資料表。 也可以用來針對[彈性資料庫查詢](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/)建立外部資料表。  
  
 使用外部資料表來：  
  
-   搭配 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢 Hadoop 或 Azure Blob 儲存體資料。  
  
-   從 Hadoop 或 Azure Blob 儲存體將資料匯入並儲存到您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中。  
  
-   建立要搭配彈性資料庫查詢使用的外部資料表  
     。  
     
- 從 Azure Data Lake Store 將資料匯入並儲存至 Azure SQL 資料倉儲
  
 另請參閱 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) 和 [DROP EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-table-transact-sql.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  

```  
-- Syntax for SQL Server 
  
-- Create a new external table  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH (   
        LOCATION = 'folder_or_filepath',  
        DATA_SOURCE = external_data_source_name,  
        FILE_FORMAT = external_file_format_name  
        [ , <reject_options> [ ,...n ] ]  
    )  
[;]  
  
<reject_options> ::=  
{  
    | REJECT_TYPE = value | percentage  
    | REJECT_VALUE = reject_value  
    | REJECT_SAMPLE_VALUE = reject_sample_value  
  
}  
  
-- Create a table for use with Elastic Database query  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH ( <sharded_external_table_options> )  
[;]  
  
<sharded_external_table_options> ::=  
        DATA_SOURCE = external_data_source_name,   
        SCHEMA_NAME = N'nonescaped_schema_name',  
        OBJECT_NAME = N'nonescaped_object_name',  
        [DISTRIBUTION  = SHARDED(sharding_column_name) | REPLICATED | ROUND_ROBIN]]  
    )  
[;]  
```  

```  
-- Syntax for Azure SQL Database
  
-- Create a table for use with Elastic Database query  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH ( <sharded_external_table_options> )  
[;]  
  
<sharded_external_table_options> ::=  
        DATA_SOURCE = external_data_source_name,   
        SCHEMA_NAME = N'nonescaped_schema_name',  
        OBJECT_NAME = N'nonescaped_object_name',  
        [DISTRIBUTION  = SHARDED(sharding_column_name) | REPLICATED | ROUND_ROBIN]]  
    )  
[;]  
```  


```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Create a new external table in SQL Server PDW  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH (   
        LOCATION = 'hdfs_folder_or_filepath',  
        DATA_SOURCE = external_data_source_name,  
        FILE_FORMAT = external_file_format_name  
        [ , <reject_options> [ ,...n ] ]  
    )  
[;]  
  
<reject_options> ::=  
{  
    | REJECT_TYPE = value | percentage,  
    | REJECT_VALUE = reject_value,  
    | REJECT_SAMPLE_VALUE = reject_sample_value,
    | REJECTED_ROW_LOCATION = '\REJECT_Directory'
  
}  
```  
  
## <a name="arguments"></a>引數  
 *database_name* . [ schema_name ] . | schema_name. ] *table_name*  
 要建立之資料表名稱的第一到第三部分。 針對外部資料表，只有資料表中繼資料會儲存在 SQL 中，而有關所參考檔案或資料夾的基本統計資料則會儲存在 Hadoop 或 Azure Blob 儲存體中。 實際上不會有任何資料會移至或儲存於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中。  
  
 \<column_definition> [ ,...*n* ] CREATE EXTERNAL TABLE 允許一或多個資料行定義。 CREATE EXTERNAL TABLE 和 CREATE TABLE 在定義資料行上都使用相同的語法。 唯一的例外是無法在外部資料表上使用 DEFAULT CONSTRAINT。 如需資料行定義及其資料類型的完整詳細資料，請參閱 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) 和 [Azure SQL Database 上的 CREATE TABLE](http://msdn.microsoft.com/library/d53c529a-1d5f-417f-9a77-64ccc6eddca1)。  
  
 資料行定義 (包括資料類型和資料行數目) 必須符合外部檔案中的資料。 若有不相符的情形，系統在查詢實際資料時將會拒絕檔案資料列。  
  
 針對會參考位於外部資料來源中之檔案的外部資料表，資料行和類型定義必須對應至外部檔案中的確切結構描述。 定義會參考儲存於 Hadoop/Hive 中資料的資料類型時，請在 SQL 和 Hive 資料類型之間使用下列對應，並在從類型進行選取時將該類型轉換成 SQL 資料類型。 除非另行指定，否則這些類型都包含 Hive 的所有版本。

> [!NOTE]  
>  SQL Server 在任何轉換中皆不支援 Hive 的 _infinity_ 資料值。 PolyBase 將會搭配資料類型轉換錯誤而失敗。


|SQL 資料類型|.NET 資料類型|Hive 資料類型|Hadoop/Java 資料類型|註解|  
|-------------------|--------------------|--------------------|----------------------------|--------------|  
|TINYINT|Byte|TINYINT|ByteWritable|僅適用於不帶正負號的數字。|  
|SMALLINT|Int16|SMALLINT|ShortWritable||  
|ssNoversion|Int32|ssNoversion|IntWritable||  
|BIGINT|Int64|BIGINT|LongWritable||  
|bit|布林|boolean|BooleanWritable||  
|FLOAT|Double|double|DoubleWritable||  
|REAL|Single|FLOAT|FloatWritable||  
|money|Decimal|double|DoubleWritable||  
|SMALLMONEY|Decimal|double|DoubleWritable||  
|NCHAR|String<br /><br /> Char[]|string|text||  
|NVARCHAR|String<br /><br /> Char[]|string|文字||  
|char|String<br /><br /> Char[]|string|文字||  
|varchar|String<br /><br /> Char[]|string|文字||  
|BINARY|Byte[]|BINARY|BytesWritable|適用於 Hive 0.8 及更新版本。|  
|varbinary|Byte[]|BINARY|BytesWritable|適用於 Hive 0.8 及更新版本。|  
|日期|DateTime|TIMESTAMP|TimestampWritable||  
|smalldatetime|DateTime|TIMESTAMP|TimestampWritable||  
|datetime2|DateTime|TIMESTAMP|TimestampWritable||  
|DATETIME|DateTime|TIMESTAMP|TimestampWritable||  
|time|TimeSpan|TIMESTAMP|TimestampWritable||  
|Decimal|Decimal|Decimal|BigDecimalWritable|適用於 Hive 0.11 及更新版本。|  
  
 LOCATION =  '*folder_or_filepath*'  
 指定位於 Hadoop 或 Azure Blob 儲存體中之實際資料的資料夾或檔案路徑，以及檔案名稱。 位置會從根資料夾開始；根資料夾是在外部資料來源中指定的資料位置。  


在 SQL Server 中，CREATE EXTERNAL TABLE 陳述式會建立尚未存在的路徑和資料夾。 您接著可以使用 INSERT INTO 將資料從本機 SQL Server 資料表匯出至外部資料來源。 如需詳細資訊，請參閱 [Polybase 查詢](/sql/relational-databases/polybase/polybase-queries)。 

在 SQL 資料倉儲和 Analytics Platform System 中，[CREATE EXTERNAL TABLE AS SELECT](create-external-table-as-select-transact-sql.md) 陳述式會建立不存在的路徑和資料夾。 在這兩個產品中，CREATE EXTERNAL TABLE 不會建立路徑和資料夾。

  
 若您將 LOCATION 指定為資料夾，會從外部資料表中選取的 PolyBase 查詢，將會從該資料夾及其所有子資料夾中擷取檔案。 PolyBase 和 Hadoop 相同，並不會傳回隱藏的資料夾。 它也不會傳回檔案名稱是以底線 (_) 或句號 (.) 開始的檔案。  
  
 在此範例中，若 LOCATION='/webdata/'，PolyBase 查詢將會傳回來自 mydata.txt 和 mydata2.txt 的資料列。  它不會傳回 mydata3.txt，因為它是隱藏資料夾的子資料夾。 它不會傳回 _hidden.txt，因為它是隱藏的資料夾。  
  
 ![外部資料表的遞迴資料](../../t-sql/statements/media/aps-polybase-folder-traversal.png "外部資料表的遞迴資料")  
  
 若要變更預設設定並僅從根資料夾讀取，請在 core-site.xml 設定檔中將 \<polybase.recursive.traversal> 屬性設為 'false'。 此檔案位於 `<SqlBinRoot>\Polybase\Hadoop\Conf with SqlBinRoot the bin root of SQl Server`。 例如， `C:\\Program Files\\Microsoft SQL Server\\MSSQL13.XD14\\MSSQL\\Binn`。  
  
 DATA_SOURCE = *external_data_source_name*  
 指定包含外部資料位置之外部資料來源的名稱。 此位置可為 Hadoop 或 Azure Blob 儲存體。 若要建立外部資料來源，請使用 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)。  
  
 FILE_FORMAT = *external_file_format_name*  
 指定儲存外部資料檔案類型和壓縮方法之外部檔案格式物件的名稱。 若要建立外部檔案格式，請使用 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)。  
  
 拒絕選項  
 您可以指定能決定 PolyBase 如何處理其從外部資料來源所擷取之*已修改*記錄的拒絕參數。 若資料記錄的實際資料類型或資料行數目與外部資料表的資料行定義不相符，該資料記錄就會被系統視為「已修改」。  
  
 當您不指定會變更拒絕值時，PolyBase 就會使用預設值。 拒絕參數的相關資訊會在您搭配 CREATE EXTERNAL TABLE 陳述式建立外部資料表時，以額外中繼資料的形式儲存。   當未來有 SELECT 陳述式或 SELECT INTO SELECT 陳述式從外部資料表中選取資料時，PolyBase 將會使用拒絕選項來判斷在實際的查詢失敗之前，可以拒絕的資料列數目或百分比。 執行個體時提供 SQL Server 登入。 查詢將會傳回 (部分的) 結果，直到超過拒絕閾值為止；接著它便會搭配適當的錯誤訊息而失敗。  
  
 REJECT_TYPE = **value** | 百分比  
 指明是要將 REJECT_VALUE 選項指定為常值還是百分比。  
  
 value  
 REJECT_VALUE 是常值，而不是百分比。 PolyBase 查詢會在被拒絕資料列的數目超過 *reject_value* 時失敗。  
  
 例如，若 REJECT_VALUE = 5 且 REJECT_TYPE = value，PolyBase SELECT 查詢將會在系統拒絕 5 個資料列之後失敗。  
  
 percentage  
 REJECT_VALUE 是百分比，而不是常值。 PolyBase 查詢會在被拒絕資料列的*百分比*超過 *reject_value* 時失敗。 失敗的資料列百分比會每隔一段時間就計算一次。  
  
 REJECT_VALUE = *reject_value*  
 指定在查詢失敗之前可以拒絕的資料列數目或百分比。  
  
 針對 REJECT_TYPE = value，*reject_value* 必須為介於 0 和 2,147,483,647 的整數。  
  
 針對 REJECT_TYPE = percentage，*reject_value* 必須為介於 0 和 100 的浮點數。  
  
 REJECT_SAMPLE_VALUE = *reject_sample_value*  
 當您指定 REJECT_TYPE = percentage 時，這是必要的屬性。 它會決定在 PolyBase 重新計算被拒絕資料列的百分比之前，應嘗試擷取的資料列數目。  
  
 *reject_sample_value* 參數必須是介於 0 和 2,147,483,647 的整數。  
  
 例如，如果 REJECT_SAMPLE_VALUE = 1000，PolyBase 將會在已嘗試從外部資料檔案匯入 1000 個資料列之後，計算失敗的資料列百分比。 如果失敗的資料列百分比小於 *reject_value*，PolyBase 就會嘗試擷取另外 1000 個資料列。 它會在嘗試匯入每個額外的 1000 個資料列之後，持續重新計算失敗的資料列百分比。  
  
> [!NOTE]  
>  由於 PolyBase 會不時計算失敗的資料列百分比，因此實際的失敗資料列百分比可能超出 *reject_value*。  
  

範例  
  
 此範例說明三個 REJECT 選項彼此如何互動。 例如，如果 REJECT_TYPE = percentage、REJECT_VALUE = 30 且 REJECT_SAMPLE_VALUE = 100，就可能發生下列案例：  
  
-   PolyBase 會嘗試擷取前 100 個資料列；其中有 25 個失敗，75 個成功。  
  
-   失敗資料列的百分比會計算為 25%，低於拒絕值 30%。 因此，PolyBase 將會繼續從外部資料來源擷取資料。  
  
-   PolyBase 會嘗試載入接下來 100 個資料列；這次有 25 個成功，75 個失敗。  
  
-   失敗資料列的百分比在重新計算後為 50%。 失敗資料列的百分比已超出 30% 的拒絕值。  
  
-   PolyBase 查詢在嘗試傳回前 200 個資料列後，會因被拒絕的資料列達 50% 而失敗。 請注意，相符的資料列會在 PolyBase 查詢偵測到超出拒絕閾值之前傳回。  
  
REJECTED_ROW_LOCATION = *Directory Location*
  
  指定外部資料來源中，已拒絕資料列和相應錯誤檔案應寫入的目錄。
若指定的路徑不存在，PolyBase 會為您建立一個目錄。 會建立名稱為 “_rejectedrows” 的子目錄。“_” 字元可確保該目錄從其他資料處理逸出，除非已明確在位置參數中指名。 在此目錄中，會有一個根據載入提交時間建立的資料夾，格式為 YearMonthDay -HourMinuteSecond (例如 20180330-173205)。 在此資料中寫入了兩種類型的檔案，分別是 _reason 檔案與資料檔案。 

原因檔案與資料檔案均具有與 CTAS 陳述式相關的 queryID。 因為資料與原因檔案在不同的檔案中，所以對應的檔案會具有相符的尾碼。 
  
 分區外部資料表選項  
 針對[彈性資料庫查詢](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/)指定外部資料來源 (非 SQL Server 資料來源) 及發佈方法。  
  
 DATA_SOURCE  
 外部資料來源，例如儲存在 Hadoop 檔案系統、Azure Blob 儲存體，或是[分區對應管理員](https://azure.microsoft.com/documentation/articles/sql-database-elastic-scale-shard-map-management/)中的資料。  
  
 SCHEMA_NAME  
 SCHEMA_NAME 子句能讓您將外部資料表定義對應至位於遠端資料庫上之不同結構描述中的資料表。 使用此子句來區分同時存在於本機和遠端資料庫上的結構描述。  
  
 OBJECT_NAME  
 OBJECT_NAME 子句能讓您將外部資料表定義對應至位於遠端資料庫上具有不同名稱的資料表。 使用此子句來區分同時存在於本機和遠端資料庫上的物件名稱。  
  
 DISTRIBUTION  
 選擇性。 只有類型為 SHARD_MAP_MANAGER 的資料庫才需要此項目。 這能控制資料表是否會被視為分區資料表或複寫資料表。 針對 **SHARDED** (*資料行名稱*) 資料表，來自不同資料表的資料不會彼此重疊。 **REPLICATED** 指定資料表在每個分區上都有相同的資料。 **ROUND_ROBIN** 指出系統會使用應用程式特定的方法來散發資料。  
  
## <a name="permissions"></a>Permissions  
 需要下列使用者權限：  
  
-   **CREATE TABLE**  
  
-   **ALTER ANY SCHEMA**  
  
-   **ALTER ANY EXTERNAL DATA SOURCE**  
  
-   **ALTER ANY EXTERNAL FILE FORMAT**  

-   **CONTROL DATABASE**
  
 請注意，建立外部資料來源的登入，必須具有讀取和寫入位於 Hadoop 或 Azure Blob 儲存體上之外部資料來源的權限。  


 > [!IMPORTANT]  

>  ALTER ANY EXTERNAL DATA SOURCE 權限可讓任何主體都能夠建立及修改任何外部資料來源物件，因此也會讓主體能夠存取資料庫上的所有資料庫範圍認證。 必須將此權限視為具高度權限，因此必須僅授與系統中受信任的主體。

## <a name="error-handling"></a>錯誤處理  
 執行 CREATE EXTERNAL TABLE 陳述式的同時，PolyBase 會嘗試連線至外部資料來源。 如果連線的嘗試失敗，陳述式就會失敗，且不會建立外部資料表。 由於 PolyBase 在查詢失敗之前會多次嘗試連線，因此可能需要一分鐘或更久的時間，命令才會失敗。  
  
## <a name="general-remarks"></a>一般備註  
 在臨機操作的案例中 (也就是 SELECT FROM EXTERNAL TABLE)，PolyBase 會將擷取自外部資料來源的資料列儲存在暫存資料表中。 在查詢完成之後，PolyBase 便會移除並刪除該暫存資料表。 SQL 資料表中不會永久存放資料。  
  
 相反地，在匯入案例中 (也就是 SELECT INTO FROM EXTERNAL TABLE)，PolyBase 會將擷取自外部資料來源的資料列，以永久資料的形式儲存在 SQL 資料表中。 新的資料表會在查詢執行期間，當 PolyBase 擷取外部資料時建立。  
  
 PolyBase 可以將部分的查詢計算推送至 Hadoop 以改善查詢效能。 這稱為述詞下推。 若要啟用此功能，請指定 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) 中所述的 Hadoop 資源管理員位置選項。  
  
 您可以建立多個參考相同或不同外部資料來源的外部資料表。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 CTP2 中尚不支援匯出功能，也就是將 SQL 資料永久儲存至外部資料來源的功能。 此功能將會在 CTP3 中提供。  
  
 由於外部資料表的資料位於設備之外，因此它並不受 PolyBase 控制，並可以隨時由外部程序變更或移除。 因此，針對外部資料表的查詢結果並不保證具有確定性。 相同的查詢在每次針對外部資料表執行時，都有可能傳回不同的結果。 同樣地，在外部資料被移除或移動的情況下，查詢也有可能會失敗。  
  
 您可以建立多個參考不同外部資料來源的外部資料表。 不過，如果您同時針對不同的 Hadoop 資料來源執行查詢，則每個 Hadoop 來源都必須使用相同的「Hadoop 連線能力」伺服器組態設定。 例如，您不能同時針對 Cloudera Hadoop 叢集和 Hortonworks Hadoop 叢集執行查詢，因為這些叢集是使用不同的組態設定。 如需組態設定和支援的組合，請參閱 [PolyBase 連線組態 &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。  
  
 外部資料表上僅允許使用下列資料定義語言 (DDL) 陳述式：  
  
-   CREATE TABLE 和 DROP TABLE  
  
-   CREATE STATISTICS 和 DROP STATISTICS  
注意：Azure SQL Database 不支援在外部資料表上使用 CREATE 和 DROP STATISTICS。 
  
-   CREATE VIEW 和 DROP VIEW  
  
 不支援的建構和作業：  
  
-   外部資料表資料行上的 DEFAULT 限制式  
  
-   刪除、插入及更新的資料操作語言 (DML) 作業  
  
 查詢限制：  
  
 執行 32 個並行的 PolyBase 查詢時，PolyBase 每個資料夾可取用的檔案數目上限為 33000 個檔案。 這個上限數同時包含了每個 HDFS 資料夾中的檔案和子資料夾。 如果並行程度小於 32，使用者就可以針對 HDFS 中內含超過 33000 個檔案的資料夾執行 PolyBase 查詢。 我們建議您使用簡短的外部檔案路徑，且所使用的每個 HDFS 資料夾檔案數目不要超過 30000 個檔案。 參考太多檔案時，可能會發生 Java 虛擬機器 (JVM) 記憶體不足的例外狀況。  

資料表寬度限制：SQL Server 2016 中的 PolyBase 具有 32KB 的資料列寬度限制，這是以根據資料表定義之單一有效資料列的大小上限為基礎。 若資料行結構描述的總和超過 32KB，PolyBase 將無法查詢資料。 

在 SQL 資料倉儲中，此限制已提升至 1MB。


## <a name="locking"></a>鎖定  
 SCHEMARESOLUTION 物件上的共用鎖定。  
  
## <a name="security"></a>Security  
 外部資料表的資料檔案會儲存在 Hadoop 或 Azure Blob 儲存體中。 這些資料檔案是由您自己的處理程序所建立及管理。 因此您應負責管理外部資料的安全性。  
  
## <a name="examples"></a>範例  
  
### <a name="a-create-an-external-table-with-data-in-text-delimited-format"></a>A. 建立具有文字分隔格式之資料的外部資料表。  
 此範例會示範建立將資料儲存為文字分隔檔案之外部資料表的所有步驟。 它會定義外部資料來源 *mydatasource*，以及外部檔案格式 *myfileformat*。 系統接著會在 CREATE EXTERNAL TABLE 陳述式中參考這些資料庫層級的物件。 如需詳細資訊，請參閱 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) 和 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)。  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat  
WITH (  
    FORMAT_TYPE = DELIMITEDTEXT,   
    FORMAT_OPTIONS (FIELD_TERMINATOR ='|')  
);  
  
CREATE EXTERNAL TABLE ClickStream (   
    url varchar(50),  
    event_date date,  
    user_IP varchar(50)  
)  
WITH (  
        LOCATION='/webdata/employee.tbl',  
        DATA_SOURCE = mydatasource,  
        FILE_FORMAT = myfileformat  
    )  
;  
  
```  
  
### <a name="b-create-an-external-table-with-data-in-rcfile-format"></a>B. 建立具有 RCFile 格式之資料的外部資料表。  
 此範例會示範建立將資料格式化為 RCFile 之外部資料表的所有步驟。 它會定義外部資料來源 *mydatasource_rc*，以及外部檔案格式 *myfileformat_rc*。 系統接著會在 CREATE EXTERNAL TABLE 陳述式中參考這些資料庫層級的物件。 如需詳細資訊，請參閱 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) 和 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)。  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource_rc  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat_rc  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'  
)  
;  
  
CREATE EXTERNAL TABLE ClickStream_rc (   
    url varchar(50),  
    event_date date,  
    user_ip varchar(50)  
)  
WITH (  
        LOCATION='/webdata/employee_rc.tbl',  
        DATA_SOURCE = mydatasource_rc,  
        FILE_FORMAT = myfileformat_rc  
    )  
;  
  
```  
  
### <a name="c-create-an-external-table-with-data-in-orc-format"></a>C. 建立具有 ORC 格式之資料的外部資料表。  
 此範例會示範建立將資料格式化為 ORC 檔案之外部資料表的所有步驟。 它會定義外部資料來源 mydatasource_orc，以及外部檔案格式 myfileformat_orc。 系統接著會在 CREATE EXTERNAL TABLE 陳述式中參考這些資料庫層級的物件。 如需詳細資訊，請參閱 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) 和 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)。  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource_orc  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat_orc  
WITH (  
    FORMAT = ORC,  
    COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
)  
;  
  
CREATE EXTERNAL TABLE ClickStream_orc (   
    url varchar(50),  
    event_date date,  
    user_ip varchar(50)  
)  
WITH (  
        LOCATION='/webdata/',  
        DATA_SOURCE = mydatasource_orc,  
        FILE_FORMAT = myfileformat_orc  
    )  
;  
  
```  
  
### <a name="d-querying-hadoop-data"></a>D. 查詢 Hadoop 資料  
 Clickstream 為能夠連線至 Hadoop 叢集上 employee.tbl 分隔符號文字檔案的外部資料表。 下列查詢看起來像是針對標準資料表的查詢。 不過，此查詢會從 Hadoop 擷取資料，然後計算結果。  
  
```  
SELECT TOP 10 (url) FROM ClickStream WHERE user_ip = 'xxx.xxx.xxx.xxx'  
;  
```  
  
### <a name="e-join-hadoop-data-with-sql-data"></a>E. 將 Hadoop 資料與 SQL 資料聯結  
 此查詢看起來像是針對兩個 SQL 資料表的標準 JOIN 查詢。 差異在於，PolyBase 會從 Hadoop 擷取 Clickstream 資料，然後將它聯結至 UrlDescription 資料表。 其中一個資料表是外部資料表，另一個則是標準 SQL 資料表。  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="f-import-data-from-hadoop-into-a-sql-table"></a>F. 將資料從 Hadoop 匯入至 SQL 資料表  
 此範例會建立新的 SQL 資料表 ms_user，它能永久儲存標準 SQL 資料表 *user* 及外部資料表 *ClickStream* 之間的聯結結果。  
  
```  
SELECT DISTINCT user.FirstName, user.LastName  
INTO ms_user  
FROM user INNER JOIN (  
    SELECT * FROM ClickStream WHERE cs.url = 'www.microsoft.com'  
    ) AS ms_user  
ON user.user_ip = ms.user_ip  
;  
  
```  
  
### <a name="g-create-an-external-table-for-a-sharded-data-source"></a>G. 針對分區資料來源建立外部資料表  
 此範例會使用 SCHEMA_NAME 和 OBJECT_NAME 子句將遠端 DMV 重新對應至外部資料表。  
  
```  
CREATE EXTERNAL TABLE [dbo].[all_dm_exec_requests]([session_id] smallint NOT NULL,  
  [request_id] int NOT NULL,  
  [start_time] datetime NOT NULL,   
  [status] nvarchar(30) NOT NULL,  
  [command] nvarchar(32) NOT NULL,  
  [sql_handle] varbinary(64),  
  [statement_start_offset] int,  
  [statement_end_offset] int,  
  [cpu_time] int NOT NULL)  
WITH  
(  
  DATA_SOURCE = MyExtSrc,  
  SCHEMA_NAME = 'sys',  
  OBJECT_NAME = 'dm_exec_requests',  
  DISTRIBUTION=ROUND_ROBIN  
);   
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="h-importing-data-from-adls-into-azure-includessdwincludesssdw-mdmd"></a>H. 將資料從 ADLS 匯入至 Azure [!INCLUDE[ssDW](../../includes/ssdw-md.md)]  
 
  
```  

-- These values come from your Azure Active Directory Application used to authenticate to ADLS
CREATE DATABASE SCOPED CREDENTIAL ADLUser 
WITH IDENTITY = '<clientID>@\<OAuth2.0TokenEndPoint>',
SECRET = '<KEY>' ;


CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (TYPE = HADOOP,
      LOCATION = 'adl://pbasetr.azuredatalakestore.net'
)



CREATE EXTERNAL FILE FORMAT TextFileFormat 
WITH
(
    FORMAT_TYPE = DELIMITEDTEXT 
    , FORMAT_OPTIONS ( FIELDTERMINATOR = '|' 
                     , STRINGDELIMITER = '' 
                     , DATEFORMAT = 'yyyy-MM-dd HH:mm:ss.fff' 
                     , USETYPE_DEFAULT = FALSE 
                     ) 
)


CREATE EXTERNAL TABLE [dbo].[DimProductexternal] 
( [ProductKey] [int] NOT NULL, 
  [ProductLabel] nvarchar NULL, 
  [ProductName] nvarchar NULL ) 
WITH
(
    LOCATION='/DimProduct/' , 
    DATA_SOURCE = AzureDataLakeStore , 
    FILE_FORMAT = TextFileFormat , 
    REJECT_TYPE = VALUE ,
    REJECT_VALUE = 0
) ;


CREATE TABLE [dbo].[DimProduct] 
WITH (DISTRIBUTION = HASH([ProductKey] ) ) 
AS SELECT * FROM 
[dbo].[DimProduct_external] ; 
     
```  
  
### <a name="i-join-external-tables"></a>I. 聯結外部資料表  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="j-join-hdfs-data-with-pdw-data"></a>J. 聯結 HDFS 資料與 PDW 資料  
  
```  
SELECT cs.user_ip FROM ClickStream cs  
JOIN User u ON cs.user_ip = u.user_ip  
WHERE cs.url = 'www.microsoft.com'  
;  
  
```  
  
### <a name="k-import-row-data-from-hdfs-into-a-distributed-pdw-table"></a>K. 將來自 HDFS 的資料列資料匯入至分散式 PDW 資料表  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = HASH (url) )  
AS SELECT url, event_date, user_ip FROM ClickStream  
;  
```  
  
### <a name="l-import-row-data-from-hdfs-into-a-replicated-pdw-table"></a>L. 將來自 HDFS 的資料列資料匯入至複寫的 PDW 資料表  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = REPLICATE )  
AS SELECT url, event_date, user_ip   
FROM ClickStream  
;  
```  
  
## <a name="see-also"></a>另請參閱  
 [常見的中繼資料查詢範例 (SQL Server PDW)](http://msdn.microsoft.com/en-us/733fc99b-b9f6-4a29-b085-a1bd4f09f2ed)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [CREATE TABLE AS SELECT &#40;Azure SQL 資料倉儲&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
  
  



