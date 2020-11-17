---
title: 設定叢集
titleSuffix: Configure a SQL Server big data cluster
description: 如何設定 SQL Server 巨量資料叢集的概觀
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: rahul.ajmera
ms.date: 08/04/2020
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b75f6946af9a13d6a8202c627d4c24a2225a51c1
ms.sourcegitcommit: 4545b502e3cae7136411fd9a7c15450315665f38
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/12/2020
ms.locfileid: "94549984"
---
# <a name="configure-a-sql-server-big-data-cluster"></a>設定 SQL Server 巨量資料叢集

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

在部署階段，您可以在 SQL Server 2019 巨量資料叢集中設定 SQL Server 主要執行個體、Apache Spark 與 Apache Hadoop 的屬性。

部署之後，巨量資料叢集不支援修改設定屬性。

## <a name="configuration-scopes"></a>設定範圍
巨量資料叢集設定有兩個範圍層級：`service` 與 `resource`。 設定的階層也會遵循這個從最高到最低的順序。 BDC 元件將會採用在最低範圍定義之設定的值。 如果未在指定範圍定義設定，其將繼承來自其較高父範圍的值。

例如，建議您定義 Spark 驅動程式將用於存放集區與 Sparkhead `resources` 中的預設核心數目。 您可以使用兩種方式執行此動作： 
- 於 `Spark` 服務範圍指定預設核心值  
- 於 `storage-0` 與 `sparkhead` 資源範圍指定預設核心值

在第一個案例中，Spark 服務 (存放集區與 Sparkhead) 的所有較低範圍資源都將「繼承」來自 Spark 服務預設值的預設核心數目。

在第二個案例中，每個資源都將使用在其各自範圍中定義的值。

如果核心的預設數目已同時在服務與資源範圍中定義，則資源範圍值將會覆寫服務範圍值，因為這是指定設定的最低「使用者設定」範圍。

如需有關設定的特定資訊，請參閱適當的文章：

如何： 
- [設定 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 的主要執行個體](configure-sql-server-master-instance.md)
- [在巨量資料叢集中設定 Apache Spark 和 Apache Hadoop](configure-spark-hdfs.md)

參考： 
- [SQL Server 主要執行個體設定屬性](reference-config-master-instance.md)
- [Apache Spark 與 Apache Hadoop (HDFS) 設定屬性](reference-config-spark-hadoop.md)
