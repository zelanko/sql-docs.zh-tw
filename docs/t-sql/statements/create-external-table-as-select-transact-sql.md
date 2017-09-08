---
title: "建立外部 TABLE AS SELECT (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.service: sql-data-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
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
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 716c0fdaa701865e8d35154cd19068051e0ab017
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-external-table-as-select-transact-sql"></a>建立外部 TABLE AS SELECT (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  建立外部資料表，然後，以平行方式，將結果匯出的[!INCLUDE[tsql](../../includes/tsql-md.md)]至 Hadoop 或 Azure 儲存體 Blob 的 SELECT 陳述式。  
  
 使用建立外部資料表 AS 選取 (CETAS) 陳述式：  
  
-   將資料庫資料表匯出至 Hadoop 或 Azure blob 儲存體。  
  
-   從 Hadoop 或 Azure blob 儲存體匯入資料，並將它儲存在資料庫中。  
  
-   查詢資料從 Hadoop 或 Azure blob 儲存體、 加入關聯式資料庫的資料表，並將結果寫回至 Hadoop 或 Azure blob 儲存體。  
  
-   查詢資料從 Hadoop 或 Azure blob 儲存體、 轉換使用資料庫的快速處理功能，並寫回至 Hadoop 或 Azure blob 儲存體。  
  
 如需詳細資訊，請參閱 [開始使用 PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [TRANSACT-SQL 語法慣例 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [[ *database_name* 。 [ *schema_name* ]。 ] |*schema_name* 。 ] *table_name*  
 一至三位在資料庫中建立資料表的部分名稱。 外部資料表，資料表中繼資料會儲存在關聯式資料庫。  
  
 位置 = '*hdfs_folder*'  
 指定要寫入外部資料來源上的 SELECT 陳述式的結果。 資料夾名稱，並且可以選擇性地包含在 Hadoop 叢集或 Azure 儲存體 Blob 的根資料夾的相對路徑。  PolyBase 會建立路徑和資料夾不存在。  
  
 外部檔案會寫入至*hdfs_folder*和具名*QueryID_date_time_ID.format*，其中*識別碼*是累加識別碼和*格式*是匯出的資料格式。 例如，QID776_20160130_182739_0.orc。  
  
 DATA_SOURCE = *external_data_source_name*  
 指定外部資料來源物件包含外部資料已儲存的位置，或將儲存的位置的名稱。 Hadoop 叢集或 Azure 儲存體 Blob 的位置。 若要建立外部資料來源，使用[CREATE EXTERNAL DATA SOURCE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 FILE_FORMAT = *external_file_format_name*  
 指定外部檔案格式物件包含外部資料檔案的格式名稱。 若要建立外部檔案格式，請使用[CREATE EXTERNAL FILE FORMAT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
 拒絕選項  
 拒絕選項不適當時執行此 CREATE EXTERNAL TABLE AS SELECT 陳述式。 相反地，在此處所指定，讓資料庫可以使用它們在稍後當它從匯入資料的外部資料表。 稍後，當 CREATE TABLE AS SELECT 陳述式會從外部資料表選取資料，資料庫將使用拒絕選項來判斷數字或匯入之前停止匯入失敗的資料列的百分比。  
  
 REJECT_VALUE = *reject_value*  
 指定的值或匯入資料庫中止匯入之前失敗的資料列百分比。  
  
 REJECT_TYPE =**值**| 百分比  
 將釐清是否 REJECT_VALUE 選項指定為常值或百分比。  
  
 value  
 REJECT_VALUE 是常值，而不是百分比。  資料庫將會停止從外部資料檔案匯入的資料列，當失敗的資料列數目超過*reject_value*。  
  
 例如，如果 REJECT_VALUE = 5 且 REJECT_TYPE = value，資料庫將會停止匯入的資料列之後無法匯入 5 個資料列。  
  
 百分比  
 REJECT_VALUE 是百分比，而不是常值的值。 資料庫將會停止匯入的資料列，從外部資料檔案時*百分比*失敗的資料列超過*reject_value*。 失敗的資料列百分比的計算間隔。  
  
 REJECT_SAMPLE_VALUE = *reject_sample_value*  
 當 REJECT_TYPE = 百分比，這會指定要在資料庫重新計算失敗資料列百分比之前嘗試匯入的資料列數。  
  
 例如，如果 REJECT_SAMPLE_VALUE = 1000，已嘗試從外部資料檔案匯入 1000 個資料列之後，資料庫會計算失敗資料列的百分比。 如果失敗的資料列的百分比小於*reject_value*，資料庫會嘗試載入其他 1000 個資料列。 資料庫會繼續嘗試匯入每個額外的 1000 個資料列重新計算失敗資料列的百分比。  
  
> [!NOTE]  
>  由於資料庫會在時間間隔計算失敗資料列的百分比，可能會超過實際的失敗資料列百分比*reject_value*。  
  
 範例：  
  
 這個範例會示範如何與彼此互動的三個拒絕選項。 例如，如果 REJECT_TYPE = 百分比，REJECT_VALUE = 30，而且 REJECT_SAMPLE_VALUE = 100，發生下列狀況：  
  
-   資料庫會嘗試載入前 100 個資料列。25 失敗和 75 成功。  
  
-   失敗的資料列百分比的計算方式為 25%小於拒絕值為 30%。 因此，不需要停止負載。  
  
-   資料庫會嘗試載入 100 的資料列。這次 25 成功和失敗 75。  
  
-   重新計算失敗資料列的百分比為 50%。 失敗的資料列的百分比已超過 30%拒絕的值。  
  
-   載入失敗與失敗的 50%的資料列之後嘗試載入 200 個資料列，其大於指定 30%的限制。  
  
 與*common_table_expression*  
 指定稱為通用資料表運算式 (CTE) 的暫存具名結果集。 如需詳細資訊，請參閱[common_table_expression &#40; 與TRANSACT-SQL &#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 選取\<select_criteria > 填入新資料表的 SELECT 陳述式的結果。 *select_criteria*是判斷哪些資料来複製到新資料表的 SELECT 陳述式的主體。 SELECT 陳述式的相關資訊，請參閱[SELECT &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 若要執行此命令**資料庫使用者**需要所有的這些權限或成員資格：  
  
-   **ALTER SCHEMA**本機的結構描述會包含新的資料表或中的成員資格的權限**db_ddladmin**固定的資料庫角色。  
  
-   **CREATE TABLE**權限或成員資格**db_ddladmin**固定的資料庫角色。  
  
-   **選取**中所參考的任何物件的權限*select_criteria*。  
  
 登入需要所有這些權限：  
  
-   **ADMINISTER BULK OPERATIONS**權限  
  
-   **ALTER ANY EXTERNAL DATA SOURCE**權限  
  
-   **ALTER ANY EXTERNAL FILE FORMAT**權限  
  
-   登入必須具有讀取和寫入至外部資料夾的 Hadoop 叢集或 Azure 儲存體 Blob 的寫入權限。  
 
 > [!IMPORTANT]  
 >  ALTER ANY EXTERNAL DATA SOURCE 權限授與任何主體建立和修改任何外部資料來源物件的能力，因此，它也會授與存取在資料庫上的所有資料庫範圍認證的能力。 此權限必須被視為具有高度權限，因此必須只授與信任的主體在系統中。
  
## <a name="error-handling"></a>錯誤處理  
 當 CREATE EXTERNAL TABLE AS SELECT 將資料匯出到以文字分隔的檔案時，但沒有拒絕檔案無法匯出的資料列。  
  
 當建立外部資料表，資料庫會嘗試連接到外部的 Hadoop 叢集或 Azure 儲存體 Blob。 如果連接失敗，此命令會失敗，並將不會建立外部資料表。 可能需要一分鐘以上的命令失敗後的資料庫重試連接至少 3 倍。  
  
 如果 CREATE EXTERNAL TABLE AS SELECT 遭到取消或失敗，資料庫就會進行一次嘗試移除任何新的檔案和資料夾中已建立的外部資料來源。  
  
 資料庫將會報告任何資料匯出期間發生外部資料來源的 Java 錯誤。  
  
##  <a name="GeneralRemarks"></a>一般備註  
 CETAS 陳述式完成之後，您可以執行[!INCLUDE[tsql](../../includes/tsql-md.md)]外部資料表的查詢。 這些作業將資料匯入資料庫查詢的持續時間除非您使用 CREATE TABLE AS SELECT 陳述式匯入。  
  
 外部資料表名稱和定義會儲存在資料庫中繼資料中。 資料會儲存在外部資料來源。  
  
 外部檔案命名為 *QueryID_date_time_ID.format*，其中 *ID* 是累加識別碼，而 *format* 是匯出的資料格式。 例如，QID776_20160130_182739_0.orc。  
  
 CETAS 陳述式永遠都會建立一個非資料分割資料表，即使已分割來源資料表。  
  
 針對查詢計畫，以解釋，databaseuses 建立這些外部資料表的查詢計劃作業：  
  
-   外部隨機移動  
  
-   外部廣播移動  
  
-   外部的資料分割移動  
  
 **適用於：**[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]建立外部資料表的必要元件，為應用裝置系統管理員必須設定 hadoop 連接性。   如需詳細資訊，請參閱 < 設定連線到外部資料 (Analytics Platform System) 您可以從下載的 APS 文件中[這裡](http://www.microsoft.com/download/details.aspx?id=48241)。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 因為此外部資料表資料位於外部的資料庫備份和還原作業將只會儲存在資料庫中的資料上操作。 這表示將備份和還原的中繼資料。  
  
 資料庫在還原資料庫備份，其中包含外部資料表時，不會驗證外部資料來源的連接。 如果無法存取原始來源，在外部資料表的中繼資料還原仍然會成功，但上的外部資料表的 SELECT 作業將會失敗。  
  
 資料庫不保證資料一致性 databaseand 外部的資料。 您的客戶，只負責維護外部資料與資料庫之間的一致性。  
  
 外部資料表不支援資料操作語言 (DML) 作業。 例如，您不能使用[!INCLUDE[tsql](../../includes/tsql-md.md)]更新、 插入或刪除[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式以修改外部資料。  
  
 CREATE TABLE、 DROP TABLE、 CREATE STATISTICS、 卸除統計資料、 建立檢視和 DROP VIEW 會允許對外部資料表的唯一資料定義語言 (DDL) 作業。  
  
 PolyBase 可以取用每個資料夾的 33 k 檔案最的多 32 個並行 PolyBase 查詢的執行時。 這個最大的數字會包含每個 HDFS 資料夾中檔案和子資料夾。 如果並行程度小於 32，使用者可以執行 PolyBase 查詢，針對包含多個 33 k 檔案的 HDFS 中的資料夾。 [!INCLUDE[msCoName](../../includes/msconame-md.md)]建議使用者 Hadoop 和 PolyBase 保持簡短的檔案路徑，並且使用每個 HDFS 資料夾不能超過 30 個 k 檔案。 太多檔案參考時，就會發生 JVM 記憶體不足例外狀況。  
  
 [SET ROWCOUNT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-rowcount-transact-sql.md)對此 CREATE EXTERNAL TABLE AS SELECT 沒有影響。 若要達成類似的行為，使用[TOP &#40;TRANSACT-SQL &#41;](../../t-sql/queries/top-transact-sql.md).  
  
 當 CREATE EXTERNAL TABLE AS SELECT 選取從 RCFile 時，RCFile 中的資料行值不能包含管道 ' |' 字元。  
  
## <a name="locking"></a>鎖定  
 SCHEMARESOLUTION 物件上採用共用的鎖定。  
  
##  <a name="Examples"></a> 範例  
  
### <a name="a-create-a-hadoop-table-using-create-external-table-as-select-cetas"></a>A. 建立 Hadoop 資料表使用建立外部資料表 AS 選取 (CETAS)  
 下列範例會建立新的外部資料表名為`hdfsCustomer`，使用資料行定義和資料從來源資料表`dimCustomer`。  
  
 資料表定義會儲存在資料庫中，而且 SELECT 陳述式的結果匯出至 ' / pdwdata/customer.tbl' Hadoop 的外部資料來源上的檔案*customer_ds*。 檔案會依照外部檔案格式來格式化*customer_ff*。  
  
 檔案名稱由資料庫所產生，而且包含輕鬆對齊的查詢來產生該檔案的查詢識別碼。  
  
 路徑`hdfs://xxx.xxx.xxx.xxx:5000/files/`之前在客戶目錄必須已經存在。 不過，如果在客戶目錄不存在，則資料庫會建立目錄。  
  
> [!NOTE]  
>  這個範例會指定為 5000。 如果未指定連接埠，則資料庫會使用 8020 做為預設連接埠。  
  
 位置和檔案名稱將會產生 Hadoop `hdfs:// xxx.xxx.xxx.xxx:5000/files/Customer/ QueryID_YearMonthDay_HourMinutesSeconds_FileIndex.txt.`。  
  
```  
  
      -- Example is based on AdventureWorks   
CREATE EXTERNAL TABLE hdfsCustomer  
WITH (  
        LOCATION='/pdwdata/customer.tbl',  
        DATA_SOURCE = customer_ds,  
        FILE_FORMAT = customer_ff  
) AS SELECT * FROM dimCustomer;  
```  
  
### <a name="b-use-a-query-hint-with-create-external-table-as-select-cetas"></a>B. 使用查詢提示搭配建立外部資料表選取 (CETAS)  
 此查詢會顯示與 CETAS 陳述式中使用查詢的聯結提示的基本語法。 提交查詢之後，資料庫會使用雜湊聯結策略產生查詢計劃。 如需有關聯結提示，以及如何使用 OPTION 子句的詳細資訊，請參閱[OPTION 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/option-clause-transact-sql.md).  
  
> [!NOTE]  
>  這個範例會指定為 5000。 如果未指定連接埠，則資料庫會使用 8020 做為預設連接埠。  
  
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
 [建立資料表 &#40;Azure SQL 資料倉儲、 Parallel Data Warehouse &#41;](~/t-sql/statements/create-table-azure-sql-data-warehouse.md)   
 [建立 TABLE AS SELECT &#40;Azure SQL 資料倉儲 &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [DROP TABLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  



