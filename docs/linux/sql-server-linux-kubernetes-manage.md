---
title: 管理 SQL Server Always On 可用性群組 Kubernetes
description: 這篇文章說明如何管理 SQL Server Always On 可用性群組在 Kubernetes 中。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 078149ff8d9c9c81ac8db95862bf685ca66fbe36
ms.sourcegitcommit: df21af652d0906ade8cc9ca3985a7ba5569f0db6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2018
ms.locfileid: "47049348"
---
# <a name="manage-sql-server-always-on-availability-group-kubernetes"></a>管理 SQL Server Always On 可用性群組 Kubernetes

若要管理 Alwayson 可用性群組在 Kubernetes 上，建立資訊清單，並將它套用到叢集。 資訊清單是`.yaml`檔案。  

這篇文章中的範例適用於所有的 Kubernetes 叢集。 這些範例中的狀況會套用針對在 Azure Kubernetes 服務叢集。

請參閱範例中的端對端部署[本教學課程](tutorial-sql-server-ag-kubernetes.md)。

## <a name="fail-over---sql-server-availability-group-on-kubernetes"></a>容錯移轉-在 Kubernetes 上的 SQL Server 可用性群組

若要容錯移轉可用性群組主要複本到不同的節點在 Kubernetes 中，使用作業。 這篇文章會識別此工作的環境變數。

下列範例資訊清單檔案的描述手動容錯移轉上的 Kubernetes 複本的可用性群組的作業工作。 複製到新的檔案範例的內容呼叫`failover.yaml`。

[failover.yaml](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/templates/failover.yaml)

若要部署作業，使用`Kubectl`。

```azurecli
kubectl apply -f failover.yaml
```

當您套用資訊清單檔案時，Kubernetes 會執行作業。 工作執行時，監督員會選出一個新的前置，並將主要複本移至 SQL Server 執行個體的領導者。

執行此作業之後，請將它刪除。 在 Kubernetes 中的工作物件仍然完成後，讓您可以檢視其狀態。 您必須手動刪除舊的作業之後您會看到其狀態。 刪除作業時，也會刪除 Kubernetes 記錄檔。 如果您沒有刪除作業，未來的容錯移轉作業將會失敗，除非您變更的作業名稱與 pod 選取器。 如需詳細資訊，請參閱 <<c0> [ 執行到完成的工作-](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/)。

## <a name="rotate-credentials"></a>替換認證

旋轉更新 SA 和主要金鑰認證。

複製[旋轉 creds.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script)在本機使用`kubectl`套用至您的叢集。

```azurecli
kubectl apply -f rotate-creds.yaml
```

## <a name="next-steps"></a>後續步驟

[存取 Kubernetes 儀表板與 Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)

[在 Kubernetes 叢集上的 SQL Server 可用性群組](sql-server-ag-kubernetes.md)