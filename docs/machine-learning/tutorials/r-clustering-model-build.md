---
title: 教學課程：使用 R 建置叢集模型
titleSuffix: SQL machine learning
description: 在這個教學課程系列的第三部分 (總共四個部分) 中，您將使用 SQL 機器學習在 R 中建立一個 K-Means 模型，以執行群集。
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: cawrites
ms.author: chadam
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 5d56b3cb50c268a2af74ec4bfacebf8049a4518d
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178452"
---
# <a name="tutorial-build-a-clustering-model-in-r-with-sql-machine-learning"></a>教學課程：使用 SQL 機器學習在 R 中建置群集模型
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
在這個教學課程系列的第三部分 (總共四個部分) 中，您將在 R 中建立一個 K-Means 模型以執行群集。 在本系列的下一部分中，您將使用 SQL Server 機器學習服務在資料庫中部署此模型，或在巨量資料叢集上進行此部署。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
在這個教學課程系列的第三部分 (總共四個部分) 中，您將在 R 中建立一個 K-Means 模型以執行群集。 在本系列的下一部分中，您將使用 SQL Server 機器學習服務在資料庫中部署此模型。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
在這個教學課程系列的第三部分 (總共四個部分) 中，您將在 R 中建立一個 K-Means 模型以執行群集。 在本系列的下一部分中，您將使用 SQL Server R Services 在資料庫中部署此模型。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
在這個教學課程系列的第三部分 (總共四個部分) 中，您將在 R 中建立一個 K-Means 模型以執行群集。 在本系列的下一部分中，您將使用 Azure SQL 受控執行個體機器學習服務，在資料庫中部署此模型。
::: moniker-end

在本文中，您將學會如何：

> [!div class="checklist"]
> * 為 K-Means 演算法定義叢集數目
> * 執行叢集
> * 分析結果

在[第一部分](r-clustering-model-introduction.md)中，您已安裝必要條件並還原範例資料庫。

在[第二部分](r-clustering-model-prepare-data.md)，您已了解如何準備資料庫中的資料，以執行群集。

在[第四部分](r-clustering-model-deploy.md)中，您將了解如何在資料庫中建立預存程序，以根據新的資料在 R 中執行群集。

## <a name="prerequisites"></a>Prerequisites

* 本教學課程系列的第三部分假設您已滿足[**第一部分**](r-clustering-model-introduction.md)的必要條件，並已完成[**第二部分**](r-clustering-model-prepare-data.md)中的步驟。

## <a name="define-the-number-of-clusters"></a>定義叢集數目

若要為您的客戶資料進行叢集化，您將使用 **K-Means** 叢集演算法，這是對資料進行分組的最簡單、最廣為人知的方法之一。
您可以在 [K-means 叢集演算法的完整指南](https://www.kdnuggets.com/2019/05/guide-k-means-clustering-algorithm.html)中深入了解 K-Means。

此演算法接受兩個輸入：資料本身，以及預先定義的數字「*k*」代表要產生的叢集數目。
輸出為 *k* 個叢集，包含在叢集之間分割的輸入資料。

若要對要使用的演算法判斷其叢集數目，請使用「群組平方和」內的繪圖，並以擷取的叢集數目為依據。 要使用的適當叢集數目是在繪圖的折彎處或「肘線」處。

```r
# Determine number of clusters by using a plot of the within groups sum of squares,
# by number of clusters extracted. 
wss <- (nrow(customer_data) - 1) * sum(apply(customer_data, 2, var))
for (i in 2:20)
    wss[i] <- sum(kmeans(customer_data, centers = i)$withinss)
plot(1:20, wss, type = "b", xlab = "Number of Clusters", ylab = "Within groups sum of squares")
```

![肘線圖](./media/elbow-graph.png)

根據圖表，*k = 4* 看起來是理想的嘗試值。 *k* 值會將客戶分組成四個叢集。

## <a name="perform-clustering"></a>執行叢集

在下列 R 指令碼中，您將使用函式 **kmeans** 來執行群集。

```r
# Output table to hold the customer group mappings.
# Generate clusters using Kmeans and output key / cluster to a table
# called return_cluster

## create clustering model
clust <- kmeans(customer_data[,2:5],4)

## create clustering ouput for table
customer_cluster <- data.frame(cluster=clust$cluster,customer=customer_data$customer,orderRatio=customer_data$orderRatio,
        itemsRatio=customer_data$itemsRatio,monetaryRatio=customer_data$monetaryRatio,frequency=customer_data$frequency)

## write cluster output to DB table
sqlSave(ch, customer_cluster, tablename = "return_cluster")

# Read the customer returns cluster table from the database
customer_cluster_check <- sqlFetch(ch, "return_cluster")

head(customer_cluster_check)
```

## <a name="analyze-the-results"></a>分析結果

現在您已使用 K-Means 完成群集，下一個步驟是分析結果，並確認是否可以找到任何可採取動作的資訊。

```r
#Look at the clustering details to analyze results
clust[-1]
```

```results
$centers
   orderRatio itemsRatio monetaryRatio frequency
1 0.621835791  0.1701519    0.35510836  1.009025
2 0.074074074  0.0000000    0.05886575  2.363248
3 0.004807692  0.0000000    0.04618708  5.050481
4 0.000000000  0.0000000    0.00000000  0.000000

$totss
[1] 40191.83

$withinss
[1] 19867.791   215.714   660.784     0.000

$tot.withinss
[1] 20744.29

$betweenss
[1] 19447.54

$size
[1]  4543   702   416 31675

$iter
[1] 3

$ifault
[1] 0

```

使用[第二部分](r-clustering-model-prepare-data.md#separate-customers)中定義的變數以提供四種叢集平均值：

* *orderRatio* = 退貨訂單率 (部分退貨或全部退貨的訂單總數與訂單總數比較)
* *itemsRatio* = 退貨率 (退貨總數與購買項目數目比較)
* *monetaryRatio* = 退貨金額率 (退貨的貨幣金額總計與購買金額比較)
* *frequency* = 退貨頻率

使用 K-Means 的資料採礦經常需要進一步分析結果，並採取更多步驟，以深入了解每個叢集，但可以提供一些良好的潛在客戶。
您可以透過以下幾種方式來解譯這些結果：

* 叢集 1 (最大的叢集) 似乎是不活躍的客戶群組 (所有值皆為零)。
* 叢集 3 似乎是在退貨行為方面比較明顯的群組。

## <a name="clean-up-resources"></a>清除資源

如果您不打算繼續進行本教學課程，請刪除 tpcxbb_1gb 資料庫。

## <a name="next-steps"></a>後續步驟

在本教學課程系列的第三部分中，您學到了如何：

* 為 K-Means 演算法定義叢集數目
* 執行叢集
* 分析結果

若要部署您已建立的機器學習模型，請遵循本教學課程系列的第四部分：

> [!div class="nextstepaction"]
> [使用 SQL 機器學習在 R 中部署群集模型](r-clustering-model-deploy.md)
