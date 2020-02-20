---
title: 使用 Spark 作業內嵌資料
titleSuffix: SQL Server Big Data Clusters
description: 此教學課程示範如何使用 Azure Data Studio 中的 Spark 作業，將資料內嵌至 SQL Server 巨量資料叢集的資料集區。
author: rajmera3
ms.author: raajmera
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1f3a8956120f16282cf0a3829f03bf5586c9d791
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75776526"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-spark-jobs"></a>教學課程：使用 Spark 作業將資料內嵌至 SQL Server 資料集區

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本教學課程示範如何使用 Spark 作業將資料載入 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 的[資料集區](concept-data-pool.md)。 

在本教學課程中，您會了解如何：

> [!div class="checklist"]
> * 在資料集區中建立外部資料表。
> * 建立 Spark 作業，以便從 HDFS 載入資料。
> * 查詢外部資料表中的結果。

> [!TIP]
> 如果您想要的話，也可以下載並執行用於本教學課程中命令的指令碼。 如需指示，請參閱 GitHub 上的[資料集區範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool)。

## <a id="prereqs"></a> 必要條件

- [巨量資料工具](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
- [將範例資料載入巨量資料叢集](tutorial-load-sample-data.md)

## <a name="create-an-external-table-in-the-data-pool"></a>在資料集區中建立外部資料表

下列步驟會在資料集區中建立名為 **web_clickstreams_spark_results** 的外部資料表。 然後，此資料表可作為資料內嵌至巨量資料叢集的位置。

1. 在 Azure Data Studio 中，連線到巨量資料叢集的 SQL Server 主要執行個體。 如需詳細資訊，請參閱[連線到 SQL Server 主要執行個體](connect-to-big-data-cluster.md#master)。

1. 按兩下 [伺服器]  視窗中的連線，顯示 SQL Server 主要執行個體的伺服器儀表板。 選取 [新增查詢]  。

   ![SQL Server 主要執行個體查詢](./media/tutorial-data-pool-ingest-spark/sql-server-master-instance-query.png)

1. 建立 MSSQL-Spark 連接器的權限。
   ```sql
   USE Sales
   CREATE LOGIN sample_user  WITH PASSWORD ='password123!#' 
   CREATE USER sample_user FROM LOGIN sample_user

   -- To create external tables in data pools
   GRANT ALTER ANY EXTERNAL DATA SOURCE TO sample_user;

   -- To create external table
   GRANT CREATE TABLE TO sample_user;
   GRANT ALTER ANY SCHEMA TO sample_user;

   ALTER ROLE [db_datareader] ADD MEMBER sample_user
   ALTER ROLE [db_datawriter] ADD MEMBER sample_user
   ```

1. 如果資料集區沒有外部資料來源，請加以建立。

   ```sql
   USE Sales
   GO
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
     CREATE EXTERNAL DATA SOURCE SqlDataPool
     WITH (LOCATION = 'sqldatapool://controller-svc/default');
   ```

1. 在資料集區中建立名為 **web_clickstreams_spark_results** 的外部資料表。

   ```sql
   USE Sales
   GO
   IF NOT EXISTS(SELECT * FROM sys.external_tables WHERE name = 'web_clickstreams_spark_results')
      CREATE EXTERNAL TABLE [web_clickstreams_spark_results]
      ("wcs_click_date_sk" BIGINT , "wcs_click_time_sk" BIGINT , "wcs_sales_sk" BIGINT , "wcs_item_sk" BIGINT , "wcs_web_page_sk" BIGINT , "wcs_user_sk" BIGINT)
      WITH
      (
         DATA_SOURCE = SqlDataPool,
         DISTRIBUTION = ROUND_ROBIN
      );
   ```
   
1. 建立資料集區的登入，並提供權限給使用者。
   ```sql 
   EXECUTE( ' Use Sales; CREATE LOGIN sample_user  WITH PASSWORD = ''password123!#'' ;') AT  DATA_SOURCE SqlDataPool;

   EXECUTE('Use Sales; CREATE USER sample_user; ALTER ROLE [db_datareader] ADD MEMBER sample_user;  ALTER ROLE [db_datawriter] ADD MEMBER sample_user;') AT DATA_SOURCE SqlDataPool;
   ```
   
資料集區外部資料表的建立是封鎖作業。 當指定的資料表已經在所有後端資料集區節點上建立之後，就會恢復控制權。 如果建立作業期間發生失敗，錯誤訊息會傳回給呼叫者。

## <a name="start-a-spark-streaming-job"></a>啟動 Spark 串流作業

下一個步驟是建立 Spark 串流作業，將來自存放集區 (HDFS) 的 Web 點選流資料載入您在資料集區中建立的外部資料表。 這項資料已在[將範例資料載入您的巨量資料叢集](tutorial-load-sample-data.md)中新增至 /clickstream_data。

1. 在 Azure Data Studio 中，連線到巨量資料叢集的主要執行個體。 如需詳細資訊，請參閱[連線到巨量資料叢集](connect-to-big-data-cluster.md)。

2. 建立新的筆記本並選取 Spark | Scala 作為您的核心。

3. 執行 Spark 擷取作業
   1. 設定 Spark-SQL 連接器參數
      ```
      import org.apache.spark.sql.types._
      import org.apache.spark.sql.{SparkSession, SaveMode, Row, DataFrame}

      // Change per your installation
      val user= "username"
      val password= "****"
      val database =  "MyTestDatabase"
      val sourceDir = "/clickstream_data"
      val datapool_table = "web_clickstreams_spark_results"
      val datasource_name = "SqlDataPool"
      val schema = StructType(Seq(
      StructField("wcs_click_date_sk",LongType,true), StructField("wcs_click_time_sk",LongType,true), 
      StructField("wcs_sales_sk",LongType,true), StructField("wcs_item_sk",LongType,true),
      StructField("wcs_web_page_sk",LongType,true), StructField("wcs_user_sk",LongType,true)
      ))

      val hostname = "master-0.master-svc"
      val port = 1433
      val url = s"jdbc:sqlserver://${hostname}:${port};database=${database};user=${user};password=${password};"
      ```
   2. 定義並執行 Spark 作業
      * 每個作業都有兩個部分：readStream 和 writeStream。 以下我們會使用以上定義的結構描述來建立資料框架，然後寫入資料集區中的外部資料表。
      ```
      import org.apache.spark.sql.{SparkSession, SaveMode, Row, DataFrame}
      
      val df = spark.readStream.format("csv").schema(schema).option("header", true).load(sourceDir)
      val query = df.writeStream.outputMode("append").foreachBatch{ (batchDF: DataFrame, batchId: Long) => 
                batchDF.write
                 .format("com.microsoft.sqlserver.jdbc.spark")
                 .mode("append")
                  .option("url", url)
                  .option("dbtable", datapool_table)
                  .option("user", user)
                  .option("password", password)
                  .option("dataPoolDataSource",datasource_name).save()
               }.start()

      query.awaitTermination(40000)
      query.stop()
      ```
## <a name="query-the-data"></a>查詢資料

下列步驟顯示 Spark 串流作業已將來自 HDFS 的資料載入資料集區。

1. 在查詢內嵌資料前，請查看 Spark 執行狀態 (包括 Yarn 應用程式識別碼、Spark UI 和驅動程式記錄)。 當您第一次啟動 Spark 應用程式時，此資訊會顯示在筆記本中。

   ![Spark 執行詳細資料](./media/tutorial-data-pool-ingest-spark/Spark-Joblog-sparkui-yarn.png)

1. 返回您在本教學課程開頭開啟的 SQL Server 主要執行個體查詢視窗。

1. 執行下列查詢，檢查內嵌資料。

   ```sql
   USE Sales
   GO
   SELECT count(*) FROM [web_clickstreams_spark_results];
   SELECT TOP 10 * FROM [web_clickstreams_spark_results];
   ```
1. 您也可以在 Spark 中查詢資料。 例如，以下程式碼會印出資料表中的記錄數：
   ```
   def df_read(dbtable: String,
                url: String,
                dataPoolDataSource: String=""): DataFrame = {
        spark.read
             .format("com.microsoft.sqlserver.jdbc.spark")
             .option("url", url)
             .option("dbtable", dbtable)
             .option("user", user)
             .option("password", password)
             .option("dataPoolDataSource", dataPoolDataSource)
             .load()
             }

   val new_df = df_read(datapool_table, url, dataPoolDataSource=datasource_name)
   println("Number of rows is " +  new_df.count)
   ```
## <a name="clean-up"></a>清除

使用下列命令，移除本教學課程所建立的資料庫物件。

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_spark_results];
```

## <a name="next-steps"></a>後續步驟

了解如何在 Azure Data Studio 中執行範例筆記本：
> [!div class="nextstepaction"]
> [執行範例筆記本](tutorial-notebook-spark.md)
