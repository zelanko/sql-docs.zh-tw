---
title: 什麼是資料集區？
titleSuffix: SQL Server big data clusters
description: 本文描述 SQL Server 2019 巨量資料叢集中的資料集區。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bfd4d9d6ca24599a2297799555f53a83c6601420
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652269"
---
# <a name="what-are-data-pools-in-a-sql-server-big-data-cluster"></a>什麼是 SQL Server 巨量資料叢集中的資料集區？

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明中[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] *SQL Server 資料*集區的角色。 下列各節描述 SQL 資料集區的架構和功能。

## <a name="data-pool-architecture"></a>資料集區架構

資料集區是由一或多個 SQL Server 資料集區執行個體所組成。 SQL 資料集區執行個體為叢集提供永續性的 SQL Server 儲存體。 資料集區可用於內嵌來自 SQL 查詢或 Spark 作業的資料。 為了在大型資料集上提供更好的效能，資料集區中的資料會分散到成員 SQL 資料集區執行個體的分區。

## <a name="scale-out-data-marts"></a>向外延展資料超市

資料集區可讓您建立向外延展資料超市，其中來自多個來源的外部資料會內嵌到資料集區。 由於資料會分散到資料集區執行個體，因此可更有效率地對管理的資料進行平行查詢。

![向外延展資料超市](media/concept-data-pool/data-virtualization-improvements.png)

## <a name="next-steps"></a>後續步驟

若要深入瞭解[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], 請參閱下列資源:

- [什麼是[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
- [工作坊：Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
