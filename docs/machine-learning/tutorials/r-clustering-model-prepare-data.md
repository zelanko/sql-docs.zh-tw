---
title: 教學課程：準備在 R 中執行群集所需的資料
titleSuffix: SQL machine learning
description: 在這個四部分教學課程系列的第二部分中，您將準備來自資料庫的資料，以使用 SQL 機器學習在 R 中執行叢集。
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: cawrites
ms.author: chadam
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 794ef80656a23f36d7dc5bd99ddfd8f2662478bd
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178730"
---
# <a name="tutorial-prepare-data-to-perform-clustering-in-r-with-sql-machine-learning"></a>教學課程：準備資料以使用 SQL 機器學習在 R 中執行叢集
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
在這個四部分教學課程系列的第二部分中，您將準備來自資料庫中的資料，以使用 SQL Server 機器學習服務在 R 中執行叢集，或在巨量資料叢集上執行叢集。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
在這個四部分教學課程系列的第二部分中，您將準備來自資料庫的資料，以使用 SQL Server 機器學習服務在 R 中執行叢集。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
在這個四部分教學課程系列的第二部分中，您將準備來自資料庫的資料，以使用 SQL Server 2016 R Services 在 R 中執行叢集。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
在這個四部分教學課程系列的第二部分中，您將準備來自 SQL 資料庫的資料，以使用 Azure SQL 受控執行個體機器學習服務，在 R 中執行叢集。
::: moniker-end

在本文中，您將學會如何：

> [!div class="checklist"]
> * 使用 R 依不同的維度區分客戶
> * 將資料庫中的資料載入到 R 資料框架中

在[第一部分](r-clustering-model-introduction.md)中，您已安裝必要條件並還原範例資料庫。

在[第三部分](r-clustering-model-build.md)中，您將了解如何在 R 中建立和定型 K-Means 叢集模型。

在[第四部分](r-clustering-model-deploy.md)中，您將了解如何在資料庫中建立預存程序，以根據新的資料在 R 中執行群集。

## <a name="prerequisites"></a>Prerequisites

* 本教學課程的第二部分會假設您已完成[**第一部分**](r-clustering-model-introduction.md)。

## <a name="separate-customers"></a>劃分客戶

在 RStudio 中建立新的 RScript 檔案，並執行下列指令碼。
在 SQL 查詢中，您將依據下列維度來區分客戶：

* **orderRatio** = 退貨訂單率 (部分退貨或全部退貨的訂單總數與訂單總數比較)
* **itemsRatio** = 退貨率 (退貨總數與購買項目數目比較)
* **monetaryRatio** = 退貨金額率 (退貨的貨幣金額總計與購買金額比較)
* **frequency** = 退貨頻率

在 **connStr** 函數中，將 **ServerName** 取代為您自己的連線資訊。

```r
# Define the connection string to connect to the tpcxbb_1gb database

connStr <- "Driver=SQL Server;Server=ServerName;Database=tpcxbb_1gb;uid=Username;pwd=Password"

#Define the query to select data
input_query <- "
SELECT ss_customer_sk AS customer
    ,round(CASE 
            WHEN (
                       (orders_count = 0)
                    OR (returns_count IS NULL)
                    OR (orders_count IS NULL)
                    OR ((returns_count / orders_count) IS NULL)
                    )
                THEN 0.0
            ELSE (cast(returns_count AS NCHAR(10)) / orders_count)
            END, 7) AS orderRatio
    ,round(CASE 
            WHEN (
                     (orders_items = 0)
                  OR (returns_items IS NULL)
                  OR (orders_items IS NULL)
                  OR ((returns_items / orders_items) IS NULL)
                 )
            THEN 0.0
            ELSE (cast(returns_items AS NCHAR(10)) / orders_items)
            END, 7) AS itemsRatio
    ,round(CASE 
            WHEN (
                     (orders_money = 0)
                  OR (returns_money IS NULL)
                  OR (orders_money IS NULL)
                  OR ((returns_money / orders_money) IS NULL)
                 )
            THEN 0.0
            ELSE (cast(returns_money AS NCHAR(10)) / orders_money)
            END, 7) AS monetaryRatio
    ,round(CASE 
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
    ) returned ON ss_customer_sk = sr_customer_sk";
```

## <a name="load-the-data-into-a-data-frame"></a>將資料載入資料框架

現在請使用下列指令碼，將查詢的結果傳回至 R 資料框架。

```r
# Query using input_query and get the results back
# to data frame customer_data

library(RODBC)

ch <- odbcDriverConnect(connStr)

customer_data <- sqlQuery(ch, input_query)

# Take a look at the data just loaded
head(customer_data, n = 5);
```

您應該會看見如下所示的結果。

```results
  customer orderRatio itemsRatio monetaryRatio frequency
1    29727          0          0      0.000000         0
2    26429          0          0      0.041979         1
3    60053          0          0      0.065762         3
4    97643          0          0      0.037034         3
5    32549          0          0      0.031281         4
```

## <a name="clean-up-resources"></a>清除資源

如果您不打算繼續進行本教學課程，請刪除 tpcxbb_1gb 資料庫。

## <a name="next-steps"></a>後續步驟

在本教學課程系列的第二部分中，您學到了如何：

* 使用 R 依不同的維度區分客戶
* 將資料庫中的資料載入到 R 資料框架中

若要建立使用此客戶資料的機器學習模型，請遵循此教學課程系列的第三部分：

> [!div class="nextstepaction"]
> [使用 SQL 機器學習在 R 中建立預測模型](r-clustering-model-build.md)
