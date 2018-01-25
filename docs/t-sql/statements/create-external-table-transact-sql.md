---
title: "建立外部資料表 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 11/27/2017
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
- CREATE_EXTERNAL_TABLE
- CREATE EXTERNAL TABLE
- PolyBase, T-SQL
dev_langs: TSQL
helpviewer_keywords:
- External
- External, table create
- PolyBase, external table
ms.assetid: 6a6fd8fe-73f5-4639-9908-2279031abdec
caps.latest.revision: "30"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 97381b5381491b98c81a6863b3cfcdc6a340c79e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="create-external-table-transact-sql"></a>建立外部資料表 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  建立 PolyBase 外部資料表所參考的 Hadoop 叢集或 Azure blob 儲存體中儲存的資料。 也可以用來建立外部資料表的[彈性資料庫查詢](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/)。  
  
 使用外部資料表：  
  
-   查詢使用的 Hadoop 或 Azure blob 儲存體資料[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式。  
  
-   匯入並儲存資料至 Hadoop 或 Azure blob 儲存體您[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。  
  
-   建立具有彈性的資料庫使用的外部資料表  
     查詢。  
     
- 匯入，並從 Azure 資料湖存放區的資料儲存到 Azure SQL 資料倉儲
  
 另請參閱[建立外部資料來源 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)和[卸除的外部資料表 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-external-table-transact-sql.md).  
  
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
    | REJECT_TYPE = value | percentage  
    | REJECT_VALUE = reject_value  
    | REJECT_SAMPLE_VALUE = reject_sample_value  
  
}  
```  
  
## <a name="arguments"></a>引數  
 *database_name* 。 [schema_name]。 |schema_name。 ] *table_name*  
 一至三段要建立資料表的部分名稱。 外部資料表，資料表中繼資料會儲存在 SQL 以及檔案和或 Hadoop 或 Azure blob 儲存體中所參考的資料夾的相關基本統計資料。 移動或儲存在任何實際資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 \<column_definition > [，... *n*  ] CREATE EXTERNAL TABLE 可讓一或多個資料行定義。 CREATE EXTERNAL TABLE 和 CREATE TABLE 使用相同的語法來定義資料行。 這個例外狀況，您無法使用預設條件約束，外部資料表。 如需資料行定義和其資料類型的完整詳細資料，請參閱[CREATE TABLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-table-transact-sql.md)和[Azure SQL Database 上的建立資料表](http://msdn.microsoft.com/library/d53c529a-1d5f-417f-9a77-64ccc6eddca1)。  
  
 資料行定義，包括資料類型和資料行數目必須符合的外部檔案中的資料。 如果不相符，查詢的實際資料時，將會拒絕檔案的資料列。  
  
 參考外部資料來源中的檔案外部資料表的資料行和類型定義必須對應到外部檔案的確切的結構描述。 定義參考的資料儲存在 Hadoop/登錄區中的資料類型，當使用 SQL 和 Hive 資料類型之間的下列對應，並從中選取時，轉換成 SQL 資料類型的型別。 除非指定，否則類型會包含登錄區的所有版本。

> [!NOTE]  
>  SQL Server 不支援 Hive_無限大_任何轉換作業中的資料值。 PolyBase 會因資料類型轉換錯誤。


|SQL 資料類型|.NET 資料類型|登錄區的資料類型|Hadoop/Java 資料類型|註解|  
|-------------------|--------------------|--------------------|----------------------------|--------------|  
|tinyint|Byte|tinyint|ByteWritable|只有不帶正負號數字。|  
|smallint|Int16|smallint|ShortWritable||  
|int|Int32|int|IntWritable||  
|bigint|Int64|bigint|LongWritable||  
|bit|布林|boolean|BooleanWritable||  
|float|Double|double|DoubleWritable||  
|real|Single|float|FloatWritable||  
|money|Decimal|double|DoubleWritable||  
|smallmoney|Decimal|double|DoubleWritable||  
|NCHAR|字串<br /><br /> Char]|string|text||  
|nvarchar|字串<br /><br /> Char]|string|Text||  
|char|字串<br /><br /> Char]|string|Text||  
|varchar|字串<br /><br /> Char]|string|Text||  
|BINARY|Byte[]|BINARY|BytesWritable|適用於 Hive 0.8 和更新版本。|  
|varbinary|Byte[]|BINARY|BytesWritable|適用於 Hive 0.8 和更新版本。|  
|date|DateTime|timestamp|TimestampWritable||  
|smalldatetime|DateTime|timestamp|TimestampWritable||  
|datetime2|DateTime|timestamp|TimestampWritable||  
|datetime|DateTime|timestamp|TimestampWritable||  
|time|TimeSpan|timestamp|TimestampWritable||  
|decimal|Decimal|decimal|BigDecimalWritable|適用於 Hive0.11 和更新版本。|  
  
 LOCATION =  '*folder_or_filepath*'  
 指定 Hadoop 或 Azure blob 儲存體中的資料夾或檔案路徑和檔案名稱的實際資料。 位置開始在根資料夾中。根資料夾是在外部資料來源中指定的資料位置。  
  
 如果您指定的資料夾位置，從外部資料表選取的 PolyBase 查詢會擷取檔案資料夾和其所有子資料夾。 就像 Hadoop，PolyBase 不會傳回隱藏的資料夾。 它也不會傳回的檔案的檔案名稱開頭為底線 (_) 或句號 （.）。  
  
 在此範例中，如果位置 ='webdata /'，PolyBase 查詢會從 mydata.txt 和 mydata2.txt 傳回資料列。  它不會傳回 mydata3.txt，因為它是隱藏資料夾的子資料夾。 它不會傳回 _hidden.txt，因為它是隱藏的檔案。  
  
 ![外部資料表的遞迴資料](../../t-sql/statements/media/aps-polybase-folder-traversal.png "外部資料表的遞迴資料")  
  
 若要變更預設位置和只能讀取在根資料夾中，設定屬性\<polybase.recursive.traversal > 為 'false' core-site.xml 組態檔中。 這個檔案位於`<SqlBinRoot>\Polybase\Hadoop\Conf with SqlBinRoot the bin root of SQl Server`。 例如， `C:\\Program Files\\Microsoft SQL Server\\MSSQL13.XD14\\MSSQL\\Binn`。  
  
 DATA_SOURCE = *external_data_source_name*  
 指定包含外部資料的位置的外部資料來源的名稱。 這個位置是 Hadoop 或 Azure blob 儲存體。 若要建立外部資料來源，使用[CREATE EXTERNAL DATA SOURCE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 FILE_FORMAT = *external_file_format_name*  
 指定儲存外部資料的檔案類型和壓縮方法之外部檔案格式物件的名稱。 若要建立外部檔案格式，請使用[CREATE EXTERNAL FILE FORMAT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
 拒絕選項  
 您可以指定拒絕參數，以決定如何處理 PolyBase*中途*擷取外部資料來源會加以記錄。 資料錄會被視為 '中途' 是否其實際的資料類型或資料行數目不相符的外部資料表的資料行定義。  
  
 當您不要指定或變更拒絕的值時，PolyBase 會使用預設值。 拒絕參數資訊儲存為其他的中繼資料，當您使用 CREATE EXTERNAL TABLE 陳述式建立外部資料表。   當未來的 SELECT 陳述式或選取 INTO SELECT 陳述式會從外部資料表選取資料時，PolyBase 將使用拒絕選項，來判斷實際的查詢失敗之前可以被拒絕的資料列的百分比的數字。 。 查詢會傳回 （部分） 的結果，直到超過拒絕臨界值;就會失敗並出現適當的錯誤訊息。  
  
 REJECT_TYPE =**值**| 百分比  
 將釐清是否 REJECT_VALUE 選項指定為常值或百分比。  
  
 value  
 REJECT_VALUE 是常值，而不是百分比。 PolyBase 查詢會失敗時被拒絕的資料列數超出*reject_value*。  
  
 例如，如果 REJECT_VALUE = 5 且 REJECT_TYPE = value、 PolyBase 之後已拒絕 5 個資料列，選取查詢將會失敗。  
  
 百分比  
 REJECT_VALUE 是百分比，而不是常值的值。 PolyBase 查詢將會失敗時*百分比*失敗的資料列超過*reject_value*。 失敗的資料列百分比的計算間隔。  
  
 REJECT_VALUE = *reject_value*  
 指定的值或在查詢失敗前，可能會拒絕的資料列百分比。  
  
 為 REJECT_TYPE = value， *reject_value*必須是介於 0 到 2147483647 之間的整數。  
  
 REJECT_TYPE = 百分比， *reject_value*必須是介於 0 到 100 之間的浮點數。  
  
 REJECT_SAMPLE_VALUE = *reject_sample_value*  
 這個屬性是必要的當您指定 REJECT_TYPE = 百分比。 它會判斷要嘗試擷取 PolyBase 重新計算已拒絕的資料列百分比之前的資料列數目。  
  
 *Reject_sample_value*參數必須是介於 0 到 2147483647 之間的整數。  
  
 例如，如果 REJECT_SAMPLE_VALUE = 1000，已嘗試從外部資料檔案匯入 1000 個資料列之後，PolyBase 會計算失敗資料列的百分比。 如果失敗的資料列的百分比小於*reject_value*，PolyBase 會嘗試擷取另一個 1000 個資料列。 它會繼續嘗試匯入每個額外的 1000 個資料列重新計算失敗資料列的百分比。  
  
> [!NOTE]  
>  PolyBase 計算失敗資料列的百分比間隔，因為可能會超出實際的失敗資料列百分比*reject_value*。  
  
 範例：  
  
 這個範例會示範如何與彼此互動的三個拒絕選項。 例如，如果 REJECT_TYPE = 百分比，REJECT_VALUE = 30，而且 REJECT_SAMPLE_VALUE = 100，發生下列狀況：  
  
-   PolyBase 會嘗試擷取的前 100 個資料列。25 失敗和 75 成功。  
  
-   失敗的資料列百分比的計算方式為 25%小於拒絕值為 30%。 因此，PolyBase 將繼續從外部資料來源擷取資料。  
  
-   PolyBase 會嘗試載入 100 的資料列。這次 25 成功和失敗 75。  
  
-   重新計算失敗資料列的百分比為 50%。 失敗的資料列的百分比已超過 30%拒絕的值。  
  
-   PolyBase 查詢而拒絕的 50%的資料列失敗之後嘗試傳回的前 200 個資料列。 請注意，PolyBase 查詢之前已傳回相符的資料列會偵測已超過拒絕臨界值。  
  
 分區化的外部資料表選項  
 指定外部資料來源 （非 SQL Server 資料來源） 和發佈方法的[彈性資料庫查詢](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/)。  
  
 DATA_SOURCE  
 資料儲存在 Hadoop 檔案系統、 Azure blob 儲存體，例如外部資料來源或[分區對應管理員](https://azure.microsoft.com/documentation/articles/sql-database-elastic-scale-shard-map-management/)。  
  
 SCHEMA_NAME  
 SCHEMA_NAME 子句提供了可對應至不同的結構描述上的遠端資料庫中資料表的外部資料表定義。 您可以使用這個來區分存在於本機和遠端資料庫的結構描述之間。  
  
 OBJECT_NAME  
 OBJECT_NAME 子句提供了可對應至使用不同的名稱，遠端資料庫上資料表的外部資料表定義。 使用此釐清存在於本機和遠端資料庫的物件名稱。  
  
 發佈  
 選擇性。 這只是只有需要類型對包含 SHARD_MAP_MANAGER 的資料庫。 這會控制資料表會被視為分區化資料表或複寫的資料表。 與**SHARDED** (*資料行名稱*) 資料表，不同資料表的資料不會重疊。 **複寫**指定資料表上每個分區有相同的資料。 **ROUND_ROBIN**指出應用程式專屬方法會用來將資料散發。  
  
## <a name="permissions"></a>Permissions  
 需要這些使用者權限：  
  
-   **CREATE TABLE**  
  
-   **改變任何結構描述**  
  
-   **改變任何外部資料來源**  
  
-   **改變任何外部檔案格式**  

-   **控制資料庫**
  
 請注意，建立外部資料來源的登入必須擁有讀取和寫入外部資料來源，Hadoop 或 Azure blob 儲存體中的權限。  


 > [!IMPORTANT]  

>  ALTER ANY EXTERNAL DATA SOURCE 權限授與任何主體建立和修改任何外部資料來源物件的能力，因此，它也會授與存取在資料庫上的所有資料庫範圍認證的能力。 此權限必須被視為具有高度權限，因此必須只授與信任的主體在系統中。

## <a name="error-handling"></a>錯誤處理  
 在執行 CREATE EXTERNAL TABLE 陳述式，PolyBase 會嘗試連接到外部資料來源。 如果連接嘗試失敗，陳述式會失敗，並將不會建立外部資料表。 可能需要一分鐘以上，命令才會失敗，因為 PolyBase 查詢的最終失敗之前連線重試。  
  
## <a name="general-remarks"></a>一般備註  
 在臨機操作查詢案例中，也就是選取從外部資料表，PolyBase 會儲存在暫存資料表的外部資料來源擷取的資料列。 查詢完成後，PolyBase 移除，並刪除暫存資料表。 沒有永久的資料會儲存在 SQL 資料表。  
  
 相反地，在匯入案例中，也就是選取到從外部資料表，PolyBase 會儲存為永久 SQL 資料表中的資料從外部資料來源擷取的資料列。 Polybase 擷取外部資料時，會在查詢執行期間建立新的資料表。  
  
 PolyBase 可以將某些查詢計算推送到 Hadoop，用來改善查詢效能。 這稱為述詞下推。 若要啟用此功能，指定 Hadoop 資源管理員位置選項，在[CREATE EXTERNAL DATA SOURCE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 您可以建立多個參考相同或不同的外部資料來源的外部資料表。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 在 CTP2 中，匯出功能不支援，也就是永久將 SQL 資料儲存到外部資料來源。 這項功能可在 CTP3 中。  
  
 外部資料表的資料位於設備關閉，因為它不是所控制的 PolyBase，和可以變更或移除在任何時間由外部處理序。 因此，對外部資料表的查詢結果不保證為確定性函數。 每次針對外部資料表執行時，相同的查詢可以傳回不同的結果。 同樣地，如果外部資料已移除或重新配置可能會失敗的查詢。  
  
 您可以建立每一個參考不同的外部資料來源的多個外部資料表。 不過，如果您同時針對不同的 Hadoop 資料來源執行查詢，然後每個 Hadoop 來源必須使用相同的 'hadoop connectivity' 伺服器組態設定。 例如，您無法同時執行的查詢針對 Cloudera Hadoop 叢集和 Hortonworks Hadoop 叢集自這些使用不同的組態設定。 在組態設定和支援的組合，請參閱[PolyBase 連線組態 &#40;TRANSACT-SQL &#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
  
 只有這些資料定義語言 (DDL) 陳述式可用於外部資料表：  
  
-   CREATE TABLE 和 DROP TABLE  
  
-   建立統計資料和卸除統計資料  
注意： 建立和 Azure SQL Database 不支援外部資料表的卸除統計資料。 
  
-   建立檢視和卸除檢視  
  
 建構並不支援的作業：  
  
-   外部資料表資料行的預設條件約束  
  
-   資料操作語言 (DML) 作業的 delete、 insert 和 update  
  
 查詢的限制：  
  
 PolyBase 可以取用每個資料夾的 33 k 檔案最的多 32 個並行 PolyBase 查詢的執行時。 這個最大的數字會包含每個 HDFS 資料夾中檔案和子資料夾。 如果並行程度小於 32，使用者可以執行 PolyBase 查詢，針對包含多個 33 k 檔案的 HDFS 中的資料夾。 我們建議您保持簡短的外部檔案路徑，並使用每個 HDFS 資料夾不能超過 30 個 k 檔案。 太多檔案參考時，可能是 Java 虛擬機器 (JVM) 的記憶體不足例外狀況。  

表格寬度限制： PolyBase，SQL Server 2016 中的資料列寬度上限為 32 KB 依據資料表定義的單一有效的資料列大小上限。 如果資料行的結構描述的總和大於 32 KB，PolyBase 將無法查詢資料。 

在 SQL 資料倉儲中，已發出這項限制為 1 MB。


## <a name="locking"></a>鎖定  
 共用 SCHEMARESOLUTION 物件上的鎖定。  
  
## <a name="security"></a>Security  
 外部資料表的資料檔案會儲存在 Hadoop 或 Azure blob 儲存體。 這些資料檔案建立和管理您自己的處理程序。 您必須負責管理外部資料的安全性。  
  
## <a name="examples"></a>範例  
  
### <a name="a-create-an-external-table-with-data-in-text-delimited-format"></a>A. 以資料建立外部資料表，以文字分隔的格式。  
 這個範例會示範建立已格式化文字分隔檔案中資料的外部資料表所需的所有步驟。 它會定義外部資料來源*mydatasource*和外部檔案格式*myfileformat*。 這些資料庫層級物件接著會在 CREATE EXTERNAL TABLE 陳述式參考。 如需詳細資訊，請參閱[CREATE EXTERNAL DATA SOURCE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)和[建立外部檔案格式 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
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
  
### <a name="b-create-an-external-table-with-data-in-rcfile-format"></a>B. RCFile 格式中的資料建立的外部資料表。  
 這個範例會示範建立具有資料會格式化為 RCFiles 的外部資料表所需的所有步驟。 它會定義外部資料來源*mydatasource_rc*和外部檔案格式*myfileformat_rc*。 這些資料庫層級物件接著會在 CREATE EXTERNAL TABLE 陳述式參考。 如需詳細資訊，請參閱[CREATE EXTERNAL DATA SOURCE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)和[建立外部檔案格式 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource_rc  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat_rc  
WITH (  
    FORMAT = RCFILE,  
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
  
### <a name="c-create-an-external-table-with-data-in-orc-format"></a>C. 建立外部資料表 ORC 格式中的資料。  
 這個範例會示範建立外部資料表具有為 ORC 檔案格式的資料所需的所有步驟。 它會定義外部資料來源 mydatasource_orc 和外部檔案格式 myfileformat_orc。 這些資料庫層級物件接著會在 CREATE EXTERNAL TABLE 陳述式參考。 如需詳細資訊，請參閱[CREATE EXTERNAL DATA SOURCE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)和[建立外部檔案格式 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
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
  
### <a name="d-querying-hadoop-data"></a>D. 查詢 Hadoop 資料：  
 點選流是連接到 Hadoop 叢集上的 employee.tbl 分隔的文字檔案的外部資料表。 下列查詢會尋找如同針對標準資料表的查詢。 不過，此查詢會從 Hadoop 擷取資料，然後再計算 restuls。  
  
```  
SELECT TOP 10 (url) FROM ClickStream WHERE user_ip = 'xxx.xxx.xxx.xxx'  
;  
```  
  
### <a name="e-join-hadoop-data-with-sql-data"></a>E. 加入 Hadoop 資料： SQL 資料  
 此查詢看起來就像標準的聯結兩個 SQL 資料表。 差別在於 PolyBase Hadoop 從擷取的點選流資料，然後將它聯結至 UrlDescription 資料表。 有一個資料表是外部資料表，另一個是標準的 SQL 資料表。  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="f-import-data-from-hadoop-into-a-sql-table"></a>F. 將資料從 Hadoop 匯入至 SQL 資料表  
 這個範例會建立新的 SQL 資料表 ms_user 永久儲存在標準的 SQL 資料表之間聯結的結果*使用者*和外部資料表*點選流*。  
  
```  
SELECT DISTINCT user.FirstName, user.LastName  
INTO ms_user  
FROM user INNER JOIN (  
    SELECT * FROM ClickStream WHERE cs.url = 'www.microsoft.com'  
    ) AS ms_user  
ON user.user_ip = ms.user_ip  
;  
  
```  
  
### <a name="g-create-an-external-table-for-a-sharded-data-source"></a>G. 建立分區化的資料來源的外部資料表  
 此範例中重新對應至外部資料表使用 SCHEMA_NAME 和 OBJECT_NAME 子句遠端 DMV。  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="h-importing-data-from-adls-into-azure-includessdwincludesssdw-mdmd"></a>H. 從 ADLS 匯入資料至 Azure[!INCLUDE[ssDW](../../includes/ssdw-md.md)]  
 
  
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
WITH ( FORMATTYPE = DELIMITEDTEXT 
     , FORMATOPTIONS ( FIELDTERMINATOR = '|' 
                     , STRINGDELIMITER = '' 
                     , DATEFORMAT = 'yyyy-MM-dd HH:mm:ss.fff' 
                     , USETYPE_DEFAULT = FALSE 
                     ) 
    )


CREATE EXTERNAL TABLE [dbo].[DimProductexternal] 
( [ProductKey] [int] NOT NULL, 
  [ProductLabel] nvarchar NULL, 
  [ProductName] nvarchar NULL ) 
WITH ( LOCATION='/DimProduct/' , 
       DATA_SOURCE = AzureDataLakeStore , 
       FILE_FORMAT = TextFileFormat , 
       REJECT_TYPE = VALUE ,
       REJECT_VALUE = 0 ) ;


CREATE TABLE [dbo].[DimProduct] 
WITH (DISTRIBUTION = HASH([ProductKey] ) ) 
AS SELECT * FROM 
[dbo].[DimProduct_external] ; 
     
```  
  
### <a name="i-join-external-tables"></a>I. 加入外部資料表  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="j-join-hdfs-data-with-pdw-data"></a>J. 加入 HDFS 資料與 PDW 資料  
  
```  
SELECT cs.user_ip FROM ClickStream cs  
JOIN User u ON cs.user_ip = u.user_ip  
WHERE cs.url = 'www.microsoft.com'  
;  
  
```  
  
### <a name="k-import-row-data-from-hdfs-into-a-distributed-pdw-table"></a>K. 從 HDFS 到分散式 PDW 資料表匯入資料列資料  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = HASH (url) )  
AS SELECT url, event_date, user_ip FROM ClickStream  
;  
```  
  
### <a name="l-import-row-data-from-hdfs-into-a-replicated-pdw-table"></a>L. 從 HDFS 到複寫的 PDW 資料表匯入資料列資料  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = REPLICATE )  
AS SELECT url, event_date, user_ip   
FROM ClickStream  
;  
```  
  
## <a name="see-also"></a>另請參閱  
 [常見的中繼資料的查詢範例 (SQL Server PDW)](http://msdn.microsoft.com/en-us/733fc99b-b9f6-4a29-b085-a1bd4f09f2ed)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [建立外部 TABLE AS SELECT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [建立 TABLE AS SELECT &#40;Azure SQL 資料倉儲 &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
  
  



