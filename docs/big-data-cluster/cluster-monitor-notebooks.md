---
title: 使用 Jupyter 筆記本和 Azure Data Studio 監視叢集
titleSuffix: SQL Server Big Data Clusters
description: 使用 Jupyter 筆記本和 Azure Data Studio 在 SQL Server 2019 巨量資料叢集上監視叢集。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 10/01/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 516b1bb461e5927ff52f0cee79e48d9945e6da21
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378384"
---
# <a name="monitoring-cluster-with-notebooks"></a>使用筆記本監視叢集

此頁面是適用於 SQL Server 巨量資料叢集的筆記本索引。 這些可執行的筆記本 (.ipynb) 是針對 SQL Server 2019 所設計的，可協助監視巨量資料叢集。

每個筆記本都設計為會檢查自己的相依性。 [執行所有資料格] 不是會順利完成，就是會引發例外狀況，並提供可供前往另一個筆記本的超連結提示以便解決遺失的相依性。 請遵循後續筆記本的提示超連結，按下 [執行所有資料格]，並在成功時返回原始筆記本，然後 [執行所有資料格]。

所有相依性都安裝好之後，若 [執行所有資料格] 失敗，則每個筆記本都會分析結果，並在可能的情況下，產生可供前往另一個筆記本的超連結提示，以進一步協助解決此問題。


## <a name="monitoring-kubernetes"></a>監視 Kubernetes

本節包含一組筆記本，適用於使用 `azdata` 命令列介面 (CLI) 來取得 SQL Server 巨量資料叢集的資訊和狀態。

|Name |描述 |
|---|---|---|---|
|TSG006 - 取得系統 Pod 狀態|檢視所有系統 Pod 的狀態。 |
|TSG007 - 取得 BDC Pod 狀態|檢視巨量資料叢集 Pod 狀態。|
|TSG008 - 取得版本資訊 (Kubernetes)|取得 Kubernetes cluster-info。|
|TSG009 - 取得節點 (Kubernetes)|取得 kubernetes 內容。 |
|TSG010 - 取得設定內容|使用 DMV 查詢來取得有關內部查詢處理器錯誤的詳細資訊|
|TSG015 - 檢視 BDC 服務 (Kubernetes)|取得部署在 Kubernetes 叢集中 BDC 叢集的服務狀態。 |
|TSG016 - 描述 BDC Pod|取得部署在 Kubernetes 叢集中 BDC 的 Pod 狀態。 |
|TSG020 - 描述節點 (Kubernetes)|取得 BDC 叢集的節點資訊，使用 kubectl 命令列介面。 |
|TSG021 - 取得叢集資訊 (Kubernetes)|取得 Kubernetes cluster-info。 |
|TSG022 - 取得 kubeadm 主機的外部 IP 位址|取得 kubeadm 主機的外部 IP 位址。 |
|TSG023 - 取得所有 BDC 物件 (Kubernetes)|取得系統命名空間和巨量資料叢集命名空間的所有 Kubernetes 資源摘要。 |
|TSG042 - 取得資料和記錄 PVC 的節點名稱和外部掛接|取得節點名稱裝載 Pod 以及資料和記錄外部掛接。 |
|TSG063 - 取得儲存類別 (Kubernetes)|使用此筆記本來取得 Kubernetes 儲存類別。 |
|TSG064 - 取得 BDC 永續性磁碟區宣告|顯示巨量資料叢集的永續性磁碟區宣告 (PVC)。 |
|TSG065 - 取得 BDC 秘密 (Kubernetes)|檢視巨量資料叢集祕密。 |
|TSG066 - 取得 BDC 事件 (Kubernetes)|檢視巨量資料叢集事件。|
|TSG072 - 取得永續性磁碟區 (Kubernetes)|顯示 Kubernetes 叢集的持續性磁碟區 (PV)。 持續性磁碟區是非命名空間物件。 |
|TSG081 - 取得命名空間 (Kubernetes)|取得 Kubernetes 命名空間。 |
|TSG089 - 描述 BDC 非執行中 Pod|顯示 Kubernetes 叢集的非執行中 BDC Pod。 |
|TSG097 - 取得 BDC StatefulSet (Kubernetes)|顯示 Kubernetes 叢集的 BDC statefulset。 |
|TSG098 - 取得 BDC replicaset (Kubernetes)|顯示 Kubernetes 叢集的 BDC replicaset。 |
|TSG099 - 取得 BDC daemonset (Kubernetes)|顯示 Kubernetes 叢集的 BDC daemonset。 |


## <a name="monitor-big-data-cluster-bdc"></a>監視巨量資料叢集 (BDC)

本節包含一組筆記本，適用於取得裝載 SQL Server 巨量資料叢集 (BDC) 之 Kubernetes 叢集的資訊和狀態。

|Name |描述 |
|---|---|---|---|
|TSG003 - 顯示 BDC Spark 工作階段|檢視 BDC Spark 工作階段。 |
|TSG004 - 顯示 BDC 應用程式|檢視在 BDC 叢集中啟動並執行的應用程式。|
|TSG012 - 顯示 BDC 狀態|取得 BDC 叢集不同元件的目前狀態。|
|TSG013 - 在存放集區 (HDFS) 中顯示檔案清單|取得存放集區 (HDFS) 中的檔案清單。 |
|TSG014 - 顯示 BDC 端點|取得 BDC 叢集的所有可用端點。|
|TSG017 - 顯示 BDC 設定|取得 BDC 設定。 |
|TSG033 - 顯示 BDC SQL 狀態|取得部署在 Kubernetes 叢集中 BDC 的 SQL Server 狀態。 |
|TSG049 - 顯示 BDC 控制器狀態|取得部署在 Kubernetes 叢集中 BDC 的控制器狀態。 |
|TSG068 - 顯示 BDC HDFS 狀態|取得部署在 Kubernetes 叢集中 BDC 的 HDFS 狀態。 |
|TSG069 - 顯示巨量資料叢集閘道狀態|取得部署在 Kubernetes 叢集中 BDC 的 BDC 閘道狀態。 |
|TSG070 - 查詢 SQL 主要集區| 在主要執行個體上執行 SQL 查詢。 |

## <a name="next-steps"></a>後續步驟

如需 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。
