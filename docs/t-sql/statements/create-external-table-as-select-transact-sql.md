---
title: CREATE EXTERNAL TABLE AS SELECT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- CREATE EXTERNAL TABLE AS SELECT
- CREATE_EXTERNAL_TABLE_AS_SELECT
- CREATE EXTERNAL TABLE AS SELECT_TSQL
helpviewer_keywords:
- External, table
- PolyBase, external table
- External, table create as select
- PolyBase, create table as select
ms.assetid: 32dfe254-6df7-4437-bfd6-ca7d37557b0a
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: e727b05f4b57e00694c2bf12aa60a972838a9af2
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2018
---
# <a name="create-external-table-as-select-transact-sql"></a>CREATE EXTERNAL TABLE AS SELECT (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  建立外部資料表，然後將 [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT 陳述式的結果以平行方式匯出至 Hadoop 或「Azure 儲存體 Blob」。  
  
 使用 CREATE EXTERNAL TABLE AS SELECT (CETAS) 陳述式來：  
  
-   將資料褲資料表匯出至 Hadoop 或 Azure Blob 儲存體。  
  
-   從 Hadoop 或 Azure Blob 儲存體匯入資料，然後儲存在資料庫中。  
  
-   從 Hadoop 或 Azure Blob 儲存體查詢資料、將該資料與資料庫關聯式資料表聯結，然後將結果寫回至 Hadoop 或 Azure Blob 儲存體。  
  
