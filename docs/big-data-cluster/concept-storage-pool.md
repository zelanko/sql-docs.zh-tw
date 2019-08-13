---
title: 什麼是存放集區？
titleSuffix: SQL Server big data clusters
description: 本文描述 SQL Server 2019 巨量資料叢集中的存放集區。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 58e6f16a088d6dc6c1fc6bd32297e7bd698acbbf
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958652"
---
# <a name="what-is-the-storage-pool-sql-server-big-data-clusters"></a>什麼是存放集區 (SQL Server 巨量資料叢集)？

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文描述 SQL Server 2019 巨量資料叢集 (預覽) 中的「SQL Server 存放集區」  角色。 下列各節描述 SQL 存放集區的架構和功能。

## <a name="storage-pool-architecture"></a>存放集區架構

存放集區包含由 Linux 上的 SQL Server、Spark 和 HDFS 組成的存放裝置節點。 SQL 巨量資料叢集中的所有存放裝置節點都是 HDFS 叢集成員。

![存放集區架構](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>職責

存放裝置節點負責：

- 透過 Spark 的資料擷取。
- HDFS 中的資料儲存 (Parquet 格式)。 HDFS 也提供資料持續性，因為 HDFS 資料會散佈到 SQL 巨量資料叢集中的所有存放裝置節點。
- 透過 HDFS 和 SQL Server 端點的資料存取。

## <a name="next-steps"></a>後續步驟

若要深入了解 SQL Server 巨量資料叢集，請參閱下列資源：

- [什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)
- [工作坊：Microsoft SQL Server 巨量資料叢集架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
