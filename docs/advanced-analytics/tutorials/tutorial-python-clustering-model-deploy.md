---
title: 教學課程：在 Python 中部署群集模型
description: 在這四部分教學課程系列的第四部分中, 您將使用 SQL Server Machine Learning 服務, 在 Python 中部署群集模型。
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/27/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 746629d35be93997e4cda389e284aee9bb5f8544
ms.sourcegitcommit: 3de1fb410de2515e5a00a5dbf6dd442d888713ba
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/02/2019
ms.locfileid: "70211932"
---
# <a name="tutorial-deploy-a-clustering-model-in-python-with-sql-server-machine-learning-services"></a>教學課程：使用 SQL Server Machine Learning 服務在 Python 中部署群集模型

在這四部分教學課程系列的第四部分中, 您將使用 SQL Server Machine Learning 服務, 將以 Python 開發的叢集模型部署到 SQL 資料庫。

為了定期執行叢集化, 當新客戶註冊時, 您必須能夠從任何應用程式呼叫 Python 腳本。 若要這麼做, 您可以將 python 腳本放在資料庫的 SQL 預存程式內, 以在 SQL Server 中部署 Python 腳本。 因為您的模型會在 SQL 資料庫中執行, 所以可以輕鬆地針對儲存在資料庫中的資料進行定型。

在本節中, 您會將剛才撰寫的 Python 程式碼移至 SQL Server, 並透過 SQL Server Machine Learning 服務的協助來部署叢集。

在本文中，您將了解如何：

> [!div class="checklist"]
> * 建立會產生模型的預存程式
> * 在 SQL Server 中執行叢集
> * 使用叢集資訊

在[第一部](tutorial-python-clustering-model.md)中, 您已安裝必要條件並匯入範例資料庫。

在[第二部分](tutorial-python-clustering-model-prepare-data.md)中, 您已瞭解如何準備 SQL 資料庫中的資料, 以執行群集。

在[第三部分](tutorial-python-clustering-model-build.md)中, 您已瞭解如何在 Python 中建立和定型以 K 表示的叢集模型。

## <a name="prerequisites"></a>必要條件

* 本教學課程系列的第四部分假設您已完成[**第一**](tutorial-python-clustering-model.md)部分的必要條件, 並已完成第[**二部分**](tutorial-python-clustering-model-prepare-data.md)和[**第三部分**](tutorial-python-clustering-model-build.md)中的步驟。

## <a name="create-a-stored-procedure-that-generates-the-model"></a>建立會產生模型的預存程式

執行下列 T-sql 腳本來建立預存程式。 此程式會重新建立您在本教學課程系列的第一篇和第二部分中所開發的步驟:

* 根據購買和退貨記錄來分類客戶
* 使用 K 意指演算法產生四個客戶的叢集

```sql
USE [tpcxbb_1gb]
GO

CREATE procedure [dbo].[py_generate_customer_return_clusters]
AS

BEGIN
    DECLARE

-- Input query to generate the purchase history & return metrics
     @input_query NVARCHAR(MAX) = N'
SELECT
  ss_customer_sk AS customer,
  CAST( (ROUND(COALESCE(returns_count / NULLIF(1.0*orders_count, 0), 0), 7) ) AS FLOAT) AS orderRatio,
  CAST( (ROUND(COALESCE(returns_items / NULLIF(1.0*orders_items, 0), 0), 7) ) AS FLOAT) AS itemsRatio,
  CAST( (ROUND(COALESCE(returns_money / NULLIF(1.0*orders_money, 0), 0), 7) ) AS FLOAT) AS monetaryRatio,
  CAST( (COALESCE(returns_count, 0)) AS FLOAT) AS frequency
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
    GROUP BY sr_customer_sk
  ) returned ON ss_customer_sk=sr_customer_sk
 '

EXEC sp_execute_external_script
      @language = N'Python'
    , @script = N'

import pandas as pd
from sklearn.cluster import KMeans

#get data from input query
customer_data = my_input_data

#We concluded in step 2 in the tutorial that 4 would be a good number of clusters
n_clusters = 4

#Perform clustering
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orderRatio","itemsRatio","monetaryRatio","frequency"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
    , @input_data_1 = @input_query
    , @input_data_1_name = N'my_input_data'
             with result sets (("Customer" int, "orderRatio" float,"itemsRatio" float,"monetaryRatio" float,"frequency" float,"cluster" float));
END;
GO
```

## <a name="perform-clustering-in-sql-database"></a>在 SQL Database 中執行叢集

現在您已建立預存程式, 請執行下列腳本, 以使用程式執行叢集操作。

```sql
--Create a table to store the predictions in

DROP TABLE IF EXISTS [dbo].[py_customer_clusters];
GO

CREATE TABLE [dbo].[py_customer_clusters] (
    [Customer] [bigint] NULL
  , [OrderRatio] [float] NULL
  , [itemsRatio] [float] NULL
  , [monetaryRatio] [float] NULL
  , [frequency] [float] NULL
  , [cluster] [int] NULL
  ,
    ) ON [PRIMARY]
GO

--Execute the clustering and insert results into table
INSERT INTO py_customer_clusters
EXEC [dbo].[py_generate_customer_return_clusters];

-- Select contents of the table to verify it works
SELECT * FROM py_customer_clusters;
```

## <a name="use-the-clustering-information"></a>使用叢集資訊

由於您已將叢集程式儲存在資料庫中, 因此它可以有效率地對儲存在相同資料庫中的客戶資料執行叢集。 您可以在客戶資料更新時執行此程式, 並使用更新的叢集資訊。

假設您想要將促銷電子郵件傳送給叢集0中的客戶, 也就是非使用中的群組 (您可以在本教學課程的第[三部分](tutorial-python-clustering-model-build.md#analyze-the-results)中看到這四個叢集的說明)。 下列程式碼會選取叢集0中客戶的電子郵件地址。

```sql
USE [tpcxbb_1gb]
--Get email addresses of customers in cluster 0 for a promotion campaign
SELECT customer.[c_email_address], customer.c_customer_sk
  FROM dbo.customer
  JOIN
  [dbo].[py_customer_clusters] as c
  ON c.Customer = customer.c_customer_sk
  WHERE c.cluster = 0
```

您可以變更**c. cluster**值, 以傳回其他叢集中客戶的電子郵件地址。

## <a name="clean-up-resources"></a>清除資源

當您完成本教學課程時, 您可以從 SQL Server 刪除 tpcxbb_1gb 資料庫。

## <a name="next-steps"></a>後續步驟

在本教學課程系列的第四部分中, 您已完成下列步驟:

* 建立會產生模型的預存程式
* 在 SQL Server 中執行叢集
* 使用叢集資訊

若要深入瞭解如何在 SQL Server Machine Learning 服務中使用 Python, 請參閱:

* [快速入門：在 SQL Server Machine Learning 服務上執行 "Hello world" Python 腳本](quickstart-python-run-using-t-sql.md)
* [其他適用于 SQL Server Machine Learning 服務的 Python 教學課程](sql-server-python-tutorials.md)
* [使用 sqlmlutils 安裝 Python 套件](../package-management/install-additional-python-packages-on-sql-server.md)

