---
title: 使用 Jupyter 筆記本和 Azure Data Studio 處理巨量資料叢集 (BDC) 的常見案例
titleSuffix: SQL Server Big Data Clusters
description: 在 SQL Server 2019 巨量資料叢集上使用 Jupyter 筆記本和 Azure Data Studio 來處理 BDC 的常見案例。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 09/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 99e62be597e4ce08d38db199116f1bd4d5ab33f6
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378375"
---
# <a name="common-notebooks-for-sql-server-big-data-clusters"></a>SQL Server 巨量資料叢集的常見筆記本

本文列出 SQL Server 巨量資料叢集的筆記本。 可執行的筆記本 (.ipynb) 是針對 SQL Server 2019 而設計的，可協助您顯示巨量資料叢集上的常見案例。

每個筆記本都設計為會檢查自己的相依性。 [執行所有資料格] 選項不是順利完成，就是引發了例外狀況，並提供可供前往另一個筆記本的超連結 *提示* 以便解決遺失的相依性。 請遵循後續筆記本的提示超連結，按下 [執行所有資料格]，並在成功時返回原始筆記本，然後 [執行所有資料格]。

所有相依性都安裝好之後，若 [執行所有資料格] 失敗，則每個筆記本都會分析結果，並在可能的情況下，產生可供前往另一個筆記本的超連結提示，以進一步協助解決此問題。

## <a name="gathering-logs-from-big-data-cluster-bdc"></a>從巨量資料叢集 (BDC) 收集記錄

本節中的筆記本可作為其他筆記本的必要條件，例如登入和登出叢集。

|Name |描述 |
|---|---|
|SOP005 - az login|使用 az 命令列介面登入 Azure。 |
|SOP006 - az logout|使用 az 命令列介面登出 Azure。|
|SOP007 - 版本資訊 (azdata、bdc、kubernetes)|定義筆記本中所用關於版本設定資訊的 helper 函式。|
|SOP011 - 設定 kubernetes 設定內容|設定要使用的 kubernetes 設定。 |
|SOP028 - azdata login|使用 azdata 命令列介面來登入巨量資料叢集。 |
|SOP033 - azdata logout|使用 azdata 命令列介面來登出巨量資料叢集。 |
|SOP034 - 等候 BDC 狀況良好|會封鎖到巨量資料叢集變成狀況良好，或指定的逾時時間到期。min_pod_count 參數指出，要等到叢集中至少存在此數目的 Pod 時，才會通過健康情況檢查。 如果有任何超出此限制的現有 Pod 狀況不良，則叢集會狀況不良。|
|OPR001 - 建立應用程式部署|使用此筆記本在巨量資料叢集中建立應用程式。 |
|OPR002 - 執行應用程式部署|使用此筆記本在巨量資料叢集中執行應用程式。 |
|OPR003 - 建立 cronjob|使用此筆記本在巨量資料叢集中建立 cronjob。 |
|OPR004 - 暫停 cronjob|使用此筆記本在巨量資料叢集中暫停 cronjob。 |
|OPR005 - 繼續 cronjob|使用此筆記本在巨量資料叢集中繼續 cronjob。 |
|OPR006 - 刪除 cronjob|使用此筆記本在巨量資料叢集中刪除 cronjob。 |
|OPR007 - 刪除應用程式部署|使用此筆記本在巨量資料叢集中刪除應用程式。 |
|OPR100 - 部署及排程筆記本|使用此筆記本，將筆記本清單部署到應用程式部署 Pod、使用 Kubernetes CronJob 依排程執行應用程式部署，並安裝 Grafana 儀表板來檢視結果。|
|OPR600 - 監視基礎結構 (Kubernetes)|使用此筆記本來監視基礎結構。|
|OPR700 - 為應用程式部署應用程式建立 Grafana 儀表板|使用此筆記本在 Grafana 中建立儀表板，以監視應用程式部署結果，並在 Canary 或應用程式啟動失敗時產生警示。|
|OPR900 - 針對執行應用程式部署進行疑難排解|使用此筆記本在容器中直接執行應用程式部署指令碼 (使用 kubectl exec)。 這可提供更多的偵錯資訊來針對問題 (特別是關於指令碼啟動階段中的問題) 進行疑難排解。|
|OPR901 - 針對 cronjob 進行疑難排解|使用此筆記本在容器中直接執行 cronjob 指令碼 (使用 kubectl exec)。 這可提供更多偵錯資訊來針對問題進行疑難排解。|


## <a name="analyze-logs-from-big-data-clusters-bdc"></a>分析來自巨量資料叢集 (BDC) 的記錄

一組示範 SQL Server 巨量資料叢集案例的範例筆記本。

|Name |描述 |
|---|---|
|SAM001a - 從 SQL Server 主要集區查詢存放集區 (1/3) - 載入範例資料|在這個有 3 個部分的教學課程中，使用 azdata 將資料載入到存放集區 (HDFS)、將資料轉換為 Parquet (使用 Spark)，然後在第 3 個部分中，使用主要集區 (SQL Server) 查詢資料。 |
|SAM001b - 從 SQL Server 主要集區查詢存放集區 (2/3) - 將資料轉換為 parquet|在 3 部分教學課程的第 2 部分中，使用 Spark 將 .csv 檔案轉換成 parquet 檔案。|
|SAM001c - 從 SQL Server 主要集區查詢存放集區 (3/3) - 從 SQL Server 查詢 HDFS|在「存放集區」教學課程的第 3 部分中，您將了解如何建立指向巨量資料叢集中 HDFS 資料的外部資料表，並將此資料與主要執行個體中的高價值資料聯結。|
|SAM002 - 存放集區 (2/2) - 查詢 HDFS|在「存放集區」教學課程的第 2 部分中，您將了解如何建立指向巨量資料叢集中 HDFS 資料的外部資料表，並將此資料與主要執行個體中的高價值資料聯結|
|SAM003 - 資料集區範例|在本教學課程中，您將了解如何在資料集區中建立資料集區來源和外部資料表，然後在資料集區資料表中插入資料，並將資料從一個資料集區資料表載入到另一個。 將資料集區資料表中的資料與其他資料集區資料表聯結，同時截斷資料表和清除。 |
|SAM004 - 虛擬化 MongoDB 的資料|若要查詢來自 MongoDB 外部資料來源的資料，您必須建立外部資料表來參考該外部資料。 本節提供建立這些外部資料表的範例程式碼。|
|SAM005 - 虛擬化 Oracle 的資料|若要查詢來自 Oracle 外部資料來源的資料，您必須建立外部資料表來參考該外部資料。 本節提供建立這些外部資料表的範例程式碼。|
|SAM006 - 虛擬化 SQL Server 的資料|若要以虛擬方式查詢另一個 SQL Server 資料來源的資料，您必須建立外部資料表來參考該外部資料。 本節提供建立這些外部資料表的範例程式碼。|
|SAM007 - 虛擬化 Teradata 的資料|若要查詢來自 Teradata 外部資料來源的資料，您必須建立外部資料表來參考該外部資料。 本節提供建立這些外部資料表的範例程式碼。|
|SAM008 - 使用 azdata 的 Spark|用來與 Spark 工作階段搭配運作的 Azdata 和 kubectl 命令。|
|SAM009 - 使用 azdata 的 HDFS|用來與 HDFS 搭配運作的 Azdata 和 kubectl 命令。|
|SAM010 - 使用 azdata 的應用程式|用來與應用程式部署搭配運作的 Azdata 和 kubectl 命令。 |

## <a name="next-steps"></a>後續步驟

如需 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。
