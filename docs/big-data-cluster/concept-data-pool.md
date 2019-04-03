---
title: 資料集區有哪些？
titleSuffix: SQL Server big data clusters
description: 本文說明在 SQL Server 2019 巨量資料叢集中的資料集區。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 8345ae06280458e7fa479ad95ffa20383e429267
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860119"
---
# <a name="what-are-data-pools-in-a-sql-server-big-data-cluster"></a>在 SQL Server 的巨量資料叢集中的資料集區有哪些？

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明所扮演的角色*SQL Server 資料集區*在 SQL Server 2019 巨量資料叢集 （預覽） 中。 下列各節描述的架構和 SQL 資料集區的功能。

## <a name="data-pool-architecture"></a>資料集區架構

資料集區是由一或多個 SQL Server 資料集區執行個體所組成。 SQL 資料集區執行個體提供永續性的 SQL Server 儲存體叢集。 資料集區用來擷取從 SQL 查詢或 Spark 作業的資料。 若要提供更佳的效能，跨大型資料集，資料集區中的資料會分散到分區成員 SQL 資料集區執行個體。

## <a name="scale-out-data-marts"></a>向外延展資料超市

資料集區啟用向外延展資料超市，其中多個來源的外部資料擷取至資料集區建立作業。 因為資料會分散到資料集區執行個體，對策劃資料執行平行查詢會更有效率。

![向外延展資料超市](media/concept-data-pool/data-virtualization-improvements.png)

## <a name="next-steps"></a>後續步驟

若要深入了解 SQL Server 巨量資料叢集，請參閱下列資源：

- [什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)
- [研討會：Microsoft SQL Server 的巨量資料叢集架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
