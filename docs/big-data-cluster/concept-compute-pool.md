---
title: 什麼是計算集區？
titleSuffix: SQL Server big data clusters
description: 本文說明 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]中的計算集區。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 420c4705d86eb55b6b99a6cf432cb95f3b9a6694
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798242"
---
# <a name="what-are-compute-pools-in-a-sql-server-big-data-cluster"></a>什麼是 SQL Server 巨量資料叢集中的計算集區？

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文描述 SQL Server 2019 巨量資料叢集 (預覽) 中的「SQL Server 計算集區」角色。 計算集區為巨量資料叢集提供向外延展計算資源。 下列各節描述計算集區的架構和功能。

## <a name="compute-pool-architecture"></a>計算集區架構

計算集區是由在 Kubernetes 中執行的一或多個計算 Pod 所組成。 這些 Pod 的自動建立和管理是由 [SQL Server 主要執行個體](concept-master-instance.md)進行協調。 每個 Pod 會包含一組基本服務和一個 SQL Server 資料庫引擎執行個體。

## <a name="scale-out-groups"></a>向外延展群組

計算集區可以做為 PolyBase 向外延展群組，以便在不同的資料來源（例如 HDFS、Oracle、MongoDB 或 Teradata）上進行分散式查詢。 藉由使用 Kubernetes 中的計算 Pod，巨量資料叢集即可自動為 PolyBase 向外延展群組建立和設定計算 Pod。

## <a name="next-steps"></a>後續的步驟

若要深入瞭解 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]，請參閱下列資源：

- [什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
- [研討會： Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
