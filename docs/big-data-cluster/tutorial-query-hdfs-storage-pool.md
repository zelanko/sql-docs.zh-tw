---
title: 如何在 SQL Server 的巨量資料叢集查詢 HDFS |Microsoft Docs
description: 本教學課程會示範如何查詢 SQL Server 2019 巨量資料叢集 （預覽） 中的 HDFS 資料。 您建立儲存體集區中資料的外部資料表，然後再執行查詢。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/11/2018
ms.topic: tutorial
ms.prod: sql
ms.openlocfilehash: c6f0f01936d5b6e570c2bff53d19ae7a64f151ab
ms.sourcegitcommit: 38f35b2f7a226ded447edc6a36665eaa0376e06e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2018
ms.locfileid: "49644117"
---
# <a name="tutorial-query-hdfs-in-a-sql-server-big-data-cluster"></a>教學課程： SQL Server 的巨量資料叢集以查詢 HDFS

本教學課程會示範如何查詢中的 SQL Server 2019 巨量資料叢集的 HDFS 資料。

在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 建立指向在巨量資料叢集的 HDFS 資料的外部資料表。
> * 在主要執行個體中加入此資料與高價值的資料。

> [!TIP]
> 如果您想，您可以下載並執行命令的指令碼，在本教學課程。 如需相關指示，請參閱 <<c0> [ 資料虛擬化範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-virtualization)GitHub 上。

## <a name="prerequisites"></a>先決條件

- [將巨量資料叢集的 Kubernetes 上部署](deployment-guidance.md)。
- [安裝 Azure Data Studio 和 SQL Server 2019 副檔名](deploy-big-data-tools.md)。
- [將範例資料載入叢集](#sampledata)。

[!INCLUDE [Load sample data](../includes/big-data-cluster-load-sample-data.md)]

## <a name="create-an-external-table-to-hdfs"></a>建立外部資料表到 HDFS

存放集區包含儲存在 HDFS 中的 CSV 檔案中的 web 點選流資料。 您可以使用下列步驟來定義外部資料表可存取該檔案中的資料。

1. 在 Azure Data Studio，連接到您的巨量資料叢集的 SQL Server 主要執行個體。 如需詳細資訊，請參閱 <<c0> [ 連接到 SQL Server 的主要執行個體](deploy-big-data-tools.md#master)。

2. 在連線 中按兩下**伺服器**視窗以顯示 SQL Server 的主要執行個體的伺服器儀表板。 選取 **新的查詢**。

   ![SQL Server 的主要執行個體查詢](./media/tutorial-query-hdfs-storage-pool/sql-server-master-instance-query.png)

3. 執行下列 TRANSACT-SQL 命令，以將內容變更為**銷售**主要執行個體中的資料庫。

   ```sql
   USE Sales
   GO
   ```

4. 定義要從 HDFS 讀取的 CSV 檔案格式。 按 F5 執行陳述式。

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

5. 建立可讀取的外部資料表`/clickstream_data`從存放集區。 **SqlStoragePool**可從巨量資料叢集的主要執行個體存取。

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
