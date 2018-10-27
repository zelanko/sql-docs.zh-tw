---
title: 如何將資料內嵌到 Spark 作業的 SQL Server 資料集區 |Microsoft Docs
description: 本教學課程會示範如何將資料內嵌到 Spark 作業在 Studio 中使用 Azure 資料的 SQL Server 2019 巨量資料叢集 （預覽） 的資料集區。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/16/2018
ms.topic: tutorial
ms.prod: sql
ms.openlocfilehash: d4ee9037e1762f11a569c94e416fcf5e45449d46
ms.sourcegitcommit: 38f35b2f7a226ded447edc6a36665eaa0376e06e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2018
ms.locfileid: "49644130"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-spark-jobs"></a>教學課程： 將資料內嵌到 Spark 作業的 SQL Server 資料集區

本教學課程示範如何使用 Spark 作業，將資料載入[資料集區](concept-data-pool.md)的 SQL Server 2019 巨量資料叢集 （預覽）。 

在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 建立外部資料表的資料集區中。
> * 建立將資料從 HDFS Spark 作業。
> * 查詢外部資料表中的結果。

> [!TIP]
> 如果您想，您可以下載並執行命令的指令碼，在本教學課程。 如需相關指示，請參閱 <<c0> [ 資料集區範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool)GitHub 上。

## <a id="prereqs"></a> 必要條件

* [將巨量資料叢集的 Kubernetes 上部署](deployment-guidance.md)。
* [安裝 Azure Data Studio 和 SQL Server 2019 副檔名](deploy-big-data-tools.md)。
* [將範例資料載入叢集](#sampledata)。

[!INCLUDE [Load sample data](../includes/big-data-cluster-load-sample-data.md)]

## <a name="create-an-external-table-in-the-data-pool"></a>建立資料集區中的外部資料表

下列步驟會建立外部資料表名為資料集區內**web_clickstreams_spark_results**。 本表然後可用做為位置擷取資料到巨量資料叢集。

1. 在 Azure Data Studio，連接到您的巨量資料叢集的 SQL Server 主要執行個體。 如需詳細資訊，請參閱 <<c0> [ 連接到 SQL Server 的主要執行個體](deploy-big-data-tools.md#master)。

1. 在連線 中按兩下**伺服器**視窗以顯示 SQL Server 的主要執行個體的伺服器儀表板。 選取 **新的查詢**。

   ![SQL Server 的主要執行個體查詢](./media/tutorial-data-pool-ingest-spark/sql-server-master-instance-query.png)

1. 建立名為外部資料表**web_clickstreams_spark_results**資料集區中。 `SqlDataPool`資料來源是可從任何巨量資料叢集的主要執行個體的特殊的資料來源類型。

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
  
1. 在 CTP 2.0 中，建立資料集區是非同步的但沒有任何方式可判斷當尚未完成。 等候兩分鐘，以確定資料集區建立後再繼續。

## <a name="start-a-spark-streaming-job"></a>啟動 Spark 串流作業

下一個步驟是建立 Spark 串流作業，從存放集區 (HDFS) 載入 web 點選流資料到您建立資料集區中的外部資料表。

1. 在 Azure Data Studio，連接到您的巨量資料叢集的 HDFS/Spark 閘道。 如需詳細資訊，請參閱 <<c0> [ 連接到 HDFS/Spark 閘道](deploy-big-data-tools.md#hdfs)。

1. 在 HDFS/Spark 閘道連按兩下**伺服器**視窗。 然後選取**新的 Spark 作業**。

   ![新的 Spark 作業](media/tutorial-data-pool-ingest-spark/hdfs-new-spark-job.png)

1. 在**新的工作** 視窗中，輸入中的名稱**作業名稱**欄位。

1. 在  **Jar/py 檔案**下拉式清單中，選取**HDFS**。 然後輸入下列 jar 檔案路徑：

   ```text
   /jar/mssql-spark-lib-assembly-1.0.jar
   ```

1. 在 **引數**欄位中，輸入下列文字： 指定 SQL Server 主要執行個體中的密碼`<your_password>`預留位置。 

   ```text
   mssql-master-pool-0.service-master-pool 1433 sa <your_password> sales web_clickstreams_spark_results hdfs:///clickstream_data csv false
   ```

   下表描述每個引數：

   | 引數 | 描述 |
   |---|---|
   | 伺服器名稱 (server name) | SQL Server 使用，來讀取資料表的結構描述 |
   | 連接埠編號 | SQL Server 連接埠 （預設值 1433年） 上接聽 |
   | username | SQL Server 登入使用者名稱 |
   | 密碼 | SQL Server 登入密碼 |
   | 資料庫名稱 | 目標資料庫 |
   | 外部資料表名稱 | 使用查詢結果的資料表 |
   | 資料流的來源目錄 | 這必須是完整的 URI，例如"hdfs: / / clickstream_data" |
   | 輸入的格式 | 這可以是"csv"、"parquet"或"json" |
   | 啟用檢查點 | true 或 false |

1. 按下**送出**提交工作。

   ![Spark 作業提交](media/tutorial-data-pool-ingest-spark/spark-new-job-settings.png)

## <a name="query-the-data"></a>查詢資料

下列步驟說明，Spark 串流作業載入的資料從 HDFS 資料集區。

1. 之前查詢將內嵌的資料，看看工作歷程記錄輸出，以查看的作業已完成。

   ![Spark 作業歷程記錄](media/tutorial-data-pool-ingest-spark/spark-task-history.png)

1. 返回您在本教學課程開頭所開啟的 SQL Server 主要執行個體查詢視窗...

1. 執行下列查詢來檢查將內嵌的資料。

   ```sql
   USE Sales
   GO
   SELECT count(*) FROM [web_clickstreams_spark_results];
   SELECT TOP 10 * FROM [web_clickstreams_spark_results];
   ```

## <a name="clean-up"></a>清除

您可以使用下列命令，移除在本教學課程中建立的資料庫物件。

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_spark_results];
```

## <a name="next-steps"></a>後續步驟

深入了解如何在 Azure 資料 Studio 中執行 notebook 範例：
> [!div class="nextstepaction"]
> [執行範例 notebook](tutorial-notebook-spark.md)
