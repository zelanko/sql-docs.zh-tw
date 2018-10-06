---
title: 部署 SQL Server Always On 可用性群組上的 Kubernetes 叢集
description: 這篇文章說明 SQL Server Kubernetes Always On 可用性群組運算子全球需求的參數
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 10/02/2018
ms.topic: article
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 776b4390c78a6bd228989b94dd76d4a269f94126
ms.sourcegitcommit: 8aecafdaaee615b4cd0a9889f5721b1c7b13e160
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2018
ms.locfileid: "48818056"
---
# <a name="deploy-a-sql-server-always-on-availability-group-on-kubernetes-cluster"></a>部署 SQL Server Always On 可用性群組上的 Kubernetes 叢集

這篇文章中的範例會部署 SQL Server Always On 可用性群組與三個複本的 Kubernetes 叢集。 次要複本皆處於同步認可模式。

在 Kubernetes 上部署包含 SQL Server 運算子，SQL Server 容器和負載平衡器服務。 運算子會自動協調可用性群組。 這篇文章說明如何：

- 部署運算子、 SQL Server 容器和負載平衡服務
- 連接到可用性群組與服務
- 將資料庫新增至可用性群組

## <a name="requirements"></a>需求

- Kubernetes 叢集
- Kubernetes 版本 1.11.0 或更高版本
- 至少三個節點
- [kubectl](http://kubernetes.io/docs/tasks/tools/install-kubectl/)。
- 若要存取[sql server 範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)github 存放庫

  >[!NOTE]
  >您可以使用任何類型的 Kubernetes 叢集。 若要在 Azure Kubernetes Service (AKS) 建立 Kubernetes 叢集，請參閱[建立 AKS 叢集](http://docs.microsoft.com/azure/aks/create-cluster)。
  > 下列指令碼會在 Azure 中建立四個節點的 Kubernetes 叢集。
  >```azure-cli
  az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 4 --kubernetes-version 1.11.3
  >```

## <a name="deploy-the-operator-sql-server-containers-and-load-balancing-services"></a>部署運算子、 SQL Server 容器和負載平衡服務

1. 建立[命名空間](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)。

  此範例會使用命名空間稱為`ag1`。 執行下列命令來建立命名空間。

  ```azurecli
  kubectl create namespace ag1
  ```

  屬於此解決方案的所有物件都是在`ag1`命名空間。

1. 設定及部署 SQL Server 的操作員資訊清單。

  複製 SQL Server [ `operator.yaml` ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/operator.yaml)檔案[sql server 範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)。

  `operator.yaml`檔案是 Kubernetes 運算子的部署資訊清單。

  適用於 Kubernetes 叢集資訊清單。

  ```azurecli
  kubectl apply -f operator.yaml --namespace ag1
  ```

1. 使用密碼建立 Kubernetes 祕密`sa`帳戶和 SQL Server 執行個體的主要金鑰。

  建立的祕密`kubectl`。
  
  下列範例會建立名為祕密`sql-secrets`在`ag1`命名空間。 密碼會儲存兩個密碼：
  
  - `sapassword` 適用於 SQL Server 中儲存密碼`sa`帳戶。
  - `masterkeypassword` 儲存用來建立 SQL Server 主要金鑰的密碼。 

  將指令碼複製到您的終端機中。 取代每個`<>`使用複雜密碼，然後執行指令碼來建立祕密。

  >[!NOTE]
  >密碼不能使用`&`，或`` ` ``字元。

  ```azurecli
  kubectl create secret generic sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
  ```

1. 部署 SQL Server 自訂資源。

  複製 SQL Server 的資訊清單[ `sqlserver.yaml` ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/sqlserver.yaml)從[sql server 範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)。

  >[!NOTE]
  >`sqlserver.yaml`檔案描述 SQL Server 容器、 永續性磁碟區宣告、 永續性磁碟區，以及所需的每個 SQL Server 執行個體的負載平衡服務。

  適用於 Kubernetes 叢集資訊清單。

  ```azurecli
  kubectl apply -f sqlserver.yaml --namespace ag1
  ```
  
  下圖顯示成功的應用程式的`kubectl apply`此範例中。

  ![建立 sqlservers](./media/sql-server-linux-kubernetes-deploy/create-sqlservers.png)

  在您套用 SQL Server 的資訊清單之後，運算子會將 SQL Server 容器部署。

  Kubernetes 會置於 pod 中容器。 使用`kubectl get pods --namespace ag1`來查看 pod 的狀態。 SQL Server 的 pod 部署後下, 圖顯示部署的範例。 

  ![內建的 pod](./media/sql-server-linux-kubernetes-deploy/builtpods.png)

### <a name="monitor-the-deployment"></a>監視部署

您可以使用[Kubernetes 儀表板與 Azure Kubernetes Service (AKS)](https://docs.microsoft.com/en-us/azure/aks/kubernetes-dashboard)來監視部署。

使用`az aks browse`啟動儀表板。 

## <a name="connect-to-the-availability-group-with-the-services"></a>連接到可用性群組與服務

[ `ag-services.yaml` ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml)從[sql server 範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)範例將告訴您可以連接到可用性群組複本的負載平衡服務。 

- `ag1-primary` 提供連接到主要複本的端點。
- `ag1-secondary` 提供要連接至任何次要複本的端點。

當您套用資訊清單檔案時，Kubernetes 會建立複本的每個類型的負載平衡服務。 負載平衡服務包括 IP 位址。 使用此 IP 位址連接到複本，您需要的類型。

若要部署的服務，請執行下列命令。

```azurecli
kubectl apply -f ag-services.yaml --namespace ag1
```

部署服務之後，請使用`kubectl get services --namespace ag1`來識別服務的 IP 位址。

使用 IP 位址，您可以連接到 SQL Server 執行個體裝載複本的每個型別。

下圖顯示：

- 輸出`kubectl get services`命名空間`ag1`。

 服務會針對每個 SQL Server 容器的負載平衡服務。 使用這些 IP 位址做為端點，直接連接到 SQL Server 叢集中的執行個體。

- `sqlcmd`連接到主要複本，與`sa`透過負載平衡器端點的帳戶。

![connect](./media/sql-server-linux-kubernetes-deploy/connect.png)

## <a name="add-a-database-to-the-availability-group"></a>將資料庫新增至可用性群組

>[!NOTE]
>在此階段中，SQL Server Management Studio 就無法將資料庫加入可用性群組。 使用 Transact SQL。

Kubernetes 會建立 SQL Server 容器之後，請完成下列步驟來將資料庫加入可用性群組：

1. [連接](sql-server-linux-kubernetes-connect.md)叢集中的 SQL Server 執行個體。

1. 建立資料庫。

  ```sql
  CREATE DATABASE [demodb]
  ```

1. 進行完整備份的資料庫，以便啟動記錄鏈結。

  ```sql
  USE MASTER
  GO
  BACKUP DATABASE [demodb] 
  TO DISK = N'/var/opt/mssql/data/demodb.bak'
  ```

1. 您可以將資料庫加入可用性群組。

  ```sql
  ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [demodb]
  ```

使用自動植入讓 SQL Server 會自動建立次要複本建立可用性群組。

您可以檢視 SQL Server Management Studio 可用性群組儀表板的可用性群組的狀態。

![儀表板](./media/sql-server-linux-kubernetes-deploy/dashboard.png)

## <a name="next-steps"></a>後續步驟

[連接到 Kubernetes 叢集上的 SQL Server 可用性群組](sql-server-linux-kubernetes-connect.md)

[管理 Kubernetes 叢集上的 SQL Server 可用性群組](sql-server-linux-kubernetes-manage.md)

[在 Kubernetes 叢集上的 SQL Server 可用性群組](sql-server-ag-kubernetes.md)
