---
title: 使用 Jupyter 筆記本和 Azure Data Studio 來收集和分析記錄
titleSuffix: SQL Server Big Data Clusters
description: 使用 Jupyter 筆記本和 Azure Data Studio 在 SQL Server 2019 巨量資料叢集上記錄叢集。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 09/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5efb20db2b0f5e3d3509715a8711ce32414fa9ee
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378371"
---
# <a name="gathering-and-analyzing-logs-in-the-cluster-with-notebooks"></a>使用筆記本收集和分析叢集中的記錄

此頁面是適用於 SQL Server 巨量資料叢集的筆記本索引。 這些可執行的筆記本 (.ipynb) 是針對 SQL Server 2019 所設計的，可協助記錄巨量資料叢集。

每個筆記本都設計為會檢查自己的相依性。 [執行所有資料格] 不是會順利完成，就是會引發例外狀況，並提供可供前往另一個筆記本的超連結提示以便解決遺失的相依性。 請遵循後續筆記本的提示超連結，按下 [執行所有資料格]，並在成功時返回原始筆記本，然後 [執行所有資料格]。

所有相依性都安裝好之後，若 [執行所有資料格] 失敗，則每個筆記本都會分析結果，並在可能的情況下，產生可供前往另一個筆記本的超連結提示，以進一步協助解決此問題。

## <a name="gathering-logs-from-big-data-cluster-bdc"></a>從巨量資料叢集 (BDC) 收集記錄

本節包含一組筆記本，可用來從 SQL Server 巨量資料叢集 (BDC) 取得記錄。

| Name | 描述 |
|--|--|
| TSG001 - 執行 azdata copy-logs | 使用 azdata 命令列介面來複製 BDC 叢集中的資料。 |
| TSG061 - 取得 BDC 命名空間中 Pod 的所有容器記錄結尾 | 從命名空間中的 BDC 叢集取得 Pod 的所有容器記錄。 |
| TSG062 - 取得 BDC 命名空間中 Pod 的所有先前容器記錄結尾 | 從命名空間中的 BDC 叢集取得 Pod 的所有先前容器記錄。 |
| TSG083 - 執行 kubectl 叢集資訊傾印 | 使用 kubetl 命令列介面來傾印 BDC 叢集相關資訊。 |
| TSG084 - 內部查詢處理器錯誤 | 使用 DMV 查詢來取得有關內部查詢處理器錯誤的詳細資訊。 |
| TSG091 - 取得 azdata CLI 記錄 | 取得本機電腦的 azdata 記錄。 |



## <a name="analyse-logs-from-big-data-clusters-bdc"></a>分析來自巨量資料叢集 (BDC) 的記錄

一組用來收集和分析 SQL Server 巨量資料叢集記錄檔的筆記本。  針對記錄中找到的已知問題，分析流程會建議執行後續筆記本。

|Name|描述 |
|---|---|
|TSG030 - SQL Server 錯誤記錄檔|取得 SQL Server 的錯誤記錄檔，並分析記錄項目，然後建議進一步的相關疑難排解指南。 |
|TSG031 - SQL Server PolyBase 記錄|取得 SQL Server PolyBase 記錄，並分析記錄項目，然後建議進一步的相關疑難排解指南。|
|TSG034 - Livy 記錄|取得 Livy 記錄，並分析記錄項目，然後建議進一步的相關疑難排解指南。|
|TSG035 - Spark 歷程記錄|取得 Spark 歷程記錄，並分析記錄項目，然後建議進一步的相關疑難排解指南。|
|TSG036 - 控制器記錄|取得控制器記錄的最後 'n' 個小時並分析記錄項目，然後建議進一步的相關疑難排解指南。|
|TSG046 - Knox 閘道記錄|Knox 會向用戶端發出 500 錯誤，並移除指向基礎問題原因的詳細資料 (堆疊)。 因此，請使用此筆記本從叢集取得 Knox 記錄。 取得 Knox 閘道記錄，並分析記錄項目，然後建議進一步的相關疑難排解指南。|
|TSG073 - InfluxDB 記錄|取得 InfluxDB 記錄，並分析記錄項目，然後建議進一步的相關疑難排解指南。|
|TSG076 - 彈性搜尋記錄|取得彈性搜尋記錄，並分析記錄項目，然後建議進一步的相關疑難排解指南。|
|TSG077 - Kibana 記錄|取得 Kibana 記錄，並分析記錄項目，然後建議進一步的相關疑難排解指南。|
|TSG088 - Hadoop datanode 記錄|取得 Hadoop datanode 記錄，並分析記錄項目，然後建議進一步的相關疑難排解指南。|
|TSG090 - Yarn nodemanager 記錄|取得 Yarn nodemanager 記錄，並分析記錄項目，然後建議進一步的相關疑難排解指南。|
|TSG092 - BDC 中所有容器的 Supervisord 記錄結尾|取得 BDC 中所有容器的 Supervisord 記錄結尾並分析記錄項目，然後建議進一步的相關疑難排解指南。|
|TSG093 - BDC 中所有容器的代理程式記錄結尾|取得 BDC 中所有容器的代理程式記錄結尾記錄並分析記錄項目，然後建議進一步的相關疑難排解指南。|
|TSG094 - Grafana 記錄|取得 Grafana 記錄，並分析記錄項目，然後建議進一步的相關疑難排解指南。|
|TSG095 - Hadoop namenode 記錄|取得 Hadoop namenode 記錄，並分析記錄項目，然後建議進一步的相關疑難排解指南。|
|TSG096 - Zookeeper 記錄|取得 Zookeeper 記錄，並分析記錄項目，然後建議進一步的相關疑難排解指南。|

## <a name="next-steps"></a>後續步驟

如需 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。
