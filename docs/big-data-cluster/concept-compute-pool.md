---
title: 什麼是計算集區？
titleSuffix: SQL Server big data clusters
description: 本文描述 SQL Server 2019 巨量資料叢集中的計算集區。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 10/15/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9c3374b0820233e20ee73b85947ed2b8a61847c0
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91866812"
---
# <a name="what-are-compute-pools-sql-server-big-data-clusters"></a>SQL Server 巨量資料叢集的計算集區是什麼？

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

本文描述 SQL Server 巨量資料叢集中「SQL Server 計算集區」的角色。 計算集區為巨量資料叢集提供向外延展的計算資源。 其可用來卸載 SQL Server 主要執行個體的計算工作或中繼結果集。 以下各節會描述計算集區的架構、功能和使用案例。

您也可以觀看這段 5 分鐘的影片，以取得計算集區簡介：

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Overview-Big-Data-Cluster-Compute-Pool/player?WT.mc_id=dataexposed-c9-niner]

## <a name="compute-pool-architecture"></a>計算集區架構

計算集區是由在 Kubernetes 中執行的一或多個計算 Pod 所組成。 這些 Pod 的自動建立和管理是由 [SQL Server 主要執行個體](concept-master-instance.md)進行協調。 每個 Pod 會包含一組基本服務和一個 SQL Server 資料庫引擎執行個體。

![計算集區架構](media/concept-compute-pool/compute-pool-architecture.png)

## <a name="scale-out-groups"></a>向外延展群組

計算集區可作為 PolyBase 向外延展群組，以便在不同的外部資料來源 (例如 SQL Server、Oracle、MongoDB、Teradata 和 HDFS) 上進行分散式查詢。 使用 Kubernetes 中的計算 Pod，巨量資料叢集可將為 PolyBase 向外延展群組建立和設定計算 Pod 的流程自動化。

## <a name="compute-pool-scenarios"></a>計算集區案例

使用計算集區的案例包括：

- 提交至主要執行個體的查詢，使用[儲存體集區](concept-storage-pool.md)中的一或多個資料表時。

- 提交至主要執行個體的查詢，使用[資料集區](concept-data-pool.md)中具有循環配置資源散發的一或多個資料表時。

- 提交至主要執行個體的查詢，使用具有 SQL Server、Oracle、MongoDB 和 Teradata 外部資料來源的**資料分割**資料表時。 本案例必須啟用查詢提示 OPTION (FORCE SCALEOUTEXECUTION)。

- 提交至主要執行個體的查詢，使用 [HDFS 階層處理](hdfs-tiering.md)中的一或多個資料表時。

**不**使用計算集區的案例包括：

- 提交至主要執行個體的查詢，使用外部 Hadoop HDFS 叢集中的一或多個資料表時。

- 提交至主要執行個體的查詢，使用 Azure Blob 儲存體中的一或多個資料表時。

- 提交至主要執行個體的查詢，使用具有 SQL Server、Oracle、MongoDB 和 Teradata 外部資料來源的**非資料分割**資料表時。

- 啟用查詢提示 OPTION (DISABLE SCALEOUTEXECUTION) 時。

- 提交至主要執行個體的查詢，套用至主要執行個體的資料庫時。

## <a name="next-steps"></a>後續步驟

若要深入了解 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]，請參閱下列資源：

- [什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
- [工作坊：Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters) \(英文\)
