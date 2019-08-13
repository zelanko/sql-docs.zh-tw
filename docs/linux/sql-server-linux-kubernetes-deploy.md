---
title: 在 Kubernetes 叢集上部署 SQL Server Always On 可用性群組
description: 本文說明 SQL Server Kubernetes Always On 可用性群組運算子參數的全域需求
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 10/02/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a4811c1f41c4c8b9a566dc13b3de713576b4980d
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "67952620"
---
# <a name="deploy-a-sql-server-always-on-availability-group-on-a-kubernetes-cluster"></a>在 Kubernetes 叢集上部署 SQL Server Always On 可用性群組

本文中的範例使用三個複本在 Kubernetes 叢集上部署 SQL Server Always On 可用性群組。 次要複本處於同步認可模式。

Kubernetes 上的部署包括 SQL Server 運算子、SQL Server 容器和負載平衡器服務。 運算子會自動協調可用性群組。 本文說明如何：

- 部署運算子、SQL Server 容器和負載平衡服務。
- 使用服務連線到可用性群組。
- 將資料庫新增至可用性群組。

## <a name="requirements"></a>需求

- 最新版本的 AKS Kubernetes 叢集
- 至少三個節點
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- 可存取 [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) GitHub 存放庫

> [!NOTE]
> 您可以使用任意類型的 Kubernetes 叢集。 若要在 Azure Kubernetes Service (AKS) 上建立 Kubernetes 叢集，請參閱[建立 AKS 叢集](https://docs.microsoft.com/azure/aks/create-cluster)。
>
> 使用最新版的 Kubernetes。 確切版本取決於您的訂用帳戶和區域。 請參閱 [Supported Kubernetes versions in AKS](https://docs.microsoft.com/en-us/azure/aks/supported-kubernetes-versions) (AKS 中支援的 Kubernetes 版本)。  
>
> 下列指令碼會在 Azure 中建立四個節點的 Kubernetes 叢集。 執行指令碼之前，請以最新的可用版本取代 `<latest version>`。 例如 `1.12.5`。
>
> ```azure-cli
> az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 4 --kubernetes-version <latest version> --generate-ssh-keys
> ```

## <a name="deploy-the-operator-sql-server-containers-and-load-balancing-services"></a>部署運算子、SQL Server 容器和負載平衡服務

1. 建立[命名空間](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)。

      此範例使用名為 `ag1` 的命名空間。 請執行下列命令，建立命名空間。
    
      ```azurecli
      kubectl create namespace ag1
      ```
    
      所有屬於此解決方案的物件都在 `ag1` 命名空間中。

1. 設定和部署 SQL Server 運算子資訊清單。

      從 [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) 複製 SQL Server [`operator.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/operator.yaml) 檔案。
    
      `operator.yaml` 檔案是 Kubernetes 運算子的部署資訊清單。
    
      將資訊清單套用至 Kubernetes 叢集。
    
      ```azurecli
      kubectl apply -f operator.yaml --namespace ag1
      ```
    
1. 使用 `sa` 帳戶的密碼和 SQL Server 執行個體主要金鑰，建立 Kubernetes 的祕密。

      使用 `kubectl` 建立祕密。
      
      下列範例會在 `ag1` 命名空間中建立名為 `sql-secrets` 的祕密。 此祕密會儲存兩個密碼：
      
      - `sapassword` 會儲存 SQL Server `sa` 帳戶的密碼。
      - `masterkeypassword` 會儲存用來建立 SQL Server 主要金鑰的密碼。 
    
   將指令碼複製到您的終端。 以複雜密碼取代每個 `<>`，並執行指令碼來建立祕密。
    
   >[!NOTE]
   >密碼不能使用 `&` 或 `` ` `` 字元。
    
   ```azurecli
   kubectl create secret generic sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
   ```

1. 部署 SQL Server 自訂資源。

      從 [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) 複製 SQL Server 資訊清單 [`sqlserver.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/sqlserver.yaml)。
    
      >[!NOTE]
      >`sqlserver.yaml` 檔案描述每個 SQL Server 執行個體所需的 SQL Server 容器、永久性磁碟區宣告、永久性磁碟區和負載平衡服務。
    
      將資訊清單套用至 Kubernetes 叢集。
    
      ```azurecli
      kubectl apply -f sqlserver.yaml --namespace ag1
      ```
      
下圖顯示在此範例中成功套用 `kubectl apply`。

![建立 sqlserver](./media/sql-server-linux-kubernetes-deploy/create-sqlservers.png)

套用 SQL Server 資訊清單之後，運算子會部署 SQL Server 容器。

Kubernetes 會將容器放在 Pod 中。 使用 `kubectl get pods --namespace ag1` 查看 Pod 的狀態。 下圖顯示部署 SQL Server Pod 之後的範例部署。 

![已建置 Pod](./media/sql-server-linux-kubernetes-deploy/builtpods.png)

### <a name="monitor-the-deployment"></a>監視部署

您可以使用 [Azure Kubernetes Service 隨附的 Kubernetes 儀表板](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)監視部署。

使用 `az aks browse` 啟動儀表板。 

## <a name="connect-to-the-availability-group-with-the-services"></a>使用服務連線到可用性群組

[sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) 範例中的 [`ag-services.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml) 描述可連線到可用性群組複本的負載平衡服務。 

- `ag1-primary` 提供連線到主要複本的端點。
- `ag1-secondary` 提供連線到任意次要複本的端點。

當您套用資訊清單檔時，Kubernetes 會建立適合各種複本類型的負載平衡服務。 負載平衡服務包括 IP 位址。 使用此 IP 位址連線到您所需的複本類型。

若要部署服務，請執行下列命令。

```azurecli
kubectl apply -f ag-services.yaml --namespace ag1
```

部署服務之後，請使用 `kubectl get services --namespace ag1` 識別服務的 IP 位址。

使用 IP 位址，您可以連線到裝載每種複本類型的 SQL Server 執行個體。

下圖顯示：

- 命名空間 `ag1` 的 `kubectl get services` 輸出。

- 針對每個 SQL Server 容器建立的負載平衡服務。 使用這些 IP 位址作為端點，直接連線到叢集中的 SQL Server 執行個體。

- 使用 `sa` 帳戶並透過負載平衡器端點，與主要複本的 `sqlcmd` 連線。

![連線](./media/sql-server-linux-kubernetes-deploy/connect.png)

## <a name="add-a-database-to-the-availability-group"></a>將資料庫新增至可用性群組

>[!NOTE]
>此時 SQL Server Management Studio 無法將資料庫新增至可用性群組。 請使用 Transact-SQL。

在 Kubernetes 建立 SQL Server 容器之後，請完成下列步驟，將資料庫新增至可用性群組。

1. [連線](sql-server-linux-kubernetes-connect.md)到叢集中的 SQL Server 執行個體。

1. 建立資料庫。

      ```sql
      CREATE DATABASE [demodb]
      ```

1. 完整備份資料庫以利啟動記錄鏈結。

      ```sql
      USE MASTER
      GO
      BACKUP DATABASE [demodb] 
      TO DISK = N'/var/opt/mssql/data/demodb.bak'
      ```

1. 將資料庫新增至可用性群組。

      ```sql
      ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [demodb]
      ```
    
使用自動植入建立可用性群組，讓 SQL Server 可自動建立次要複本。

您可以從 SQL Server Management Studio 的 [可用性群組] 儀表板，檢視可用性群組的狀態。

![儀表板](./media/sql-server-linux-kubernetes-deploy/dashboard.png)

## <a name="next-steps"></a>後續步驟

- [連線到 Kubernetes 叢集上的 SQL Server 可用性群組](sql-server-linux-kubernetes-connect.md)

- [管理 Kubernetes 叢集上的 SQL Server 可用性群組](sql-server-linux-kubernetes-manage.md)

- [SQL Server 支援 Kubernetes 叢集中容器上的可用性群組](sql-server-ag-kubernetes.md)
