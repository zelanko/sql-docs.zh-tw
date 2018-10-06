---
title: 什麼是 SQL 巨量資料叢集資料集區？ | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 3a75f47148ff59d58d0d0d1397ba445b064c028f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48795898"
---
# <a name="what-is-a-sql-big-data-clusters-data-pool"></a>什麼是 SQL 巨量資料叢集資料集區？

本文說明所扮演的角色*SQL Server 資料集區*中 SQL Server 2019 預覽巨量資料叢集。 下列各節描述的架構和 SQL 資料集區的功能。

## <a name="data-pool-architecture"></a>資料集區架構

資料集區是由一或多個 SQL Server 資料集區執行個體所組成。 SQL 資料集區執行個體提供永續性的 SQL Server 儲存體叢集。 資料集區用來擷取從 SQL 查詢或 Spark 作業的資料。 若要提供更佳的效能，跨大型資料集，資料集區中的資料會分散到分區成員 SQL 資料集區執行個體。

## <a name="scale-out-data-marts"></a>向外延展資料超市

資料集區啟用向外延展資料超市，其中多個來源的外部資料擷取至資料集區建立作業。 因為資料會分散到資料集區執行個體，對策劃資料執行平行查詢會更有效率。

![向外延展資料超市](media/concept-data-pool/data-virtualization-improvements.png)

## <a name="next-steps"></a>後續步驟

若要深入了解 SQL Server 巨量資料叢集，請參閱下列概觀：

- [什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)
