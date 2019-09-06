---
title: 教學課程：在 Python 中建立模型以將客戶分類
description: 在這四部分教學課程系列的第三部分中，您將建立一個代表以 SQL Server Machine Learning 服務在 Python 中執行叢集的 K 表示模型。
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/27/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8707d14b1e332ae6ecebf83213ed53701343bcd3
ms.sourcegitcommit: 26715b4dbef95d99abf2ab7198a00e6e2c550243
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2019
ms.locfileid: "70294403"
---
# <a name="tutorial-build-a-model-in-python-to-categorize-customers-with-sql-server-machine-learning-services"></a>教學課程：在 Python 中建立模型，以 SQL Server Machine Learning 服務將客戶分類

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在這四段式教學課程系列的第三部分中，您將在 Python 中建立以 K 表示的模型，以執行群集。 在此系列的下一個部分中，您會將此模型部署在具有 SQL Server Machine Learning 服務的 SQL database 中。

在本文中，您將了解如何：

> [!div class="checklist"]
> * 定義 K 表示演算法的群集數目
> * 執行群集
> * 分析結果

在[第一部](python-clustering-model.md)中，您已安裝必要條件並還原範例資料庫。

在[第二部分](python-clustering-model-prepare-data.md)中，您已瞭解如何準備 SQL 資料庫中的資料，以執行群集。

在[第四部分](python-clustering-model-deploy.md)中，您將瞭解如何在 SQL 資料庫中建立預存程式，以便根據新的資料在 Python 中執行叢集。

## <a name="prerequisites"></a>必要條件

* 本教學課程的第三部分假設您已完成[**第一**](python-clustering-model.md)部分的必要條件，並已完成[**第二部分**](python-clustering-model-prepare-data.md)中的步驟。

## <a name="define-the-number-of-clusters"></a>定義群集的數目

若要為您的客戶資料進行叢集化，您將使用**K 意指**群集演算法，這是群組資料最簡單且最知名的方式之一。
若要深入瞭解 K，請參閱[k-表示叢集演算法的完整指南](https://www.kdnuggets.com/2019/05/guide-k-means-clustering-algorithm.html)。

此演算法接受兩個輸入：資料本身和預先定義的數位 "*k*"，代表要產生的群集數目。
輸出為*k*個叢集，其中的輸入資料會分割在叢集之間。

K 表示的目標是將專案分組到 K 個叢集，讓相同叢集中的所有專案彼此相似，而且與其他群集中的專案不同。

若要判斷要使用之演算法的叢集數目，請在 [群組數總和] 方塊中使用已解壓縮的叢集數目來繪製。 要使用的適當群集數目是在繪圖的彎曲或「肘形」。

```python
################################################################################################
## Determine number of clusters using the Elbow method
################################################################################################

cdata = customer_data
K = range(1, 20)
KM = (sk_cluster.KMeans(n_clusters=k).fit(cdata) for k in K)
centroids = (k.cluster_centers_ for k in KM)

D_k = (sci_distance.cdist(cdata, cent, 'euclidean') for cent in centroids)
dist = (np.min(D, axis=1) for D in D_k)
avgWithinSS = [sum(d) / cdata.shape[0] for d in dist]
plt.plot(K, avgWithinSS, 'b*-')
plt.grid(True)
plt.xlabel('Number of clusters')
plt.ylabel('Average within-cluster sum of squares')
plt.title('Elbow for KMeans clustering')
plt.show()
```

![肘形圖](./media/python-tutorial-elbow-graph.png)

視圖表而定， *k = 4*看起來就是理想的嘗試值。 該*k*值會將客戶分組成四個叢集。

## <a name="perform-clustering"></a>執行群集

在下列 Python 腳本中，您將使用 sklearn 封裝中的 Kmeans 函數。

```python
################################################################################################
## Perform clustering using Kmeans
################################################################################################

# It looks like k=4 is a good number to use based on the elbow graph.
n_clusters = 4

means_cluster = sk_cluster.KMeans(n_clusters=n_clusters, random_state=111)
columns = ["orderRatio", "itemsRatio", "monetaryRatio", "frequency"]
est = means_cluster.fit(customer_data[columns])
clusters = est.labels_
customer_data['cluster'] = clusters

# Print some data about the clusters:

# For each cluster, count the members.
for c in range(n_clusters):
    cluster_members=customer_data[customer_data['cluster'] == c][:]
    print('Cluster{}(n={}):'.format(c, len(cluster_members)))
    print('-'* 17)
print(customer_data.groupby(['cluster']).mean())
```

## <a name="analyze-the-results"></a>分析結果

現在您已使用 K 來執行叢集，下一個步驟是分析結果，並查看是否可以找到任何可採取動作的資訊。

查看從上一個腳本列印的群集平均值和叢集大小。

```results
Cluster0(n=31675):
-------------------
Cluster1(n=4989):
-------------------
Cluster2(n=1):
-------------------
Cluster3(n=671):
-------------------

         customer  orderRatio  itemsRatio  monetaryRatio  frequency
cluster
0        50854.809882    0.000000    0.000000       0.000000   0.000000
1        51332.535779    0.721604    0.453365       0.307721   1.097815
2        57044.000000    1.000000    2.000000     108.719154   1.000000
3        48516.023845    0.136277    0.078346       0.044497   4.271237
```

這四個叢集表示是使用[第一部分](python-clustering-model-prepare-data.md#separate-customers)中定義的變數來提供：

* *orderRatio* = 傳回順序比率（部分或完全回傳的訂單總數與訂單總數）
* *itemsRatio* = 傳回專案比率（傳回的總專案數與購買的專案數）
* *monetaryRatio* = 退貨數量比率（傳回的總專案金額與購買的金額）
* *frequency* = 傳回頻率

使用 K 的資料採礦通常需要進一步分析結果，以及進一步瞭解每個叢集的進一步步驟，但它可以提供一些良好的潛在客戶。
以下是您可以用來解讀這些結果的幾種方式：

* 叢集0似乎是非使用中的一組客戶（所有值都是零）。
* 叢集3似乎是代表傳回行為的群組。

「叢集0」是一組明顯不活躍的客戶。 也許您可以將行銷工作的目標設為此群組，以觸發購買的相關事宜。 在下一個步驟中，您將查詢資料庫中是否有客戶在叢集0的電子郵件地址，讓您可以傳送行銷電子郵件給他們。

## <a name="clean-up-resources"></a>清除資源

如果您不打算繼續進行本教學課程，請從 SQL Server 刪除 tpcxbb_1gb 資料庫。

## <a name="next-steps"></a>後續步驟

在本教學課程系列的第三部分中，您已完成下列步驟：

* 定義 K 表示演算法的群集數目
* 執行群集
* 分析結果

若要部署您已建立的機器學習模型，請遵循本教學課程系列的第四部分：

> [!div class="nextstepaction"]
> [教學課程：使用 SQL Server Machine Learning 服務在 Python 中部署群集模型](python-clustering-model-deploy.md)