---
title: Always On 可用性群組適用於執行 Linux 的容器
titleSuffix: SQL Server
description: 這篇文章介紹 SQL Server 容器上的可用性群組
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e778af484881ae26669d2bac952b568532300c93
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833033"
---
# <a name="always-on-availability-groups-for-sql-server-containers"></a>Always On 可用性群組的 SQL Server 容器

SQL Server 2019 支援可用性群組上的 Kubernetes 叢集中的容器。 針對可用性群組，部署 SQL Server [Kubernetes 運算子](https://coreos.com/blog/introducing-operators.html)到 Kubernetes 叢集。 運算子可協助封裝、 部署及管理叢集中的可用性群組。

![Kubernetes 的容器中的 AG](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

在上圖中，四個節點的 kubernetes 叢集會裝載具有三個複本的可用性群組。 解決方案包含下列元件：

* Kubernetes [*部署*](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)。 此部署包含使用運算子，以及設定對應。 這些提供容器映像、 軟體和部署可用性群組的 SQL Server 執行個體所需的指示。

* 三個節點，每個裝載[ *StatefulSet*](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)。 包含 StatefulSet [ *pod*](https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/)。 包含每個 pod:
  * SQL Server 執行的容器一個 SQL Server 執行個體。
  * 可用性群組代理程式。 

* 兩個[ *ConfigMaps* ](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/)與可用性群組相關。 ConfigMaps 提供下列資訊：
  * 運算子的部署。
  * 可用性群組。

 * [*永續性磁碟區*](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)是儲存體的片段。 A*永續性磁碟區宣告*(PVC) 是由使用者的儲存體的要求。 資料和記錄儲存體 PVC 附屬於每個容器。 Azure Kubernetes Service (AKS) 中，您[建立永續性磁碟區宣告](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv)自動儲存類別為基礎的佈建存放裝置。


此外，叢集會儲存[*祕密*](https://kubernetes.io/docs/concepts/configuration/secret/)密碼、 憑證、 金鑰和其他機密資訊。

## <a name="deploy-the-availability-group-in-kubernetes"></a>部署在 Kubernetes 中的可用性群組

若要部署在 Kubernetes 中的可用性群組：

1. 建立 Kubernetes 叢集

   可用性群組，主要 SQL Server，再加上一個節點建立至少三個節點。

1. 部署運算子

1. 設定存放裝置

1. 部署 StatefulSet

   運算子會接聽的指示來部署 StatefulSet 中。 自動建立三個不同節點上的 SQL Server 執行個體，並與外部叢集管理員中設定可用性群組。

1. 建立資料庫，並將它們連接至可用性群組

如需詳細步驟，請參閱 < [Always On 可用性群組的 SQL Server 容器](sql-server-ag-kubernetes.md)。

## <a name="sql-server-kubernetes-operator"></a>SQL Server Kubernetes 運算子

部署運算子之後，它會註冊自訂的 SQL Server 資源。 您可以使用運算子來部署此資源。  每個資源對應至 SQL Server 的執行個體，並包含特定的屬性，例如`sapassword`和`monitoring policy`。 運算子會剖析該資源，並部署 Kubernetes StatefulSet。

StatfulSet 包含：

* mssql-server container

* mssql-ha-supervisor container

運算子、 HA 監督員和 SQL Server 的程式碼封裝在 Docker 映像呼叫`mcr.microsoft.com/mssql/ha`。 此映像會包含下列二進位檔：

* `mssql-operator`

    此程序會部署為個別的 Kubernetes 部署。 它會註冊[Kubernetes 自訂資源](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/)稱為`SqlServer`(sqlservers.mssql.microsoft.com)。 然後它會接聽此類正在建立或更新的 Kubernetes 叢集中的資源。 針對每一個這類事件，它會建立或更新對應的執行個體的 Kubernetes 資源 (例如 StatefulSet 或`mssql-server-k8s-init-sql`作業)。

* `mssql-server-k8s-health-agent`

    此網頁伺服器提供的 Kubernetes[作用探查](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/)判斷 SQL Server 執行個體的健康情況。 藉由呼叫監視本機 SQL Server 執行個體的健全狀況`sp_server_diagnostics`並比較其結果與您的監視原則。

* `mssql-ha-supervisor`

   會維護 ag 憑證和端點。 

* `mssql-server-k8s-ag-agent`
  
    此程序監視單一的 SQL Server 執行個體的 AG 複本的健全狀況，並執行容錯移轉。

    它也會保留前置選擇。

* `mssql-server-k8s-init-sql`
  
    此 Kubernetes[作業](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/)期望的狀態組態適用於 SQL Server 執行個體。 每次建立或更新 sql Server 資源時，則運算子會建立作業。 它可確保目標 SQL Server 執行個體對應至自訂的資源所需的資源中所述的設定。

    例如，如果以下任何設定需要，它會完成它們：
  * 更新的 SA 密碼
  * 建立 SQL 登入的 「 代理程式
  * 會建立 DBM 端點

* `mssql-server-k8s-rotate-creds`
  
    此 Kubernetes 作業實作旋轉認證工作。 建立此作業，以要求更新的 SA 密碼、 代理程式的 SQL 登入密碼、 DBM 憑證等等。SA 密碼指定為作業參數。 有些則是自動產生。

* `mssql-server-k8s-failover`

   Kubernetes 工作實作的手動容錯移轉工作流程。

### <a name="notes"></a>注意

不論 AG 組態中，運算子將一律部署 HA 監督員。 如果 SqlServer 資源不會列出任何 AG，運算子仍然會部署到此容器。

運算子映像的版本完全相同的 SQL Server 映像的版本。

## <a name="next-steps"></a>後續步驟

> [在 Kubernetes 中的 SQL Server 容器](tutorial-sql-server-containers-kubernetes.md)
