---
title: 什麼是存放集區？
titleSuffix: SQL Server big data clusters
description: 了解 SQL Server 2019 巨量資料叢集中 SQL Server 存放集區的角色，以及 SQL 存放集區的架構與功能。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 10/01/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4d810220e0bd1148d4f572638c3ac67d4c3b44c0
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257238"
---
# <a name="what-is-the-storage-pool-big-data-clusters-2019"></a>什麼是存放集區 ([!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)])？

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

此文章說明 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 中的「SQL Server 存放集區」角色。 下列各節描述 SQL 存放集區的架構和功能。

## <a name="storage-pool-architecture"></a>存放集區架構

存放集區是 SQL Server BDC 生態系統中的本機 HDFS (Hadoop) 叢集。 其提供非結構化與半結構化資料的永續性儲存體。 資料檔案 (例如 Parquet 或分隔的文字) 可以儲存在存放集區中。 為讓儲存體變成永續性，集區中的每個 Pod 都有附加的永久性磁碟區。 存放集區檔案可以透過 SQL Server 使用 [PolyBase](../relational-databases/polybase/polybase-guide.md) 或直接使用 Apache Knox Gateway 來存取。

傳統 HDFS 設定是由一組已附加存放裝置的商用硬體電腦所組成。 資料會分散在各個節點的區塊中，以供容錯及平行處理用途使用。 叢集中的其中一個節點會當作名稱節點使用，並包含有關資料節點中檔案的中繼資料資訊。

![傳統 HDFS 設定](media/concept-storage-pool/classic-hdfs-setup.png)

存放集區是由屬於 HDFS 叢集成員的儲存體節點所組成。 其會使用裝載下列容器的每個 Pod 來執行一或多個 Kubernetes Pod：

- 連結至永久性磁碟區 (儲存體) 的 Hadoop 容器。 此類型的所有容器會共同形成 Hadoop 叢集。 在 Hadoop 容器內是一個 YARN 節點管理員處理序，可以建立隨選 Apache Spark 背景工作處理序。 Spark 前端節點會裝載 Hive 中繼存放區、Spark 歷程記錄與 YARN 作業歷程記錄容器。
- 使用 OpenRowSet 技術從 HDFS 讀取資料的 SQL Server 執行個體。
- `collectd` 用於收集計量資料。
- `fluentbit` 用於收集計量資料。

![存放集區結構](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>職責

存放裝置節點負責：

- 透過 Apache Spark 的資料擷取。
- HDFS 中的資料儲存區 (Parquet 和分隔符號文字格式)。 HDFS 也提供資料持續性，因為 HDFS 資料會散佈到 SQL BDC 中的所有存放裝置節點。
- 透過 HDFS 和 SQL Server 端點的資料存取。

## <a name="accessing-data"></a>存取資料

存取存放集區中資料的主要方法如下：

- Spark 作業。
- SQL Server 外部資料表允許使用 PolyBase 計算節點與在 HDFS 節點中執行的 SQL Server 執行個體來查詢資料的使用率。

您也可以使用下列項目來與 HDFS 互動：

- Azure Data Studio。
- [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)].
- kubectl 以向 Hadoop 容器發出命令。
- HDFS http 閘道。

## <a name="next-steps"></a>後續步驟

若要深入了解 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]，請參閱下列資源：

- [什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
- [工作坊：Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters) \(英文\)
