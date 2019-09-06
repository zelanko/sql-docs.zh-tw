---
title: 教學課程：準備資料以在 Python 中將客戶分類
description: 在這四部分教學課程系列的第二部分中，您將從 SQL Server 資料庫準備資料，以便使用 SQL Server Machine Learning 服務在 Python 中執行叢集。
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/30/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d91f3b9f1e3d1abe53d677d9f9058058d321d985
ms.sourcegitcommit: 26715b4dbef95d99abf2ab7198a00e6e2c550243
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2019
ms.locfileid: "70294343"
---
# <a name="tutorial-prepare-data-to-categorize-customers-in-python-with-sql-server-machine-learning-services"></a>教學課程：使用 SQL Server Machine Learning 服務準備資料，以將 Python 中的客戶分類

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在這四部分教學課程系列的第二部分中，您將使用 Python 從 SQL database 還原和準備資料。 稍後在此系列中，您將使用這項資料，以 SQL Server Machine Learning 服務來定型和部署 Python 中的叢集模型。

在本文中，您將了解如何：

> [!div class="checklist"]
> * 使用 Python 將客戶和不同的維度分開
> * 將資料從 SQL 資料庫載入 Python 資料框架

在[第一部](python-clustering-model.md)中，您已安裝必要條件並還原範例資料庫。

在[第三部分](python-clustering-model-build.md)中，您將瞭解如何在 Python 中建立和定型以 K 表示的群集模型。

在[第四部分](python-clustering-model-deploy.md)中，您將瞭解如何在 SQL 資料庫中建立預存程式，以便根據新的資料在 Python 中執行叢集。

## <a name="prerequisites"></a>必要條件

* 本教學課程的第二部分假設您已完成[**第一部分**](python-clustering-model.md)的必要條件。

## <a name="separate-customers"></a>個別客戶

若要準備叢集客戶，您必須先將客戶與下列維度分開：

* **orderRatio** = 傳回順序比率（部分或完全回傳的訂單總數與訂單總數）
* **itemsRatio** = 傳回專案比率（傳回的總專案數與購買的專案數）
* **monetaryRatio** = 退貨數量比率（傳回的總專案金額與購買的金額）
* **frequency** = 傳回頻率

在 Azure Data Studio 中開啟新的筆記本，並輸入下列腳本。

在 [連接字串] 中，視需要取代連接詳細資料。

```python
# Load packages.
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import revoscalepy as revoscale
from scipy.spatial import distance as sci_distance
from sklearn import cluster as sk_cluster

################################################################################################

## Connect to DB and select data

################################################################################################

# Connection string to connect to SQL Server named instance.
conn_str = 'Driver=SQL Server;Server=localhost;Database=tpcxbb_1gb;Trusted_Connection=True;'

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

查詢的結果會使用 revoscalepy **RxSqlServerData**函數傳回至 Python。 在此過程中，您將會使用您在上一個腳本中定義的資料行資訊。

```python
data_source = revoscale.RxSqlServerData(sql_query=input_query, column_Info=column_info,
                                        connection_string=conn_str)
revoscale.RxInSqlServer(connection_string=conn_str, num_tasks=1, auto_cleanup=False)
# import data source and convert to pandas dataframe.
customer_data = pd.DataFrame(revoscale.rx_import(data_source))
```

現在會顯示資料框架的開頭，以確認它看起來是否正確。

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

* 使用 Python 將客戶和不同的維度分開
* 將資料從 SQL 資料庫載入 Python 資料框架

若要建立使用此客戶資料的機器學習模型，請遵循本教學課程系列的第三部分：

> [!div class="nextstepaction"]
> [教學課程：使用 SQL Server Machine Learning 服務在 Python 中建立預測模型](python-clustering-model-build.md)
