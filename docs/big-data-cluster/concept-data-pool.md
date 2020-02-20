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
ms.openlocfilehash: 6fdcaf7e54455d40cd3bcdb8c6ec1a1ec3bf75f7
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75253135"
---
# <a name="what-are-data-pools-in-a-sql-server-big-data-cluster"></a>什麼是 SQL Server 巨量資料叢集中的資料集區？

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]中的「SQL Server 資料集區」  角色。 下列各節描述 SQL 資料集區的架構和功能。

這段 5 分鐘的影片介紹資料集區，並說明如何從資料集區查詢資料：

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Querying-Data-from-Big-Data-Cluster-Data-Pool/player?WT.mc_id=dataexposed-c9-niner]

## <a name="data-pool-architecture"></a>資料集區架構

資料集區是由一或多個 SQL Server 資料集區執行個體所組成。 SQL 資料集區執行個體為叢集提供永續性的 SQL Server 儲存體。 資料集區可用於內嵌來自 SQL 查詢或 Spark 作業的資料。 為了在大型資料集上提供更好的效能，資料集區中的資料會分散到成員 SQL 資料集區執行個體的分區。

## <a name="scale-out-data-marts"></a>向外延展資料超市

資料集區可讓您建立向外延展資料超市，其中來自多個來源的外部資料會內嵌到資料集區。 由於資料會分散到資料集區執行個體，因此可更有效率地對管理的資料進行平行查詢。

![向外延展資料超市](media/concept-data-pool/data-virtualization-improvements.png)

## <a name="next-steps"></a>後續步驟

若要深入了解 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]，請參閱下列資源：

- [什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
- [工作坊：Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters) \(英文\)
