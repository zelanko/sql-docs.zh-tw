---
title: 執行 Linux 之容器的 Always On 可用性群組
titleSuffix: SQL Server
description: 本文介紹 SQL Server 容器上的可用性群組
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3910c74be803b7fc63c8bf560fc637387e06ee15
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "67910472"
---
# <a name="always-on-availability-groups-for-sql-server-containers"></a>SQL Server 容器的 Always On 可用性群組

SQL Server 2019 支援 Kubernetes 叢集中容器上的可用性群組。 針對可用性群組，請將 SQL Server [Kubernetes 運算子](https://coreos.com/blog/introducing-operators.html)部署至您的 Kubernetes 叢集。 運算子可協助封裝、部署及管理叢集中的可用性群組。

![Kubernetes 容器中的 AG](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

在上圖中，四個節點的 Kubernetes 叢集裝載具有三個複本的可用性群組。 解決方案包含下列元件：

* Kubernetes「[部署](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)」  。 部署包含運算子和設定對應。 這會提供部署可用性群組之 SQL Server 執行個體所需的容器映像、軟體和指示。

* 三個節點，分別裝載 [*StatefulSet*](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)。 StatefulSet 包含 [*Pod*](https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/)。 每個 Pod 都包含：
  * 執行單一 SQL Server 執行個體的 SQL Server 容器。
  * 可用性群組代理程式。 

* 與可用性群組相關聯的兩個 [*ConfigMaps*](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/)。 ConfigMaps 提供的資訊包含：
  * 運算子的部署。
  * 可用性群組。

 * 「[永久性磁碟區](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)」  是儲存體片段。 「永久性磁碟區宣告」  (PVC) 是使用者提出的儲存體要求。 每個容器都會與資料和記錄儲存體的 PVC 建立關聯。 在 Azure Kubernetes Service (AKS) 中，您會[建立永久性磁碟區宣告](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv)，根據儲存類別自動佈建儲存體。


此外，叢集會儲存密碼、憑證、金鑰和其他敏感性資訊的「[秘密](https://kubernetes.io/docs/concepts/configuration/secret/)」  。

## <a name="deploy-the-availability-group-in-kubernetes"></a>部署 Kubernetes 中的可用性群組

若要部署 Kubernetes 中的可用性群組：

1. 建立 Kubernetes 叢集

   針對可用性群組，為 SQL Server 建立至少三個節點，再加上一個用於主要執行個體的節點。

1. 部署運算子

1. 設定儲存體

1. 部署 StatefulSet

   運算子會接聽部署 StatefulSet 的指示。 運算子會自動在三個不同的節點上建立 SQL Server 執行個體，並使用外部叢集管理員設定可用性群組。

1. 建立資料庫並將其附加至可用性群組

如需詳細步驟，請參閱 [SQL Server 容器的 Always On 可用性群組](sql-server-ag-kubernetes.md)。

## <a name="sql-server-kubernetes-operator"></a>SQL Server Kubernetes 運算子

在您部署運算子之後，運算子會註冊自訂 SQL Server 資源。 使用運算子部署此資源。  每個資源會對應至一個 SQL Server 執行個體，並包含 `sapassword` 和 `monitoring policy` 等特定屬性。 運算子會剖析資源並部署 Kubernetes StatefulSet。

StatfulSet 包含：

* mssql-server 容器

* mssql-ha-supervisor 容器

運算子、HA 監督員和 SQL Server 的程式碼會封裝成名為 `mcr.microsoft.com/mssql/ha` 的 Docker 映像。 此映像包含下列二進位檔：

* `mssql-operator`

    此程序會當做個別的 Kubernetes 部署去部署。 [Kubernetes 自訂資源](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) 會註冊為 `SqlServer` (sqlservers.mssql.microsoft.com)。 然後它會接聽在 Kubernetes 叢集中建立或更新的這類資源。 針對所有這類事件，它會建立或更新對應執行個體的 Kubernetes 資源 (例如 StatefulSet 或 `mssql-server-k8s-init-sql` 作業)。

* `mssql-server-k8s-health-agent`

    此網頁伺服器會提供 Kubernetes [活躍度探查](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/)，以便判斷 SQL Server 執行個體的健全狀況。 藉由呼叫 `sp_server_diagnostics` 並將結果與您的監視原則進行比較，來監視本機 SQL Server 執行個體的健康狀態。

* `mssql-ha-supervisor`

   維護 AG 憑證和端點。 

* `mssql-server-k8s-ag-agent`
  
    此程序會監視單一 SQL Server 執行個體上 AG 複本的健康狀態，並執行容錯移轉。

    它也會維護領導者選取結果。

* `mssql-server-k8s-init-sql`
  
    此 Kubernetes [作業](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/)會將預期狀態設定套用至 SQL Server 執行個體。 每次建立或更新 SqlServer 資源時，運算子都會建立此作業。 它可確保對應至自訂資源的目標 SQL Server 執行個體具有資源中所描述的預期設定。

    例如，如果需要下列任何設定，它會予以完成：
  * 更新 SA 密碼
  * 建立代理程式的 SQL 登入
  * 建立 DBM 端點

* `mssql-server-k8s-rotate-creds`
  
    此 Kubernetes 作業會實作輪替認證工作。 建立此作業來要求更新 SA 密碼、代理程式 SQL 登入密碼、DBM 憑證等。SA 密碼會指定為作業參數。 其他密碼則會自動產生。

* `mssql-server-k8s-failover`

   實作手動容錯移轉工作流程的 Kubernetes 作業。

### <a name="notes"></a>注意

不論 AG 設定為何，運算子一律會部署 HA 監督員。 如果 SqlServer 資源未列出任何 AG，運算子仍然會部署此容器。

運算子映像的版本與 SQL Server 映像的版本相同。

## <a name="next-steps"></a>後續步驟

> [Kubernetes 中的 SQL Server 容器](tutorial-sql-server-containers-kubernetes.md)
