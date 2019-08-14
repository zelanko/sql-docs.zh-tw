---
title: SQL Server 容器的高可用性
description: 本文介紹 SQL Server 容器的高可用性
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: aa54849c16ea9dfb821404b553b1e9183b61d66a
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "68077483"
---
# <a name="high-availability-for-sql-server-containers"></a>SQL Server 容器的高可用性

在 Kubernetes 中以原生方式建立並管理您的 SQL Server 執行個體。

將 SQL Server 部署至由 [Kubernetes](https://kubernetes.io/) 管理的 Docker 容器。 在 Kubernetes 中，如果叢集節點失敗，則具有 SQL Server 執行個體的容器可以自動復原。 如需更強固的可用性，請在 Kubernetes 叢集上的容器中，使用 SQL Server 執行個體來設定 SQL Server Always On 可用性群組。 本文會比較這兩個解決方案。

## <a name="compare-sql-server-versions-on-kubernetes"></a>比較 Kubernetes 上的 SQL Server 版本

SQL Server 2017 提供可在 Kubernetes 上部署的 Docker 映像。 您可以使用 Kubernetes 的持續性磁碟區宣告 (PVC) 來設定映像。 Kubernetes 會監視容器中的 SQL Server 處理緒。 如果處理緒、Pod、容器或節點失敗，Kubernetes 會自動啟動另一個執行個體，並重新連線至儲存體。

SQL Server 2019 (預覽) 引進具有 Kubernetes StatefulSet 的更強固架構。 Kubernetes 會在參與 SQL Server Always On 可用性群組的容器映像中，協調 SQL Server 的執行個體。 此模式可提供改善的健康狀態監視、更快速的復原、卸載備份和讀取相應放大。  

## <a name="container-with-sql-server-instance-on-kubernetes"></a>在 Kubernetes 上具有 SQL Server 執行個體的容器

Kubernetes 1.6 和更新版本支援[儲存體類別](https://kubernetes.io/docs/concepts/storage/storage-classes/)  、[持續性磁碟區宣告](https://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims)  ，以及[Azure 磁片磁碟區類型](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk)  。 

在此設定中，Kubernetes 扮演容器協調者的角色。 

![Kubernetes SQL Server 叢集的圖表](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

在上圖中，`mssql-server` 是 [*Pod*](https://kubernetes.io/docs/concepts/workloads/pods/pod/) 中的 SQL Server 執行個體 (容器)。 [複本集](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)可確保 Pod 會在節點失敗後自動復原。 應用程式會連線至服務。 在此情況下，服務代表的負載平衡器會在 `mssql-server` 失敗後維持相同 IP 位址。

Kubernetes 會協調叢集中的資源。 裝載 SQL Server 執行個體容器的節點失敗時，會啟動具有 SQL Server 執行個體的新容器，並將其附加至相同的永續性儲存體。

SQL Server 2017 和更新版本支援 Kubernetes 上的容器。

若要在 Kubernetes 中建立容器，請參閱[在 Kubernetes 中部署 SQL Server 容器](tutorial-sql-server-containers-kubernetes.md)

## <a name="a-sql-server-always-on-availability-group-on-sql-server-containers-in-kubernetes"></a>在 Kubernetes 中 SQL Server 容器上的 SQL Server Always On 可用性群組

SQL Server 2019 支援 Kubernetes 中容器上的可用性群組。 針對可用性群組，請將 SQL Server [Kubernetes 運算子](https://coreos.com/blog/introducing-operators.html)部署至您的 Kubernetes 叢集。 運算子可協助封裝、部署及管理叢集中的 SQL Server 執行個體和可用性群組。

![Kubernetes 容器中的 AG](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

在上圖中，四個節點的 kubernetes 叢集裝載具有三個複本的可用性群組。 解決方案包含下列元件：

* Kubernetes [部署](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)  。 部署包含運算子和設定對應。 部署會描述部署可用性群組的 SQL Server 執行個體所需容器映像、軟體和指示。

* 三個節點，分別裝載 [*StatefulSet*](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)。 StatefulSet 包含 Pod。 每個 Pod 都包含：
  * 執行單一 SQL Server 執行個體的 SQL Server 容器。
  * 管理可用性群組的 `mcr.microsoft.com/mssql/ha` 監督員。

* 與可用性群組相關的兩個 [*ConfigMaps*](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/)。 ConfigMaps 提供的資訊包含：
  * 運算子的部署。
  * 可用性群組。

 * 每個 SQL Server 執行個體的持續性磁碟區，都會提供資料和記錄檔的存放區。

此外，叢集會儲存密碼、憑證、金鑰和其他敏感性資訊的[祕密](https://kubernetes.io/docs/concepts/configuration/secret/)  。

## <a name="compare-sql-server-high-availability-on-containers-with-and-without-the-availability-group"></a>比較容器 (具有和不具有可用性群組) 上的 SQL Server 高可用性

下表比較 Kubernetes (具有和不具有可用性群組) 上容器中的 SQL Server 高可用性功能：

| |具有可用性群組 | 獨立容器執行個體<br/> 不具有可用性群組
|:------|:------|:------
|自動從節點失敗復原 | 是 | 是
|自動從 Pod 失敗復原 | 是 | 是
|更快速的容錯移轉 |是 |
|從 SQL Server 執行個體失敗中自動復原 | 是 | 
|自動從資料庫健康狀態檢查失敗中復原 | 是 | 
|提供唯讀複本 | 是 |
|次要複本備份 | 是 | 
|以 StatefulSet 身分執行 | 是 | 

其中一個主要差異在於，具有可用性群組的復原 (或容錯移轉) 時間，比在容器中 SQL Server 的單一執行個體更快。 這項改善是因為 SQL Server 可用性群組會在叢集中的其他節點上保留次要複本。 在容錯移轉時會選取次要複本，並升階為主要複本。 連線至服務的應用程式會重新導向至新主要複本。

如果沒有可用性群組，當 Kubernetes 偵測到容錯移轉時會需要建立容器、將其連線至儲存體，然後連線至服務的應用程式會重新連線。 確切的容錯移轉時間取決於容錯移轉位置，以及偵測到的方式。 

一般來說，可用性群組的容錯移轉時間是以秒為單位來測量，而單一執行個體的容錯移轉時間可能最多 10 分鐘。

## <a name="next-steps"></a>後續步驟

若要在 Azure Kubernetes Service (AKS) 中部署 SQL Server 容器，請參閱這些範例：

* [在 Docker 容器中部署 SQL Server](sql-server-linux-configure-docker.md)
* [在 Kubernetes 中部署 SQL Server 容器](tutorial-sql-server-containers-kubernetes.md)
* [SQL Server 容器的 Always On 可用性群組](sql-server-ag-kubernetes.md)

