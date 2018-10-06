---
title: 什麼是 SQL Server 的巨量資料叢集存放集區？ | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 100ce09f7066a6df33d7b1daaf50db50bda4ed03
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48796039"
---
# <a name="what-is-the-sql-server-big-data-clusters-storage-pool"></a>什麼是 SQL Server 的巨量資料叢集存放集區？

本文說明所扮演的角色*SQL Server 儲存體集區*中 SQL Server 2019 預覽巨量資料叢集。 下列各節描述的架構和功能的 SQL 儲存體集區。

## <a name="storage-pool-architecture"></a>儲存體集區架構

存放集區是由節點組成 SQL Server on Linux、 Spark 和 HDFS 的儲存體所組成。 在 SQL 巨量資料叢集中的所有存放裝置節點是 HDFS 叢集的成員。

![儲存體集區架構](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>責任

儲存體節點會負責：

- 透過 Spark 的資料擷取。
- HDFS （Parquet 格式） 中的資料存放區。 HDFS 也會提供資料持續性，因為 HDFS 資料則會分散到 SQL 的巨量資料叢集中的所有儲存體節點。
- 透過 HDFS 與 SQL Server 端點的資料存取。

## <a name="next-steps"></a>後續步驟

若要深入了解 SQL Server 巨量資料叢集，請參閱下列概觀：

- [什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)
