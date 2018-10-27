---
title: 什麼是 SQL Server 的巨量資料叢集主要執行個體嗎？ | Microsoft Docs
description: 本文說明中的 SQL Server 2019 巨量資料叢集的主要執行個體。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 7c58d925e9d52ee4496f8a324eab91bbfa7ccaad
ms.sourcegitcommit: 182d77997133a6e4ee71e7a64b4eed6609da0fba
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2018
ms.locfileid: "50051060"
---
# <a name="what-is-the-sql-server-big-data-cluster-master-instance"></a>什麼是 SQL Server 的巨量資料叢集主要執行個體嗎？

本文說明所扮演的角色*SQL Server 的主要執行個體*在 SQL Server 2019 巨量 ata 叢集中。 主要執行個體是在 SQL Server 的巨量資料叢集中執行的 SQL Server 執行個體[控制平面](big-data-cluster-overview.md#controlplane)。

SQL Server 的主要執行個體提供下列功能：

## <a name="connectivity"></a>連接性

SQL Server 的主要執行個體提供叢集的外部可存取的 TDS 端點。 您可以連接應用程式或 SQL Server 工具，例如 Azure Data Studio 或 SQL Server Management Studio 這個端點，就像任何其他 SQL Server 執行個體。

## <a name="scale-out-query-management"></a>向外延展查詢管理

SQL Server 的主要執行個體包含用來將查詢分散在節點上的 SQL Server 執行個體上的向外延展查詢引擎[計算集區](concept-compute-pool.md)。 向外延展查詢引擎也會提供所有的 Hive 資料表，而不需要任何額外的設定叢集中透過 Transact SQL 存取。 (Hive 在 CTP 2.0 中不支援的資料表)

## <a name="metadata-and-user-databases"></a>中繼資料和使用者資料庫

除了標準的 SQL Server 系統資料庫，SQL master 執行個體也包含下列內容：

- 中繼資料的資料庫保留 HDFS 資料表中繼資料
- 資料平面的分區對應
- 提供叢集中的資料平面的存取的外部資料表的詳細資料。
- PolyBase 外部資料來源和使用者資料庫中定義的外部資料表。

您也可以選擇將您自己的使用者資料庫加入至 SQL Server 的主要執行個體。

## <a name="machine-learning-services"></a>Machine learning 服務

SQL Server machine learning 服務是 database engine，用於執行 SQL Server 中的 Java、 R 和 Python 程式碼的附加元件功能。 這項功能根據 SQL Server extensibility framework、 隔離核心引擎的程序，從外部程序，但完全整合的關聯式資料當做預存程序、 T-SQL 指令碼包含 R 或 Python 的陳述式，或 Java、 R 或包含 T-SQL 的 Python 程式碼。

SQL Server 的巨量資料叢集的一部分，machine learning 服務將可在預設 SQL Serevr 主要執行個體上。 也就是說，一旦在 SQL Server 的主要執行個體上啟用外部指令碼執行時，它會就能夠執行 Java 中，使用 sp_execute_external_script 的 R 和 Python 指令碼。

### <a name="advantages-of-machine-learning-services-in-a-big-data-cluster"></a>巨量資料叢集中的機器學習服務的優點

SQL Server 2019 輕鬆加入至維度的資料通常儲存在企業資料庫中的巨量資料。 當它不只是組件，在組織的手中，但也包含在報表、 儀表板和應用程式會大幅增加的巨量資料的值。 在此同時，資料科學家可以繼續使用 Spark/HDFS 生態系統工具，並有多簡單、 即時資料的存取權可存取的外部資料來源和 SQL Server 的主要執行個體中_透過_SQL Server master執行個體。

使用 SQL Server 2019 巨量資料叢集，您可以執行多個與您的企業資料湖。 SQL Server 開發人員和分析師可以：

* 建置應用程式取用來自 enterprise data lake 的資料。
* 使用 TRANSACT-SQL 查詢所有資料的原因。
* 您可以使用現有的 SQL Server 工具和應用程式的生態系統來存取並分析企業資料。
* 減少資料虛擬化和資料超市中的資料移動。
* 繼續使用 Spark 的巨量資料案例。
* 建置智慧型的企業應用程式使用 Spark 或 SQL Server 透過 data lake 定型模型。
* 為了達到最佳效能的實際執行資料庫中的模型中運作。
* Stream 直接將企業資料超市，進行即時分析的資料。
* 瀏覽資料以視覺化方式使用互動式分析和 BI 工具。

## <a name="next-steps"></a>後續步驟

若要深入了解 SQL Server 巨量資料叢集，請參閱下列概觀：

- [什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)
