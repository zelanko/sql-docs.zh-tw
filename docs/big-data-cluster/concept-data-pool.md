---
title: 什麼是資料集區？
titleSuffix: SQL Server big data clusters
description: 了解 SQL Server 巨量資料叢集中 SQL Server 資料集區的角色，以及 SQL 資料集區的架構與功能。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 73fe5c5b7be90d8c351aa08b3d5fe0247ecfceb0
ms.sourcegitcommit: ab9ddcc16fdfc245cf9a49d1e90bb1ffe3958c38
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/29/2020
ms.locfileid: "92914328"
---
# <a name="what-are-data-pools-in-a-sql-server-big-data-cluster"></a>什麼是 SQL Server 巨量資料叢集中的資料集區？

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

本文說明 SQL Server 巨量資料叢集中的「SQL Server 資料集區」角色。 以下各節說明資料集區的架構、功能和使用案例。

這段 5 分鐘的影片介紹資料集區，並說明如何從資料集區查詢資料：

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Querying-Data-from-Big-Data-Cluster-Data-Pool/player?WT.mc_id=dataexposed-c9-niner]

## <a name="data-pool-architecture"></a>資料集區架構

資料集區由一或多個 SQL Server 資料集區執行個體所組成，可為叢集提供持續的 SQL Server 儲存體。 它可讓您對外部資料來源和工作卸載進行快取資料的效能查詢。 資料會使用 T-SQL 查詢或從 Spark 作業內嵌到資料集區中。 若要強化大型資料集的效能，可將內嵌的資料散發至分區，並儲存在集區中的各個 SQL Server 執行個體間。 支援的散發方法為循環配置資源和複寫。 若要將讀取存取最佳化，可在每個資料集區執行個體中的每個資料表上建立叢集資料行存放區索引。 資料集區可作為 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 的向外延展資料超市。

![向外延展資料超市](media/concept-data-pool/data-virtualization-improvements.png)

您可以從 SQL Server 主要執行個體管理對資料集區 SQL Server 執行個體的存取。 系統會建立資料集區的外部資料來源，以及用來儲存資料快取的 PolyBase 外部資料表。 在背景中，控制器會使用符合外部資料表的資料表，在資料集區中建立資料庫。 在 SQL Server 主要執行個體中，工作流程是透明的；控制器會將特定外部資料表要求重新導向至資料集區的 SQL Server 執行個體 (可能透過計算集區)，並執行查詢，然後傳回結果集。 資料集區中的資料只能內嵌或查詢，且無法修改。 因此，進行任何資料重新整理時，都需要先卸除資料表，然後再依序重新建立資料表及重新填入資料。

## <a name="data-pool-scenarios"></a>資料集區案例

 報告用途是常見的資料集區案例。 例如，聯結多個 PolyBase 資料來源的複雜查詢 (用於每週報表)，可能會卸載至資料集區。 快取的資料可直接在本機快速計算，而無須回到原始資料集。 同樣地，也可以在資料集區中快取需要定期重新整理的儀表板資料，以達到最理想的報告效能。 機器學習重複探索也可以受益於資料集區中的資料集快取。

## <a name="next-steps"></a>後續步驟

若要深入了解 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]，請參閱下列資源：

- [什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
- [工作坊：Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters) \(英文\)
