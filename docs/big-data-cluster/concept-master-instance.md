---
title: 什麼是主要執行個體？
titleSuffix: SQL Server big data clusters
description: 本文描述 SQL Server 2019 巨量資料叢集中的 SQL Server 主要執行個體。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 57de001599923d46139883f2f8a691f9d682abf3
ms.sourcegitcommit: ab9ddcc16fdfc245cf9a49d1e90bb1ffe3958c38
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/29/2020
ms.locfileid: "92914307"
---
# <a name="what-is-the-master-instance-in-a-sql-server-big-data-cluster"></a>什麼是 SQL Server 巨量資料叢集中的主要執行個體？

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

本文說明 SQL Server 巨量資料叢集中的「SQL Server 主要執行個體」角色。 主要執行個體是在 SQL Server 巨量資料叢集中執行的 SQL Server 執行個體，可管理連線能力、向外延展查詢、中繼資料與使用者資料庫，以及機器學習服務。

SQL Server 主要執行個體提供下列功能：

## <a name="connectivity"></a>連線能力

SQL Server 主要執行個體為叢集提供可從外部存取的 TDS 端點。 您可以將應用程式或 SQL Server 工具 (例如 Azure Data Studio 或 SQL Server Management Studio) 連線到此端點，就像其他 SQL Server 執行個體一樣。

## <a name="scale-out-query-management"></a>向外延展查詢管理

SQL Server 主要執行個體包含向外延展查詢引擎，可用來將查詢分散到[計算集區](concept-compute-pool.md)中節點上的不同 SQL Server 執行個體。 向外延展查詢引擎也可讓您透過 Transact-SQL 存取叢集中的所有 Hive 資料表，不需要進行其他設定。

## <a name="metadata-and-user-databases"></a>中繼資料和使用者資料庫

除了標準 SQL Server 系統資料庫之外，SQL 主要執行個體還包含下列項目：

- 保存 HDFS 資料表中繼資料的中繼資料資料庫。
- 資料平面分區對應。
- 可存取叢集資料平面的外部資料表詳細資料。
- 定義於使用者資料庫的 PolyBase 外部資料來源和外部資料表。

您也可以選擇將自己的使用者資料庫新增至 SQL Server 主要執行個體。

## <a name="machine-learning-services"></a>機器學習服務

SQL Server 機器學習服務是資料庫引擎的附加元件功能，可用於在 SQL Server 中執行 Java、R 和 Python 程式碼。 這項功能是以 SQL Server 擴充性架構為基礎，該架構可將外部處理序自核心引擎處理序隔離，但與預存程序、含有 R 或 Python 陳述式的 T-SQL 指令碼，或是含有 T-SQL 的 Java、R 或 Python 程式碼形式的關聯式資料完全整合。

機器學習服務是 SQL Server 巨量資料叢集的一部分，預設會用在 SQL Server 主要執行個體上。 這表示一旦在 SQL Server 主要執行個體上啟用外部指令碼執行，即可使用 sp_execute_external_script 執行 Java、R 和 Python 指令碼。

### <a name="advantages-of-machine-learning-services-in-a-big-data-cluster"></a>巨量資料叢集中的機器學習服務優點

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 讓您輕鬆地將巨量資料聯結到維度資料 (通常儲存在企業資料庫中)。 當巨量資料不只是由組織的部分單位掌控，還包含在報表、儀表板和應用程式裡時，將可大幅提升價值。 同時，資料科學家可以繼續使用 Spark/HDFS 生態系統工具，並輕鬆即時地存取 SQL Server 主要執行個體中的資料，以及可「透過」SQL Server 主要執行個體存取之外部資料來源中的資料。

藉由 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]，您可以使用企業資料湖來執行更多工作。 SQL Server 開發人員和分析師可以：

* 建置從企業資料湖取用資料的應用程式。
* 透過 Transact-SQL 查詢的所有資料去推論。
* 使用 SQL Server 工具和應用程式的現有生態系統，存取及分析企業資料。
* 透過資料虛擬化和資料超市降低資料移動需求。
* 繼續針對巨量資料案例使用 Spark。
* 使用 Spark 或 SQL Server 建置智慧型企業應用程式，透過資料湖將模型定型。
* 讓生產資料庫中的模型運作以獲得最佳效能。
* 將資料直接串流到企業資料超市，進行即時分析。
* 使用互動式分析和 BI 工具，以視覺化方式探索資料。

## <a name="next-steps"></a>後續步驟

若要深入了解 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]，請參閱下列資源：

- [什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
- [工作坊：Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters) \(英文\)
