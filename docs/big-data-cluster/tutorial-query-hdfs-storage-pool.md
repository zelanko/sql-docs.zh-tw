---
title: 查詢存放集區中的 HDFS 資料
titleSuffix: SQL Server big data clusters
description: 本教學課程示範如何在中[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]查詢 HDFS 資料。 您可以透過存放集區中的資料建立外部資料表，然後執行查詢。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7ba5721ef461fe327a3309431cc994a5ed377be7
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652449"
---
# <a name="tutorial-query-hdfs-in-a-sql-server-big-data-cluster"></a>教學課程：查詢 SQL Server 巨量資料叢集中的 HDFS

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本教學課程示範如何在中[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]查詢 HDFS 資料。

在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 建立外部資料表，指向巨量資料叢集中的 HDFS 資料。
> * 將此資料與主要執行個體中的高價值資料聯結。

> [!TIP]
> 如果您想要的話，也可以下載並執行用於本教學課程中命令的指令碼。 如需指示，請參閱 GitHub 上的[資料虛擬化範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-virtualization)。

## <a id="prereqs"></a> 必要條件

- [巨量資料工具](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
- [將範例資料載入巨量資料叢集](tutorial-load-sample-data.md)

## <a name="create-an-external-table-to-hdfs"></a>建立外部資料表以指向 HDFS

存放集區會在儲存於 HDFS 的 CSV 檔案中包含 Web 點選流資料。 使用下列步驟，定義可存取該檔案資料的外部資料表。

1. 在 Azure Data Studio 中，連線到巨量資料叢集的 SQL Server 主要執行個體。 如需詳細資訊，請參閱[連線到 SQL Server 主要執行個體](connect-to-big-data-cluster.md#master)。

1. 按兩下 [伺服器] 視窗中的連線，顯示 SQL Server 主要執行個體的伺服器儀表板。 選取 [新增查詢]。

   ![SQL Server 主要執行個體查詢](./media/tutorial-query-hdfs-storage-pool/sql-server-master-instance-query.png)

1. 執行下列 Transact-SQL 命令，將內容變更為主要執行個體中的 **Sales** 資料庫。

   ```sql
   USE Sales
   GO
   ```

1. 定義要從 HDFS 讀取的 CSV 檔案格式。 按 F5 執行陳述式。

   ```sql
   CREATE EXTERNAL FILE FORMAT csv_file
   WITH (
       FORMAT_TYPE = DELIMITEDTEXT,
       FORMAT_OPTIONS(
           FIELD_TERMINATOR = ',',
           STRING_DELIMITER = '"',
           FIRST_ROW = 2,
           USE_TYPE_DEFAULT = TRUE)
   );
   ```

1. 如果存放集區沒有外部資料來源，請加以建立。

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
   BEGIN
     CREATE EXTERNAL DATA SOURCE SqlStoragePool
     WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   END
   ```

1. 建立可從存放集區讀取 `/clickstream_data` 的外部資料表。 **SqlStoragePool** 可從巨量資料叢集的主要執行個體進行存取。

   ```sql
   CREATE EXTERNAL TABLE [web_clickstreams_hdfs]
   ("wcs_click_date_sk" BIGINT , "wcs_click_time_sk" BIGINT , "wcs_sales_sk" BIGINT , "wcs_item_sk" BIGINT , "wcs_web_page_sk" BIGINT , "wcs_user_sk" BIGINT)
   WITH
   (
       DATA_SOURCE = SqlStoragePool,
       LOCATION = '/clickstream_data',
       FILE_FORMAT = csv_file
   );
   GO
   ```

## <a name="query-the-data"></a>查詢資料

執行下列查詢，將 `web_clickstream_hdfs` 外部資料表中的 HDFS 資料與本機 `Sales` 資料庫中的關聯式資料聯結。

```sql
SELECT  
    wcs_user_sk,
    SUM( CASE WHEN i_category = 'Books' THEN 1 ELSE 0 END) AS book_category_clicks,
    SUM( CASE WHEN i_category_id = 1 THEN 1 ELSE 0 END) AS [Home & Kitchen],
    SUM( CASE WHEN i_category_id = 2 THEN 1 ELSE 0 END) AS [Music],
    SUM( CASE WHEN i_category_id = 3 THEN 1 ELSE 0 END) AS [Books],
    SUM( CASE WHEN i_category_id = 4 THEN 1 ELSE 0 END) AS [Clothing & Accessories],
    SUM( CASE WHEN i_category_id = 5 THEN 1 ELSE 0 END) AS [Electronics],
    SUM( CASE WHEN i_category_id = 6 THEN 1 ELSE 0 END) AS [Tools & Home Improvement],
    SUM( CASE WHEN i_category_id = 7 THEN 1 ELSE 0 END) AS [Toys & Games],
    SUM( CASE WHEN i_category_id = 8 THEN 1 ELSE 0 END) AS [Movies & TV],
    SUM( CASE WHEN i_category_id = 9 THEN 1 ELSE 0 END) AS [Sports & Outdoors]
  FROM [dbo].[web_clickstreams_hdfs]
  INNER JOIN item it ON (wcs_item_sk = i_item_sk
                        AND wcs_user_sk IS NOT NULL)
GROUP BY  wcs_user_sk;
GO
```

## <a name="clean-up"></a>清除

使用下列命令，移除本教學課程所使用的外部資料表。

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_hdfs];
GO
```

## <a name="next-steps"></a>後續步驟

請前往下一篇文章，了解如何從巨量資料叢集查詢 Oracle。
> [!div class="nextstepaction"]
> [查詢 Oracle 中的外部資料](tutorial-query-oracle.md)
