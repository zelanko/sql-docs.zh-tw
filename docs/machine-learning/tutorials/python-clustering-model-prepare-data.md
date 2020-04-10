---
title: Python 教學課程：準備叢集資料
description: 在此教學課程系列的第二部分 (總共四個部分) 中，您將會準備 SQL 資料，使用 SQL Server 機器學習服務以 Python 執行群集。
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 12/17/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8ee19ddfa59f8f1a4a32c0adf08b8f36eef9aa1f
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116511"
---
# <a name="tutorial-prepare-data-to-categorize-customers-in-python-with-sql-server-machine-learning-services"></a>教學課程：使用 SQL Server 機器學習服務在 Python 中準備資料以分類客戶

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在這個教學課程系列的第二部分 (總共四個部分) 中，您將使用 Python 準備 SQL 資料庫的資料。 在本系列稍後，您將使用 SQL Server 機器學習服務，在 Python 中定型和部署叢集模型。

在本文中，您將學會如何：

> [!div class="checklist"]
> * 使用 Python 劃分不同維度的客戶
> * 將 SQL 資料庫的資料載入 Python 資料框架

在[第一部分](python-clustering-model.md)中，您已安裝必要條件並還原範例資料庫。

在[第三部分](python-clustering-model-build.md)，您將了解如何在 Python 中建立和定型 K-Means 叢集模型。

在[第四部分](python-clustering-model-deploy.md)，您將了解如何在 SQL 資料庫中建立預存程序，以根據新的資料在 Python 中執行叢集。

## <a name="prerequisites"></a>Prerequisites

* 本教學課程的第二部分假設您已滿足[**第一部分**](python-clustering-model.md)的必要條件。

## <a name="separate-customers"></a>劃分客戶

若要準備叢集客戶，您必須先依照下列維度來劃分客戶：

* **orderRatio** = 退貨訂單率 (部分退貨或全部退貨的訂單總數與訂單總數比較)
* **itemsRatio** = 退貨率 (退貨總數與購買項目數目比較)
* **monetaryRatio** = 退貨金額率 (退貨的貨幣金額總計與購買金額比較)
* **frequency** = 退貨頻率

在 Azure Data Studio 中開啟新的筆記本，並輸入以下指令碼。

在連接字串中，視需要取代連線詳細資料。

```python
# Load packages.
import pyodbc
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
from scipy.spatial import distance as sci_distance
from sklearn import cluster as sk_cluster

################################################################################################

## Connect to DB and select data

################################################################################################

# Connection string to connect to SQL Server named instance.
conn_str = pyodbc.connect('DRIVER={ODBC Driver 17 for SQL Server}; SERVER=localhost; DATABASE=tpcxbb_1gb; Trusted_Connection=yes')

input_query = '''SELECT
ss_customer_sk AS customer,
ROUND(COALESCE(returns_count / NULLIF(1.0*orders_count, 0), 0), 7) AS orderRatio,
ROUND(COALESCE(returns_items / NULLIF(1.0*orders_items, 0), 0), 7) AS itemsRatio,
ROUND(COALESCE(returns_money / NULLIF(1.0*orders_money, 0), 0), 7) AS monetaryRatio,
COALESCE(returns_count, 0) AS frequency
FROM
(
  SELECT
    ss_customer_sk,
    -- return order ratio
    COUNT(distinct(ss_ticket_number)) AS orders_count,
    -- return ss_item_sk ratio
    COUNT(ss_item_sk) AS orders_items,
    -- return monetary amount ratio
    SUM( ss_net_paid ) AS orders_money
  FROM store_sales s
  GROUP BY ss_customer_sk
) orders
LEFT OUTER JOIN
(
  SELECT
    sr_customer_sk,
    -- return order ratio
    count(distinct(sr_ticket_number)) as returns_count,
    -- return ss_item_sk ratio
    COUNT(sr_item_sk) as returns_items,
    -- return monetary amount ratio
    SUM( sr_return_amt ) AS returns_money
FROM store_returns
GROUP BY sr_customer_sk ) returned ON ss_customer_sk=sr_customer_sk'''


# Define the columns we wish to import.
column_info = {
    "customer": {"type": "integer"},
    "orderRatio": {"type": "integer"},
    "itemsRatio": {"type": "integer"},
    "frequency": {"type": "integer"}
}
```

## <a name="load-the-data-into-a-data-frame"></a>將資料載入資料框架

查詢的結果會使用 Pandas **read_sql** 函式傳回至 Python。 作為此流程的一部分，您將使用在先前指令碼中定義的資料行資訊。

```python
customer_data = pandas.read_sql(input_query, conn_str)
```

現在會顯示資料框架的開頭，以驗證它看起來正確。

```python
print("Data frame:", customer_data.head(n=5))
```

```results
Rows Read: 37336, Total Rows Processed: 37336, Total Chunk Time: 0.172 seconds
Data frame:     customer  orderRatio  itemsRatio  monetaryRatio  frequency
0    29727.0    0.000000    0.000000       0.000000          0
1    97643.0    0.068182    0.078176       0.037034          3
2    57247.0    0.000000    0.000000       0.000000          0
3    32549.0    0.086957    0.068657       0.031281          4
4     2040.0    0.000000    0.000000       0.000000          0
```

## <a name="clean-up-resources"></a>清除資源

如果您不打算繼續進行本教學課程，請從 SQL Server 刪除 tpcxbb_1gb 資料庫。

## <a name="next-steps"></a>後續步驟

在本教學課程系列的第二部分中，您已完成下列步驟：

* 使用 Python 劃分不同維度的客戶
* 將 SQL 資料庫的資料載入 Python 資料框架

若要建立使用此客戶資料的機器學習模型，請遵循此教學課程系列的第三部分：

> [!div class="nextstepaction"]
> [教學課程：使用 SQL Server 機器學習服務在 Python 中建立預測模型](python-clustering-model-build.md)
