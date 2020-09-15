---
title: 教學課程：使用 R 部署群集模型
titleSuffix: SQL machine learning
description: 在這個四部分教學課程系列的第四部分中，您將使用 SQL 機器學習，在 R 中部署群集模型。
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: cawrites
ms.author: chadam
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 327038528ddc238eb5644ad8c0c4b35e2b969313
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178445"
---
# <a name="tutorial-deploy-a-clustering-model-in-r-with-sql-machine-learning"></a>教學課程：使用 SQL 機器學習在 R 中部署群集模型
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
在這個四部分教學課程系列的第四部分中，您將使用 SQL Server 機器學習服務或在巨量資料叢集上，將以 R 開發的群集模型部署到資料庫。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
在這個四部分教學課程系列的第四部分中，您將使用 SQL Server 機器學習服務，將以 R 開發的群集模型部署到資料庫。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
在這個四部分教學課程系列的第四部分中，您將使用 SQL Server R Services，將以 R 開發的群集模型部署到資料庫。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
在這個四部分教學課程系列的第四部分中，您將使用 Azure SQL 受控執行個體機器學習服務，將以 R 開發的群集模型部署到資料庫。
::: moniker-end

為了定期執行群集，當新客戶註冊時，您必須能夠從任何應用程式呼叫 R 指令碼。 若要這麼做，您可以將 R 指令碼放在 SQL 預存程序內，以在資料庫中部署 R 指令碼。 因為您的模型是在資料庫中執行，所以可以輕鬆地針對儲存在資料庫中的資料進行定型。

在本文中，您將學會如何：

> [!div class="checklist"]
> * 建立一個會產生模型的預存程序
> * 執行叢集
> * 使用群集資訊

在[第一部分](r-clustering-model-introduction.md)中，您已安裝必要條件並還原範例資料庫。

在[第二部分](r-clustering-model-prepare-data.md)，您已了解如何準備資料庫中的資料，以執行叢集。

在[第三部分](r-clustering-model-build.md)中，您已了解如何在 R 中建立和定型 K-Means 群集模型。

## <a name="prerequisites"></a>Prerequisites

* 本教學課程系列的第四部分假設您已滿足[**第一部分**](r-clustering-model-introduction.md)的必要條件，並已完成[**第二部分**](r-clustering-model-build.md)和[**第三部分**](r-clustering-model-build.md)中的步驟。

## <a name="create-a-stored-procedure-that-generates-the-model"></a>建立一個會產生模型的預存程序

執行下列 T-SQL 指令碼來建立預存程序。 此程序會重新建立您在本教學課程系列的第二部分和第三部分中所開發的步驟：

* 根據客戶的購買和退貨記錄來分類客戶
* 使用 K-Means 演算法產生客戶的四個叢集

此程序會將產生的客戶叢集對應儲存在資料庫資料表 **customer_return_clusters** 中。