-   從 Hadoop 或 Azure Blob 儲存體查詢資料、使用資料庫的快速處理功能來轉換該資料，然後將其寫回至 Hadoop 或 Azure Blob 儲存體。  
  
 如需詳細資訊，請參閱 [開始使用 PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE EXTERNAL TABLE [ [database_name  . [ schema_name ] . ] | schema_name . ] table_name   
    WITH (   
        LOCATION = 'hdfs_folder',  
        DATA_SOURCE = external_data_source_name,  
        FILE_FORMAT = external_file_format_name  
        [ , <reject_options> [ ,...n ] ]  
    )  
    AS <select_statement>  
[;]  
  
<reject_options> ::=  
{  
    | REJECT_TYPE = value | percentage  
    | REJECT_VALUE = reject_value  
    | REJECT_SAMPLE_VALUE = reject_sample_value  
}  
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT <select_criteria>  
```  
  
## <a name="arguments"></a>引數  
 [ [ *database_name* . [ *schema_name* ] . ] | *schema_name* . ] *table_name*  
 要在資料庫中建立之資料表的第一到第三部分名稱。 就外部資料表而言，只有資料表中繼資料會儲存在關聯式資料庫中。  
  
 LOCATION =  '*hdfs_folder*'  
 指定要將 SELECT 陳述式的結果寫入至外部資料來源上的哪個位置。 此位置是一個資料夾名稱，並可視需要包含「Hadoop 叢集」或「Azure 儲存體 Blob」之根資料夾的相對路徑。  如果此位置尚未存在，PolyBase 將會建立路徑和資料夾。  
  
 外部檔案會寫入至 *hdfs_folder* 並命名為 *QueryID_date_time_ID.format*，其中 *ID* 是一個累加識別碼，而 *format* 則是所匯出資料的格式。 例如，QID776_20160130_182739_0.orc。  
  
 DATA_SOURCE = *external_data_source_name*  
 指定包含儲存或將儲存外部資料之位置的外部資料來源 名稱。 此位置位於「Hadoop 叢集」或「Azure 儲存體 Blob」上。 若要建立外部資料來源，請使用 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)。  
  
 FILE_FORMAT = *external_file_format_name*  
 指定包含外部資料檔案格式之外部檔案格式物件的名稱。 若要建立外部檔案格式，請使用 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)。  
  
 拒絕選項  
 執行這個 CREATE EXTERNAL TABLE AS SELECT 陳述式時，不適用拒絕選項。 取而代之的是，會在這裡指定拒絕選項，以便讓資料庫能夠在稍後從外部資料表匯入資料時使用它們。 稍後，當 CREATE TABLE AS SELECT 陳述式從外部資料表選取資料時，資料庫將會使用拒絕選項來決定在停止匯入之前，可允許發生匯入失敗的資料列數目或百分比。  
  
 REJECT_VALUE = *reject_value*  
 指定在資料庫停止匯入之前，可允許發生匯入失敗的資料列值或百分比。  
  
 REJECT_TYPE = **value** | percentage  
 指明是要將 REJECT_VALUE 選項指定為常值還是百分比。  
  
 value  
 REJECT_VALUE 是常值，而不是百分比。  當失敗的資料列數目超出 *reject_value* 時，資料庫將會停止從外部資料檔案匯入資料列。  
  
 例如，如果 REJECT_VALUE = 5 且 REJECT_TYPE = value，資料庫就會在 5 個資料列發生匯入失敗時，停止匯入資料列。  
  
 percentage  
 REJECT_VALUE 是百分比，而不是常值。 當失敗的資料列「百分比」超出 *reject_value* 時，資料庫將會停止從外部資料檔案匯入資料列。 失敗的資料列百分比會每隔一段時間就計算一次。  
  
 REJECT_SAMPLE_VALUE = *reject_sample_value*  
 當 REJECT_TYPE = percentage 時便為必要項目，這指定了資料庫重新計算失敗的資料列百分比之前，會嘗試匯入的資料列數目。  
  
 例如，如果 REJECT_SAMPLE_VALUE = 1000，資料庫將會在已嘗試從外部資料檔案匯入 1000 個資料列之後，計算失敗的資料列百分比。 如果失敗的資料列百分比小於 *reject_value*，資料庫就會嘗試載入另外 1000 個資料列。 資料庫會在嘗試匯入每個額外的 1000 個資料列之後，持續重新計算失敗的資料列百分比。  
  
> [!NOTE]  
>  由於資料庫會不時計算失敗的資料列百分比，因此實際的失敗資料列百分比可能超出 *reject_value*。  
  
 範例  
  
 此範例說明三個 REJECT 選項彼此如何互動。 例如，如果 REJECT_TYPE = percentage、REJECT_VALUE = 30 及 REJECT_SAMPLE_VALUE = 100，就可能發生下列案例：  
  
-   資料庫會嘗試載入前 100 個資料列；其中有 25 個失敗，75 個成功。  
  
-   失敗的資料列百分比計算後為 25%，低於拒絕值 30%。 因此，不需要停止載入。  
  
-   資料庫會嘗試載入接下來 100 個資料列；這次有 25 個成功，75 個失敗。  
  
-   失敗的資料列百分比重新計算後為 50%。 失敗的資料列百分比已超出 30% 拒絕值。  
  
-   在嘗試載入 200 個資料列之後，因為失敗的資料列達 50%，已超出指定的 30% 限制，所以載入失敗。  
  
 WITH *common_table_expression*  
 指定稱為通用資料表運算式 (CTE) 的暫存具名結果集。 如需詳細資訊，請參閱 [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)。  
  
 SELECT \<select_criteria> 在新資料表中填入 SELECT 陳述式所產生的結果。 *select_criteria* 是 SELECT 陳述式的主體，可決定要複製到新資料表的資料。 如需 SELECT 陳述式的相關資訊，請參閱 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 若要執行此命令，**資料庫使用者**需要具備下列所有權限或成員資格：  
  
-   將包含新資料表之本機結構描述的 **ALTER SCHEMA** 權限，或 **db_ddladmin** 固定資料庫角色的成員資格。  
  
-   **CREATE TABLE** 權限或 **db_ddladmin** 固定資料庫角色的成員資格。  
  
-   *select_criteria*中所參考之任何物件上的 **SELECT** 權限。  
  
 登入需要下列所有權限：  
  
-   **ADMINISTER BULK OPERATIONS** 權限  
  
-   **ALTER ANY EXTERNAL DATA SOURCE** 權限  
  
-   **ALTER ANY EXTERNAL FILE FORMAT** 權限  
  
-   登入必須具備寫入權限，才能對「Hadoop 叢集」或「Azure 儲存體 Blob」上的外部資料夾進行讀取和寫入。  
 
 > [!IMPORTANT]  
 >  ALTER ANY EXTERNAL DATA SOURCE 權限可讓任何主體都能夠建立及修改任何外部資料來源物件，因此也會讓主體能夠存取資料庫上的所有資料庫範圍認證。 必須將此權限視為具高度權限，因此必須僅授與系統中受信任的主體。
  
## <a name="error-handling"></a>錯誤處理  
 當 CREATE EXTERNAL TABLE AS SELECT 將資料匯出至以文字分隔的檔案時，將不會有任何發生匯出失敗之資料列的拒絕檔案。  
  
 建立外部資料表時，資料庫會嘗試連線至外部 Hadoop 叢集或「Azure 儲存體 Blob」。 如果連線失敗，命令就會失敗而不會建立外部資料表。 由於資料庫會至少重試連線 3 次，因此可能需要一分鐘或更久的時間，命令才會失敗。  
  
 如果 CREATE EXTERNAL TABLE AS SELECT 被取消或失敗，資料庫將會進行一次嘗試，以移除已經在外部資料來源上建立的任何新檔案和資料夾。  
  
 資料庫將會回報在資料匯出期間，於外部資料來源上發生的任何 Java 錯誤。  
  
##  <a name="GeneralRemarks"></a> 一般備註  
 在 CETAS 陳述式執行完成之後，您便可以在外部資料表上執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢。 除非您使用 CREATE TABLE AS SELECT 陳述式來進行匯入，否則這些作業會在查詢的持續期間將資料匯入至資料庫。  
  
 外部資料表名稱和定義會儲存在資料庫中繼資料中。 資料會儲存在外部資料來源中。  
  
 外部檔案命名為 *QueryID_date_time_ID.format*，其中 *ID* 是累加識別碼，而 *format* 是匯出的資料格式。 例如，QID776_20160130_182739_0.orc。  
  
 CETAS 陳述式一律會建立非資料分割資料表，即使來源資料表是資料分割資料表時也一樣。  
  
 針對以 EXPLAIN 建立的查詢計劃，資料庫會將下列查詢計劃作業用於外部資料表：  
  
-   外部隨機移動  
  
-   外部廣播移動  
  
-   外部資料分割移動  
  
 **適用於：**  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]作為建立外部資料表的先決條件，應用裝置系統管理員必須設定 Hadoop 管連線能力。 如需詳細資訊，請參閱 APS 文件 (可從[這裡](http://www.microsoft.com/download/details.aspx?id=48241) 下載) 中的＜Configure Connectivity to External Data (Analytics Platform System)＞(設定對外部資料的連線能力 (Analytics Platform System))。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 由於外部資料表資料位於資料庫外，因此備份和還原作業將只會在儲存於資料庫中的資料上進行。 這意謂著將只會備份和還原中繼資料。  
  
 還原包含外部資料表的資料庫備份時，資料庫不會驗證對外部資料來源的連線。 如果無法存取原始來源，外部資料表的中繼資料還原仍然會成功，但外部資料表上的 SELECT 作業則會失敗。  
  
 資料庫並不保證資料庫與外部資料之間的資料一致性。 如果您是客戶，就必須全權負責維護外部資料與資料庫之間的一致性。  
  
 外部資料表不支援資料操作語言 (DML) 作業。 例如，您無法使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] update、insert 或 delete [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式來修改外部資料。  
  
 外部資料表上允許的資料定義語言 (Data Definition Language, DDL) 作業僅限 CREATE TABLE、DROP TABLE、CREATE STATISTICS、DROP STATISTICS、CREATE VIEW 及 DROP VIEW。  
  
 執行 32 個並行的 PolyBase 查詢時，PolyBase 每個資料夾可取用的檔案數目上限為 33000 個檔案。 這個上限數同時包含了每個 HDFS 資料夾中的檔案和子資料夾。 如果並行程度小於 32，使用者就可以針對 HDFS 中內含超過 33000 個檔案的資料夾執行 PolyBase 查詢。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議 Hadoop 和 PolyBase 的使用者使用簡短的檔案路徑，且所使用的每個 HDFS 資料夾檔案數目不要超過 30000 個檔案。 參考太多檔案時，就會發生 JVM 記憶體不足例外狀況。  
  
 [SET ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md) 對這個 CREATE EXTERNAL TABLE AS SELECT 沒有任何作用。 若要達到類似的行為，請使用 [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md)。  
  
 當 CREATE EXTERNAL TABLE AS SELECT 從 RCFile 進行選取時，RCFile 中的資料行值不得包含縱線字元 '|'。  
  
## <a name="locking"></a>鎖定  
 在 SCHEMARESOLUTION 上採取共用鎖定。  
  
##  <a name="Examples"></a> 範例  
  
### <a name="a-create-a-hadoop-table-using-create-external-table-as-select-cetas"></a>A. 使用 CREATE EXTERNAL TABLE AS SELECT (CETAS) 來建立 Hadoop 資料表  
 下列範例會使用來自來源資料表 `dimCustomer`的資料行定義和資料，來建立一個名為 `hdfsCustomer` 的新外部資料表。  
  
 資料表定義會儲存在資料庫中，而 SELECT 陳述式的結果則會匯出至位於 Hadoop 外部資料來源 *customer_ds* 上的 '/pdwdata/customer.tbl' 檔案。 此檔案會根據外部檔案格式 *customer_ff*來格式化。  
  
 檔案名稱會由資料庫產生，並且包含查詢識別碼，方便將檔案與產生檔案的查詢對應。  
  
 客戶目錄前的路徑 `hdfs://xxx.xxx.xxx.xxx:5000/files/` 必須是已經存在的路徑。 不過，如果客戶目錄不存在，資料庫就會建立該目錄。  
  
> [!NOTE]  
>  這個範例指定的是 5000。 如果未指定連接埠，資料庫就會使用 8020 作為預設連接埠。  
  
 產生的 Hadoop 位置和檔案名稱將會是 `hdfs:// xxx.xxx.xxx.xxx:5000/files/Customer/ QueryID_YearMonthDay_HourMinutesSeconds_FileIndex.txt.`。  
  
```  
  
      -- Example is based on AdventureWorks   
CREATE EXTERNAL TABLE hdfsCustomer  
WITH (  
        LOCATION='/pdwdata/customer.tbl',  
        DATA_SOURCE = customer_ds,  
        FILE_FORMAT = customer_ff  
) AS SELECT * FROM dimCustomer;  
```  
  
### <a name="b-use-a-query-hint-with-create-external-table-as-select-cetas"></a>B. 搭配 CREATE EXTERNAL TABLE AS SELECT (CETAS) 使用查詢提示  
 此查詢示範搭配 CETAS 陳述式使用查詢聯結提示的基本語法。 在提交查詢之後，資料庫會使用雜湊聯結策略來產生查詢計劃。 如需有關聯結提示及如何使用 OPTION 子句的詳細資訊，請參閱 [OPTION 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md)。  
  
> [!NOTE]  
>  這個範例指定的是 5000。 如果未指定連接埠，資料庫就會使用 8020 作為預設連接埠。  
  
```  
  
      -- Example is based on AdventureWorks  
CREATE EXTERNAL TABLE dbo.FactInternetSalesNew  
WITH   
    (   
        LOCATION = '/files/Customer',  
        DATA_SOURCE = customer_ds,  
        FILE_FORMAT = customer_ff  
    )  
AS SELECT T1.* FROM dbo.FactInternetSales T1 JOIN dbo.DimCustomer T2  
ON ( T1.CustomerKey = T2.CustomerKey )  
OPTION ( HASH JOIN );  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [CREATE TABLE &#40;Azure SQL 資料倉儲、平行處理資料倉儲&#41;](~/t-sql/statements/create-table-azure-sql-data-warehouse.md)   
 [CREATE TABLE AS SELECT &#40;Azure SQL 資料倉儲&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  


