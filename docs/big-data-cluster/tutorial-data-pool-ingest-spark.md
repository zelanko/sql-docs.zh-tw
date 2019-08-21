---
title: 使用 Spark 作業內嵌資料
titleSuffix: SQL Server big data clusters
description: 本教學課程示範如何[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]使用 Azure Data Studio 中的 Spark 作業, 將資料內嵌到的資料集區。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: shivsood
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5325b44512d2dc1522d4bc49478e65ae4c0999e0
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653292"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-spark-jobs"></a>教學課程：使用 Spark 作業將資料內嵌至 SQL Server 資料集區

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本教學課程示範如何使用 Spark 作業, 將資料載入的[資料集](concept-data-pool.md) [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]區。 

在本教學課程中，您將了解如何：

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

1. 按兩下 [伺服器] 視窗中的連線，顯示 SQL Server 主要執行個體的伺服器儀表板。 選取 [新增查詢]。

   ![SQL Server 主要執行個體查詢](./media/tutorial-data-pool-ingest-spark/sql-server-master-instance-query.png)

1. 如果資料集區沒有外部資料來源，請加以建立。

   ```sql
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
  
1. 在 CTP 3.1 中，資料集區的建立是非同步的，但目前沒有方法可判斷何時完成。 請等候兩分鐘，確保資料集區建立完成，再繼續進行。

## <a name="start-a-spark-streaming-job"></a>啟動 Spark 串流作業

下一個步驟是建立 Spark 串流作業，將來自存放集區 (HDFS) 的 Web 點選流資料載入您在資料集區中建立的外部資料表。

1. 在 Azure Data Studio 中，連線到巨量資料叢集的主要執行個體。 如需詳細資訊，請參閱[連線到巨量資料叢集](connect-to-big-data-cluster.md)。

1. 按兩下 [伺服器] 視窗中的 HDFS/Spark 閘道連線。 然後選取 [New Spark Job] \(新增 Spark 作業\)。

   ![新增 Spark 作業](media/tutorial-data-pool-ingest-spark/hdfs-new-spark-job.png)

1. 在 [新增作業] 視窗的 [作業名稱] 欄位中，輸入名稱。

1. 在 [Jar/py File] \(Jar/py 檔案\) 下拉式清單中，選取 [HDFS]。 然後輸入下列 jar 檔案路徑：

   ```text
   /jar/mssql-spark-lib-assembly-1.0.jar
   ```

1. 在 [主要類別] 欄位中，輸入 `FileStreaming`。

1. 在 [引數] 欄位中，輸入下列文字，並在 `<your_password>` 預留位置中指定 SQL Server 主要執行個體的密碼。 

   ```text
   --server mssql-master-pool-0.service-master-pool --port 1433 --user sa --password <your_password> --database sales --table web_clickstreams_spark_results --source_dir hdfs:///clickstream_data --input_format csv --enable_checkpoint false --timeout 380000
   ```

   下表描述每一個引數：

   | 引數 | 描述 |
   |---|---|
   | 伺服器名稱 (server name) | 用於讀取資料表結構描述的 SQL Server |
   | 連接埠編號 | SQL Server 正在接聽的連接埠 (預設值 1433) |
   | username | SQL Server 登入使用者名稱 |
   | password | SQL Server 登入密碼 |
   | 資料庫名稱 | 目標資料庫 |
   | 外部資料表名稱 | 用於表示結果的資料表 |
   | 串流的來源目錄 | 這必須是完整的 URI，例如 "hdfs:///clickstream_data" |
   | 輸入格式 | 可為 "csv"、"parquet" 或 "json" |
   | 啟用檢查點 | true 或 false |
   | timeout | 結束前可執行作業的時間 (以毫秒為單位) |

1. 按下 [提交]，提交作業。

   ![Spark 作業提交](media/tutorial-data-pool-ingest-spark/spark-new-job-settings.png)

## <a name="query-the-data"></a>查詢資料

下列步驟顯示 Spark 串流作業已將來自 HDFS 的資料載入資料集區。

1. 查詢內嵌資料之前，請先查看工作記錄輸出，看看作業是否完成。

   ![Spark 作業記錄](media/tutorial-data-pool-ingest-spark/spark-task-history.png)

1. 返回您在本教學課程開頭開啟的 SQL Server 主要執行個體查詢視窗。

1. 執行下列查詢，檢查內嵌資料。

   ```sql
   USE Sales
   GO
   SELECT count(*) FROM [web_clickstreams_spark_results];
   SELECT TOP 10 * FROM [web_clickstreams_spark_results];
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
