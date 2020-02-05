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
ms.openlocfilehash: 688db496825af348183e195bfd4003cfcfb53d81
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "69653380"
---
# <a name="high-availability-for-sql-server-containers"></a>SQL Server 容器的高可用性

在 Kubernetes 中以原生方式建立並管理您的 SQL Server 執行個體。

將 SQL Server 部署至由 [Kubernetes](https://kubernetes.io/) 管理的 Docker 容器。 在 Kubernetes 中，如果叢集節點失敗，則具有 SQL Server 執行個體的容器可以自動復原。

SQL Server 2017 引進可在 Kubernetes 上部署的 Docker 映像。 您可以使用 Kubernetes 的持續性磁碟區宣告 (PVC) 來設定映像。 Kubernetes 會監視容器中的 SQL Server 處理緒。 如果處理緒、Pod、容器或節點失敗，Kubernetes 會自動啟動另一個執行個體，並重新連線至儲存體。

## <a name="container-with-sql-server-instance-on-kubernetes"></a>在 Kubernetes 上具有 SQL Server 執行個體的容器

Kubernetes 1.6 和更新版本支援[儲存體類別  ](https://kubernetes.io/docs/concepts/storage/storage-classes/)、[持續性磁碟區宣告  ](https://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims)，以及[Azure 磁片磁碟區類型  ](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk)。 

在此設定中，Kubernetes 扮演容器協調者的角色。 

![Kubernetes SQL Server 叢集的圖表](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

在上圖中，`mssql-server` 是 [*Pod*](https://kubernetes.io/docs/concepts/workloads/pods/pod/) 中的 SQL Server 執行個體 (容器)。 [複本集](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)可確保 Pod 會在節點失敗後自動復原。 應用程式會連線至服務。 在此情況下，服務代表的負載平衡器會在 `mssql-server` 失敗後維持相同 IP 位址。

Kubernetes 會協調叢集中的資源。 裝載 SQL Server 執行個體容器的節點失敗時，會啟動具有 SQL Server 執行個體的新容器，並將其附加至相同的永續性儲存體。

SQL Server 2017 和更新版本支援 Kubernetes 上的容器。

若要在 Kubernetes 中建立容器，請參閱[在 Kubernetes 中部署 SQL Server 容器](tutorial-sql-server-containers-kubernetes.md)

## <a name="next-steps"></a>後續步驟

若要在 Azure Kubernetes Service (AKS) 中部署 SQL Server 容器，請參閱這些範例：
* [在 Docker 容器中部署 SQL Server](sql-server-linux-configure-docker.md)
* [在 Kubernetes 中部署 SQL Server 容器](tutorial-sql-server-containers-kubernetes.md)