```sql
USE [tpcxbb_1gb]
DROP PROC IF EXISTS generate_customer_return_clusters;
GO
CREATE procedure [dbo].[generate_customer_return_clusters]
AS
/*
  This procedure uses R to classify customers into different groups
  based on their purchase & return history.
*/
BEGIN
    DECLARE @duration FLOAT
    , @instance_name NVARCHAR(100) = @@SERVERNAME
    , @database_name NVARCHAR(128) = db_name()
-- Input query to generate the purchase history & return metrics
    , @input_query NVARCHAR(MAX) = N'
SELECT ss_customer_sk AS customer,
    round(CASE 
            WHEN (
                    (orders_count = 0)
                    OR (returns_count IS NULL)
                    OR (orders_count IS NULL)
                    OR ((returns_count / orders_count) IS NULL)
                    )
                THEN 0.0
            ELSE (cast(returns_count AS NCHAR(10)) / orders_count)
            END, 7) AS orderRatio,
    round(CASE 
            WHEN (
                    (orders_items = 0)
                    OR (returns_items IS NULL)
                    OR (orders_items IS NULL)
                    OR ((returns_items / orders_items) IS NULL)
                    )
                THEN 0.0
            ELSE (cast(returns_items AS NCHAR(10)) / orders_items)
            END, 7) AS itemsRatio,
    round(CASE 
            WHEN (
                    (orders_money = 0)
                    OR (returns_money IS NULL)
                    OR (orders_money IS NULL)
                    OR ((returns_money / orders_money) IS NULL)
                    )
                THEN 0.0
            ELSE (cast(returns_money AS NCHAR(10)) / orders_money)
            END, 7) AS monetaryRatio,
    round(CASE 
            WHEN (returns_count IS NULL)
                THEN 0.0
            ELSE returns_count
            END, 0) AS frequency
FROM (
    SELECT ss_customer_sk,
        -- return order ratio
        COUNT(DISTINCT (ss_ticket_number)) AS orders_count,
        -- return ss_item_sk ratio
        COUNT(ss_item_sk) AS orders_items,
        -- return monetary amount ratio
        SUM(ss_net_paid) AS orders_money
    FROM store_sales s
    GROUP BY ss_customer_sk
    ) orders
LEFT OUTER JOIN (
    SELECT sr_customer_sk,
        -- return order ratio
        count(DISTINCT (sr_ticket_number)) AS returns_count,
        -- return ss_item_sk ratio
        COUNT(sr_item_sk) AS returns_items,
        -- return monetary amount ratio
        SUM(sr_return_amt) AS returns_money
    FROM store_returns
    GROUP BY sr_customer_sk
    ) returned ON ss_customer_sk = sr_customer_sk
 '
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
# Define the connection string

connStr <- paste("Driver=SQL Server; Server=", instance_name,
                 "; Database=", database_name,
                 "; uid=Username;pwd=Password; ",
                 sep="" )

# Input customer data that needs to be classified.
# This is the result we get from the query.
library(RODBC)

ch <- odbcDriverConnect(connStr);

customer_data <- sqlQuery(ch, input_query)

sqlDrop(ch, "customer_return_clusters")

## create clustering model
clust <- kmeans(customer_data[,2:5],4)

## create clustering output for table
customer_cluster <- data.frame(cluster=clust$cluster,customer=customer_data$customer,orderRatio=customer_data$orderRatio,
            itemsRatio=customer_data$itemsRatio,monetaryRatio=customer_data$monetaryRatio,frequency=customer_data$frequency)

## write cluster output to DB table
sqlSave(ch, customer_cluster, tablename = "customer_return_clusters")

## clean up
odbcClose(ch)
'
    , @input_data_1 = N''
    , @params = N'@instance_name nvarchar(100), @database_name nvarchar(128), @input_query nvarchar(max), @duration float OUTPUT'
    , @instance_name = @instance_name
    , @database_name = @database_name
    , @input_query = @input_query
    , @duration = @duration OUTPUT;
END;

GO
```

## <a name="perform-clustering"></a>執行叢集

現在您已建立預存程序，接下來請執行下列程式碼以執行群集。

```sql
--Empty table of the results before running the stored procedure
TRUNCATE TABLE customer_return_clusters;

--Execute the clustering
--This will load the table customer_return_clusters with cluster mappings
EXECUTE [dbo].[generate_customer_return_clusters];
```

請確認作業順利執行，而且我們已取得客戶及其叢集對應的清單。

```sql
--Select data from table customer_return_clusters
--to verify that the clustering data was loaded
SELECT TOP (5) *
FROM customer_return_clusters;
```

```result
cluster  customer  orderRatio  itemsRatio  monetaryRatio  frequency
1        29727     0           0           0              0
4        26429     0           0           0.041979       1
2        60053     0           0           0.065762       3
2        97643     0           0           0.037034       3
2        32549     0           0           0.031281       4
```

## <a name="use-the-clustering-information"></a>使用群集資訊

由於您已將群集程序儲存在資料庫中，因此它可以有效率地針對儲存在相同資料庫中的客戶資料執行群集。 每當客戶資料更新時，您都可以執行此程序，並使用更新的群集資訊。

假設您想要將促銷電子郵件傳送給叢集 0 中的客戶，這是一個非使用中的群組 (您可以在本教學課程的[第三部分](r-clustering-model-build.md#analyze-the-results)中了解這四個叢集)。 下列程式碼會選取叢集 0 中客戶的電子郵件地址。

```sql
USE [tpcxbb_1gb]
--Get email addresses of customers in cluster 0 for a promotion campaign
SELECT customer.[c_email_address], customer.c_customer_sk
  FROM dbo.customer
  JOIN
  [dbo].[customer_clusters] as c
  ON c.Customer = customer.c_customer_sk
  WHERE c.cluster = 0
```

您可以變更 **c.cluster** 值，以傳回其他叢集中客戶的電子郵件地址。

## <a name="clean-up-resources"></a>清除資源

完成本教學課程後，您可以刪除 tpcxbb_1gb 資料庫。

## <a name="next-steps"></a>後續步驟

在本教學課程系列的第四部分中，您學到了如何：

* 建立一個會產生模型的預存程序
* 使用 SQL 機器學習執行群集
* 使用群集資訊

若要深入了解如何在機器學習服務中使用 R，請參閱：

* [執行簡單的 R 指令碼](quickstart-r-create-script.md)
* [R 資料結構、類型與物件](quickstart-r-data-types-and-objects.md)
* [R 函式](quickstart-r-functions.md)
