---
title: 部署 SQL Server Always On 可用性群組上的 Kubernetes 叢集
description: 這篇文章說明 SQL Server Kubernetes Always On 可用性群組運算子全球需求的參數
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
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4d24cd2ab59e1a7959f5a8ac1c929ff2e5e8e54a
ms.sourcegitcommit: df21af652d0906ade8cc9ca3985a7ba5569f0db6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2018
ms.locfileid: "47049598"
---
# <a name="deploy-a-sql-server-always-on-availability-group-on-kubernetes-cluster"></a>部署 SQL Server Always On 可用性群組上的 Kubernetes 叢集

## <a name="requirements"></a>需求

- Kubernetes 叢集
- Kubernetes 版本 1.11.0 或更高版本
- 四個或多個節點
- [kubectl](http://kubernetes.io/docs/tasks/tools/install-kubectl/)。

  >[!NOTE]
  >您可以使用任何類型的 Kubernetes 叢集。 若要在 Azure Kubernetes Service (AKS) 建立 Kubernetes 叢集，請參閱[建立 AKS 叢集](http://docs.microsoft.com/azure/aks/create-cluster.md)。
  > 下列指令碼會在 Azure 中建立四個節點的 Kubernetes 叢集。
  >```azure-cli
  az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 4 --kubernetes-version 1.11.1
  >```

## <a name="steps"></a>步驟

1. 設定儲存體

  在類似 Azure 雲端環境中，設定[永續性磁碟區](http://kubernetes.io/docs/concepts/storage/persistent-volumes/)的每個 SQL Server 執行個體。

  若要在 Azure 中建立永續性磁碟區，請參閱`pv.yaml`並`pvc.yaml`中[sql server 範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/templates)。

  若要建立的儲存體，執行下列命令：

  ```azurecli
  kubectl apply -f <pv.yaml>
  ```

1. 建立 Kubernetes 祕密的 SA 密碼和主要金鑰。

  下列範例會建立兩個密碼。 `sapassword` 為 SA 密碼和`masterkeypassword`是主要金鑰。 執行此指令碼取代之前`<MyC0mp13xP@55w04d!>`使用不同的複雜密碼，每個密碼。

   ```azurecli
   kubectl create secret generic sql-secrets --from-literal='sapassword=<MyC0mp13xP@55w04d!>' --from-literal='masterkeypassword=<MyC0mp13xP@55w04d!>'
   ```

1. 設定及部署 SQL Server 的操作員資訊清單。

  複製 SQL Server 運算子`operator.yaml`從檔案[sql server 範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)。

  `operator.yaml`檔案是部署 manifiest Kubernetes 運算子。

  若要設定資訊清單，請更新`operator.yaml`您環境的檔案。

  適用於 Kubernetes 叢集資訊清單。

  ```azurecli
  kubectl apply -f operator.yaml
  ```

1. 部署 SQL Server 自訂資源。

  複製 SQL Server 的資訊清單`sqlserver.yaml`從[sql server 範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)。

  適用於 Kubernetes 叢集資訊清單。

  ```azurecli
  kubectl apply -f sqlserver.yaml
  ```

部署 SQL Server 的資訊清單之後，運算子會將 SQL Server 執行個體部署為容器中的 pod。

指令碼完成之後，Kubernetes 運算子會建立儲存體、 SQL Server 執行個體、 負載平衡器服務。 您可以監視與部署[Kubernetes 儀表板](http://docs.microsoft.com/azure/aks/kubernetes-dashboard)。

Kubernetes 會建立後的 SQL Server 容器將會完成下列步驟來將資料庫加入可用性群組：

1. [連接](sql-server-linux-kubernetes-connect.md)叢集中的 SQL Server 執行個體。

1. 建立資料庫。

1. 進行完整備份的資料庫，以便啟動記錄鏈結。

1. 您可以將資料庫加入可用性群組。

使用自動植入讓 SQL Server 會自動建立次要複本建立可用性群組。

## <a name="next-steps"></a>後續步驟

[連接到 Kubernetes 叢集上的 SQL Server 可用性群組](sql-server-linux-kubernetes-connect.md)

[管理 Kubernetes 叢集上的 SQL Server 可用性群組](sql-server-linux-kubernetes-manage.md)

[在 Kubernetes 叢集上的 SQL Server 可用性群組](sql-server-ag-kubernetes.md)