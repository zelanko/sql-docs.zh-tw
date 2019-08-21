---
title: 什麼是存放集區？
titleSuffix: SQL Server big data clusters
description: 本文描述 SQL Server 2019 巨量資料叢集中的存放集區。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ead6c2ceeecbdfb3466bd4475978b139a0d2ddde
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652241"
---
# <a name="what-is-the-storage-pool-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>何謂存放集區 ([!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)])？

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明中[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] *SQL Server 存放集區*的角色。 下列各節描述 SQL 存放集區的架構和功能。

## <a name="storage-pool-architecture"></a>存放集區架構

存放集區包含由 Linux 上的 SQL Server、Spark 和 HDFS 組成的存放裝置節點。 SQL 巨量資料叢集中的所有存放裝置節點都是 HDFS 叢集成員。

![存放集區架構](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>職責

存放裝置節點負責：

- 透過 Spark 的資料擷取。
- HDFS 中的資料儲存 (Parquet 格式)。 HDFS 也提供資料持續性，因為 HDFS 資料會散佈到 SQL 巨量資料叢集中的所有存放裝置節點。
- 透過 HDFS 和 SQL Server 端點的資料存取。

## <a name="next-steps"></a>後續步驟

若要深入瞭解[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], 請參閱下列資源:

- [什麼是[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
- [工作坊：Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
