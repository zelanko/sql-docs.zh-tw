---
title: 什麼是計算集區？
titleSuffix: SQL Server big data clusters
description: 此文章說明 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]中的計算集區。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e54ee601b180e8883ec9fea49fff810c52fe5f49
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75253136"
---
# <a name="what-are-compute-pools-in-a-sql-server-big-data-cluster"></a>什麼是 SQL Server 巨量資料叢集中的計算集區？

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

此文章說明 SQL Server 巨量資料叢集中「SQL Server 計算集區」  的角色。 計算集區為巨量資料叢集提供向外延展計算資源。 下列各節描述計算集區的架構和功能。

您也可以觀看這段 5 分鐘的影片，以取得計算集區簡介：

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Overview-Big-Data-Cluster-Compute-Pool/player?WT.mc_id=dataexposed-c9-niner]


## <a name="compute-pool-architecture"></a>計算集區架構

計算集區是由在 Kubernetes 中執行的一或多個計算 Pod 所組成。 這些 Pod 的自動建立和管理是由 [SQL Server 主要執行個體](concept-master-instance.md)進行協調。 每個 Pod 會包含一組基本服務和一個 SQL Server 資料庫引擎執行個體。

## <a name="scale-out-groups"></a>向外延展群組

計算集區可作為 PolyBase 向外延展群組，以便在不同的資料來源 (例如 HDFS、Oracle、MongoDB 或 Teradata) 上進行分散式查詢。 藉由使用 Kubernetes 中的計算 Pod，巨量資料叢集即可自動為 PolyBase 向外延展群組建立和設定計算 Pod。

## <a name="next-steps"></a>後續步驟

若要深入了解 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]，請參閱下列資源：

- [什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
- [工作坊：Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters) \(英文\)
