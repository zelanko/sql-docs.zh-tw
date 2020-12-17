---
title: Python 教學課程：部署叢集模型
titleSuffix: SQL machine learning
description: 在這個四部分教學課程系列的第四部分中，您將使用 SQL 機器學習，在 Python 中部署群集模型。
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 05/21/2020
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current'
ms.openlocfilehash: 60119db288040111668868692eb5f3c6f1ce458c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470429"
---
# <a name="python-tutorial-deploy-a-model-to-categorize-customers-with-sql-machine-learning"></a>Python 教學課程：使用 SQL 機器學習來部署模型以分類客戶
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
在這個四部分教學課程系列的第四部分中，您要使用 SQL Server 機器學習服務或在巨量資料叢集中，將以 Python 開發的群集模型部署到資料庫。
::: moniker-end
::: moniker range="=sql-server-2017"
在這個四部分教學課程系列的第四部分中，您要使用 SQL Server 機器學習服務，將以 Python 開發的群集模型部署到資料庫。
::: moniker-end
::: moniker range="=azuresqldb-mi-current"
在這個四部分教學課程系列的第四部分中，您要使用 Azure SQL 受控執行個體機器學習服務，將以 Python 開發的群集模型部署到資料庫。
::: moniker-end

為了定期執行群集，當新客戶註冊時，您必須能夠從任何應用程式呼叫 Python 指令碼。 若要這麼做，您可以將 Python 指令碼放在 SQL 預存程序內，以在資料庫中部署 Python 指令碼。 因為您的模型是在資料庫中執行，所以可以輕鬆地針對儲存在資料庫中的資料進行定型。

在本節中，您會將剛才撰寫的 Python 程式碼移至伺服器，並部署叢集。

在本文中，您將學會如何：

> [!div class="checklist"]
> * 建立一個會產生模型的預存程序
> * 在伺服器上執行群集
> * 使用群集資訊

在[第一部分](python-clustering-model.md)中，您已安裝必要條件並還原範例資料庫。

在[第二部分](python-clustering-model-prepare-data.md)，您已了解如何準備資料庫中的資料，以執行叢集。

在[第三部分](python-clustering-model-build.md)中，您已了解如何在 Python 中建立和定型 K-Means 群集模型。

## <a name="prerequisites"></a>Prerequisites

* 本教學課程系列的第四部分假設您已滿足 [**第一部分**](python-clustering-model.md)的必要條件，並已完成 [**第二部分**](python-clustering-model-prepare-data.md)和 [**第三部分**](python-clustering-model-build.md)中的步驟。

## <a name="create-a-stored-procedure-that-generates-the-model"></a>建立一個會產生模型的預存程序

執行下列 T-SQL 指令碼來建立預存程序。 此程序會重新建立您在本教學課程系列的第一部分和第二部分中所開發的步驟：

* 根據客戶的購買和退貨記錄來分類客戶
* 使用 K-Means 演算法產生客戶的四個叢集

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

## <a name="perform-clustering"></a>執行叢集

現在您已建立預存程序，請執行下列指令碼，以使用程序執行群集。

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

## <a name="use-the-clustering-information"></a>使用群集資訊

由於您已將群集程序儲存在資料庫中，因此它可以有效率地針對儲存在相同資料庫中的客戶資料執行群集。 每當客戶資料更新時，您都可以執行此程序，並使用更新的群集資訊。

假設您想要將促銷電子郵件傳送給叢集 0 中的客戶，這是一個非使用中的群組 (您可以在本教學課程的[第三部分](python-clustering-model-build.md#analyze-the-results)中了解這四個叢集)。 下列程式碼會選取叢集 0 中客戶的電子郵件地址。

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

您可以變更 **c.cluster** 值，以傳回其他叢集中客戶的電子郵件地址。

## <a name="clean-up-resources"></a>清除資源

完成本教學課程後，您可以刪除 tpcxbb_1gb 資料庫。

## <a name="next-steps"></a>後續步驟

在本教學課程系列的第四部分中，您已完成下列步驟：

* 建立一個會產生模型的預存程序
* 在伺服器上執行群集
* 使用群集資訊

若要深入了解如何在 SQL 機器學習中使用 Python，請參閱：

* [快速入門：建立並執行簡單的 Python 指令碼](quickstart-python-create-script.md)
* [其他 SQL 機器學習的 Python 教學課程](python-tutorials.md)
* [使用 sqlmlutils 安裝 Python 套件](../package-management/install-additional-python-packages-on-sql-server.md)