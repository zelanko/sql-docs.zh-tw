---
title: 將資料內嵌至 SQL Server 資料集區
titleSuffix: SQL Server big data clusters
description: 本教學課程示範如何將資料內嵌至 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 的資料集區。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f2ae96a04da69835b4b13886637cf87e62996b57
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653316"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-transact-sql"></a>教學課程：使用 Transact-SQL 將資料內嵌到 SQL Server 資料集區

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本教學課程示範如何使用 Transact-SQL 將資料載入 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 的[資料集區](concept-data-pool.md)。 透過 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]，即可將各種來源的資料內嵌和分散到不同的資料集區執行個體。

在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 在資料集區中建立外部資料表。
> * 將範例 Web 點選流資料插入資料集區資料表。
> * 將資料集區資料表中的資料與本機資料表聯結。

> [!TIP]
> 如果您想要的話，也可以下載並執行用於本教學課程中命令的指令碼。 如需指示，請參閱 GitHub 上的[資料集區範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool)。

## <a id="prereqs"></a> 必要條件

- [巨量資料工具](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
- [將範例資料載入巨量資料叢集](tutorial-load-sample-data.md)

## <a name="create-an-external-table-in-the-data-pool"></a>在資料集區中建立外部資料表

下列步驟會在資料集區建立名為 **web_clickstream_clicks_data_pool** 的外部資料表。 然後，此資料表可作為將資料內嵌至巨量資料叢集的位置。

1. 在 Azure Data Studio 中，連線到巨量資料叢集的 SQL Server 主要執行個體。 如需詳細資訊，請參閱[連線到 SQL Server 主要執行個體](connect-to-big-data-cluster.md#master)。

1. 按兩下 [伺服器]  視窗中的連線，顯示 SQL Server 主要執行個體的伺服器儀表板。 選取 [新增查詢]  。

   ![SQL Server 主要執行個體查詢](./media/tutorial-data-pool-ingest-sql/sql-server-master-instance-query.png)

1. 執行下列 Transact-SQL 命令，將內容變更為主要執行個體中的 **Sales** 資料庫。

   ```sql
   USE Sales
   GO
   ```

1. 如果資料集區沒有外部資料表，請加以建立。

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
     CREATE EXTERNAL DATA SOURCE SqlDataPool
     WITH (LOCATION = 'sqldatapool://controller-svc/default');
   ```

1. 在資料集區建立名為 **web_clickstream_clicks_data_pool** 的外部資料表。

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_tables WHERE name = 'web_clickstream_clicks_data_pool')
      CREATE EXTERNAL TABLE [web_clickstream_clicks_data_pool]
      ("wcs_user_sk" BIGINT , "i_category_id" BIGINT , "clicks" BIGINT)
      WITH
      (
         DATA_SOURCE = SqlDataPool,
         DISTRIBUTION = ROUND_ROBIN
      );
   ```
  
1. 在 CTP 3.1 中，資料集區的建立是非同步的，但目前沒有方法能判斷會何時完成。 請等候兩分鐘，確保資料集區建立完成，再繼續進行。

## <a name="load-data"></a>載入資料

下列步驟使用在先前步驟中建立的外部資料表，將範例 Web 點選流資料內嵌至資料集區。

1. 使用 `INSERT INTO` 陳述式，將查詢結果插入資料集區 (**web_clickstream_clicks_data_pool** 外部資料表)。

   ```sql
   INSERT INTO web_clickstream_clicks_data_pool
   SELECT wcs_user_sk, i_category_id, COUNT_BIG(*) as clicks
     FROM sales.dbo.web_clickstreams_hdfs
   INNER JOIN sales.dbo.item it ON (wcs_item_sk = i_item_sk
                           AND wcs_user_sk IS NOT NULL)
   GROUP BY wcs_user_sk, i_category_id
   HAVING COUNT_BIG(*) > 100;
   ```

1. 使用兩個 SELECT 查詢，檢查插入的資料。

   ```sql
   SELECT count(*) FROM [dbo].[web_clickstream_clicks_data_pool]
   SELECT TOP 10 * FROM [dbo].[web_clickstream_clicks_data_pool]  
   ```

## <a name="query-the-data"></a>查詢資料

將資料集區中所儲存的查詢結果與 **Sales** 資料表中的本機資料聯結。

```sql
SELECT TOP (100)
   w.wcs_user_sk,
   SUM( CASE WHEN i.i_category = 'Books' THEN 1 ELSE 0 END) AS book_category_clicks,
   SUM( CASE WHEN w.i_category_id = 1 THEN 1 ELSE 0 END) AS [Home & Kitchen],
   SUM( CASE WHEN w.i_category_id = 2 THEN 1 ELSE 0 END) AS [Music],
   SUM( CASE WHEN w.i_category_id = 3 THEN 1 ELSE 0 END) AS [Books],
   SUM( CASE WHEN w.i_category_id = 4 THEN 1 ELSE 0 END) AS [Clothing & Accessories],
   SUM( CASE WHEN w.i_category_id = 5 THEN 1 ELSE 0 END) AS [Electronics],
   SUM( CASE WHEN w.i_category_id = 6 THEN 1 ELSE 0 END) AS [Tools & Home Improvement],
   SUM( CASE WHEN w.i_category_id = 7 THEN 1 ELSE 0 END) AS [Toys & Games],
   SUM( CASE WHEN w.i_category_id = 8 THEN 1 ELSE 0 END) AS [Movies & TV],
   SUM( CASE WHEN w.i_category_id = 9 THEN 1 ELSE 0 END) AS [Sports & Outdoors]
FROM [dbo].[web_clickstream_clicks_data_pool] as w
INNER JOIN (SELECT DISTINCT i_category_id, i_category FROM item) as i
   ON i.i_category_id = w.i_category_id
GROUP BY w.wcs_user_sk;
```

## <a name="clean-up"></a>清除

使用下列命令，移除本教學課程所建立的資料庫物件。

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstream_clicks_data_pool];
```

## <a name="next-steps"></a>後續步驟

了解如何使用 Spark 作業，將資料內嵌至資料集區：
> [!div class="nextstepaction"]
> [使用 Spark 作業內嵌資料](tutorial-data-pool-ingest-spark.md)
