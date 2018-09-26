---
title: 適用於 SQL Server 容器的高可用性
description: 本文將介紹適用於 SQL Server 容器的高可用性
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: 13c48bf8b5edefbfd86855197128abfd5674067e
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2018
ms.locfileid: "46714988"
---
# <a name="high-availability-for-sql-server-containers"></a>適用於 SQL Server 容器的高可用性

建立和管理 Kubernetes 中的原生的 SQL Server 執行個體。

將 SQL Server 部署到所管理的 docker 容器[Kubernetes](https://kubernetes.io/)。 在 Kubernetes 中，SQL Server 執行個體的容器可以自動在叢集節點失敗時進行復原。 更強固的可用性，請使用在容器中的 Kubernetes 叢集上的 SQL Server 執行個體來設定 SQL Server Always On 可用性群組。 本文會比較兩個方案。

## <a name="compare-sql-server-versions-on-kubernetes"></a>比較在 Kubernetes 上的 SQL Server 版本

SQL Server 2017 提供在 Kubernetes 上的 Docker 映像，可供部署。 您可以設定 Kubernetes 永續性磁碟區宣告 (PVC) 映像。 Kubernetes 會監視 SQL Server 處理序，容器中。 如果處理程序、 pod、 容器或節點失敗，Kubernetes 自動啟動另一個執行個體，並重新連接到儲存體。

SQL Server 2019 導入了更強固的 archicture 與 Kubernetes StatefulSet。 這可讓 Kubernetes 來協調 SQL Server Always On 可用性群組可以參與的容器映像中的 SQL Server 的執行個體。 這可提供改善的健全狀況監視，更快獲得復原、 卸載備份和讀取相應。  

## <a name="container-with-sql-server-instance-on-kubernetes"></a>在 Kubernetes 上的 SQL Server 執行個體的容器

Kubernetes 1.6 和更新版本可支援[*儲存類別*](http://kubernetes.io/docs/concepts/storage/storage-classes/)， [*永續性磁碟區宣告*](http://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims)，而[ *Azure 磁碟的磁碟區類型*](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk)。 

在此組態中，Kubernetes 會扮演的角色容器協調器。 

![Kubernetes SQL Server 叢集的圖表](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

在上圖中，`mssql-server`是 SQL Server 執行個體 （容器） 中[ *pod*](http://kubernetes.io/docs/concepts/workloads/pods/pod/)。 A[複本集](http://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)可確保 pod，節點失敗後自動復原。 應用程式連接至服務。 在此情況下，服務會代表裝載失敗後會保持相同的 IP 位址的負載平衡器`mssql-server`。

Kubernetes 會協調在叢集中的資源。 Pod 或裝載在容器中的 SQL Server 執行個體的節點失敗時，啟動 SQL Server 執行個體相同的 pod 中容器協調器，並將它連結至相同的永續性儲存體。

SQL Server 2017 和更新版本支援容器的 Kubernetes 上。

若要在 Kubernetes 中建立的容器，請參閱[部署 Kubernetes 中的 SQL Server 容器](tutorial-sql-server-containers-kubernetes.md)

## <a name="a-sql-server-always-on-availability-group-on-sql-server-containers-in-kubernetes"></a>SQL Server Always On 可用性群組在 Kubernetes 中的 SQL Server 容器

SQL Server 2019 支援可用性群組中針對 Kubernetes 的容器。 針對可用性群組，部署 SQL Server [Kubernetes 運算子](http://coreos.com/blog/introducing-operators.html)到 Kubernetes 叢集。 運算子可協助封裝、 部署及管理 SQL Server 執行個體和叢集中的可用性群組。

![Kubernetes 的容器中的 AG](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

在上圖中，四個節點的 kubernetes 叢集中會裝載具有三個複本的可用性群組。 解決方案包含下列元件：

* Kubernetes [*部署*](http://kubernetes.io/docs/concepts/workloads/controllers/deployment/)。 此部署包含使用運算子，以及設定對應。 這些提供容器映像、 軟體和部署可用性群組的 SQL Server 執行個體所需的指示。

* 三個節點，每個裝載[ *StatefulSet*](http://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)。 StatefulSet 包含 pod。 包含每個 pod:
  * SQL Server 執行的容器一個 SQL Server 執行個體。
  * 監督員`mcr.microsoft.com/mssql/ha`管理可用性群組。

* 兩個[ *ConfigMaps* ](http://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/)與可用性群組相關。 ConfigMaps 提供下列資訊：
  * 運算子的部署。
  * 可用性群組。

 * 針對每個 SQL Server 執行個體的永續性磁碟區會提供資料和記錄檔的儲存體。

此外，叢集會儲存[*祕密*](http://kubernetes.io/docs/concepts/configuration/secret/)密碼、 憑證、 金鑰和其他機密資訊。

## <a name="compare-sql-server-high-availabiltiy-on-containers-with-and-without-the-availability-group"></a>比較容器而不需可用性群組上的 SQL Server 高可用性

下列表格 compairs 在 Kubernetes 上的容器，而沒有可用性群組中的 SQL Server 高可用性功能：

| |使用可用性群組 | 獨立的容器執行個體<br/> 沒有可用性群組
|:------|:------|:------
|自動從節點失敗中復原 | 是 | 是
|自動從 pod 失敗中復原 | 是 | 是
|更快速的容錯移轉 |是 |
|從 SQL Server 執行個體失敗自動復原 | 是 | 
|從資料庫健全狀況檢查失敗自動復原 | 是 | 
|提供唯讀複本 | 是 |
|次要複本的備份 | 是 | 
|StatefulSet 形式執行 | 是 | 

只有一個主要差異是更快速地在容器中的 SQL Server 的單一執行個體與可用性群組的復原 （或容錯移轉） 的時間。 這是因為 SQL Server 可用性群組會保留在叢集中其他節點上的可用性群組資料庫的次要複本。 在容錯移轉，次要複本已選取，並提升為主要。 連線至服務的應用程式會重新導向至新的主要複本。 

可用性群組中，當 Kubernetes 偵測容錯移轉之後，它必須將建立容器，並將它連接至儲存體，而不重新連線至服務的應用程式。 確切的容錯移轉時間取決於其中的容錯移轉，並偵測方式。 

一般而言，可用性群組的容錯移轉時間會以秒為單位，而復原容器的單一執行個體的容錯移轉時間可能最多 10 分鐘的時間。

## <a name="next-steps"></a>後續步驟

若要部署 Azure Kubernetes Service (AKS) 中的 SQL Server 容器，請遵循這些教學課程：

* [部署 Docker 容器中的 SQL Server](sql-server-linux-configure-docker.md)
* [部署 Kubernetes 中的 SQL Server 容器](tutorial-sql-server-containers-kubernetes.md)
* [部署 SQL Server Always On 可用性群組 Kubernetes](tutorial-sql-server-ag-kubernetes.md)

