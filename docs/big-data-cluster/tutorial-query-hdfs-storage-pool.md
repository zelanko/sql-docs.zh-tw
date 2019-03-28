---
title: 查詢存放區集區中的 HDFS 資料
titleSuffix: SQL Server 2019 big data clusters
description: 本教學課程會示範如何查詢 SQL Server 2019 巨量資料叢集 （預覽） 中的 HDFS 資料。 您建立儲存體集區中資料的外部資料表，然後再執行查詢。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/27/2018
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 57851a4e0f4cedde1e630afeca49ff26c971c7b5
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511115"
---
# <a name="tutorial-query-hdfs-in-a-sql-server-big-data-cluster"></a>教學課程：查詢 HDFS 中的 SQL Server 的巨量資料叢集

本教學課程會示範如何查詢 SQL Server 2019 巨量資料叢集 （預覽） 中的 HDFS 資料。

在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 建立指向在巨量資料叢集的 HDFS 資料的外部資料表。
> * 在主要執行個體中加入此資料與高價值的資料。

> [!TIP]
> 如果您想，您可以下載並執行命令的指令碼，在本教學課程。 如需相關指示，請參閱 <<c0> [ 資料虛擬化範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-virtualization)GitHub 上。

## <a id="prereqs"></a> 必要條件

- [巨量資料工具](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
- [將範例資料載入您的巨量資料叢集](tutorial-load-sample-data.md)

## <a name="create-an-external-table-to-hdfs"></a>建立外部資料表到 HDFS

存放集區包含儲存在 HDFS 中的 CSV 檔案中的 web 點選流資料。 您可以使用下列步驟來定義外部資料表可存取該檔案中的資料。

1. 在 Azure Data Studio，連接到您的巨量資料叢集的 SQL Server 主要執行個體。 如需詳細資訊，請參閱 <<c0> [ 連接到 SQL Server 的主要執行個體](connect-to-big-data-cluster.md#master)。

1. 在連線 中按兩下**伺服器**視窗以顯示 SQL Server 的主要執行個體的伺服器儀表板。 選取 **新的查詢**。

   ![SQL Server 的主要執行個體查詢](./media/tutorial-query-hdfs-storage-pool/sql-server-master-instance-query.png)

1. 執行下列 TRANSACT-SQL 命令，以將內容變更為**銷售**主要執行個體中的資料庫。

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

1. 如果不存在，請建立存放集區的外部資料來源。

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
   BEGIN
     IF SERVERPROPERTY('ProductLevel') = 'CTP2.3'
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://service-mssql-controller:8080');
     ELSE IF SERVERPROPERTY('ProductLevel') = 'CTP2.4'
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://service-master-pool:50070');
   END
   ```

1. 建立可讀取的外部資料表`/clickstream_data`從存放集區。 **SqlStoragePool**可從巨量資料叢集的主要執行個體存取。

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

執行下列查詢來聯結 HDFS 資料`web_clickstream_hdfs`與在本機之關聯式資料的外部資料表`Sales`資料庫。

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

使用下列命令以移除在本教學課程使用的外部資料表。

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_hdfs];
GO
```

## <a name="next-steps"></a>後續步驟

請前往下一篇文章，以了解如何從巨量資料叢集查詢 Oracle。
> [!div class="nextstepaction"]
> [在 Oracle 中的查詢外部資料](tutorial-query-oracle.md)
