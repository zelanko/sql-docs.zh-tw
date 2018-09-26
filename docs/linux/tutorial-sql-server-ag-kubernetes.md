---
title: 在 Kubernetes 中的 Docker 容器上設定 SQL Server Always On 可用性群組 |Microsoft Docs
description: 本教學課程會示範如何將 SQL Server always on 可用性群組，使用 Azure Container Service 上的 Kubernetes 部署。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: tutorial
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux,mvc
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6d21866f3f7004dff1ea86ca4f608580a79ab754
ms.sourcegitcommit: df21af652d0906ade8cc9ca3985a7ba5569f0db6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2018
ms.locfileid: "47049358"
---
# <a name="configure-a-sql-server-always-on-availability-group-on-docker-containers-in-kubernetes-with-azure-kubernetes-service-aks"></a>在 Kubernetes 使用 Azure Kubernetes Service (AKS) 中的 Docker 容器上設定 SQL Server Always On 可用性群組

本教學課程會示範如何在 AKS 的容器中設定高可用性的 SQL Server 執行個體。 您也可以[部署 Kubernetes 中的 SQL Server 容器](tutorial-sql-server-containers-kubernetes.md)。 若要比較兩個不同的 Kubernetes 解決方案，請參閱[高可用性 SQL Server 容器](sql-server-linux-container-ha-overview.md)。

在本教學課程中，您將了解如何：  

> [!div class="checklist"]
> * 建立儲存體
> * 部署至 Kubernetes 叢集的 SQL Server 運算子 
> * 建立 Kubernetes 祕密
> * 部署 SQL Server 執行個體和健康情況代理程式
> * 連接到主要複本
> * 將資料庫新增至可用性群組

本教學課程示範中的架構[Azure Kubernetes Service (AKS)](http://docs.microsoft.com/azure/aks/)。 如果您還沒有 Azure 訂用帳戶，建立[免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)開始之前。

此圖顯示您在本教學課程中的方案：

![kubernetes ag 叢集](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

### <a name="deployment-methodology-for-kubernetes"></a>針對 Kubernetes 的部署方法

數個這篇文章中的步驟建立資訊清單，然後再部署到叢集的 資訊清單。 資訊清單是您部署的 Kubernetes 物件的描述.yaml 檔案。

在此範例中.yaml 檔案位於[sql server 範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability)。

物件包含儲存體、 運算子、 pod、 容器和服務。

## <a name="prerequisites"></a>先決條件

* 一般熟悉這些技術

  * [Kubernetes](http://kubernetes.io) 1.8 版
  * [Azure Kubernetes Service (AKS)](http://docs.microsoft.com/azure/aks/)
  * [在 Docker 上的 SQL Server](quickstart-install-connect-docker.md)
  * [SQL Server Always On 可用性群組](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)

* 包含四個節點的 Kubernetes 叢集。

  如需相關指示，請參閱[教學課程： 部署 Azure Kubernetes Service (AKS) 叢集](http://docs.microsoft.com/azure/aks/tutorial-kubernetes-deploy-cluster)。

* 安裝[ `kubectl` ](https://docs.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-cluster#install-the-kubectl-cli)。

## <a name="configuration-and-deployment-procedures"></a>設定和部署程序

本教學課程會示範如何將.yaml 檔案套用到 Kubernetes 叢集。

## <a name="create-the-secrets"></a>建立祕密

若要建立 Kubernetes 祕密來儲存 SQL Server SA 帳戶和 SQL Server 主要金鑰的密碼，請執行下列命令。

```azurecli
kubectl create secret generic sql-secrets --from-literal=sapassword="MyC0m9l&xP@ssw0rd" --from-literal=masterkeypassword="MyC0m9l&xP@ssw0rd2"
```

在生產環境中使用不同的複雜密碼。

## <a name="deploy-the-operator"></a>部署運算子

Kubernetes 運算子部署 SQL Server 執行個體，並在 Kubernetes 叢集中設定的可用性群組。 

請參閱範例操作員 [`operator.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/operator.yaml)

下載`operator.yaml`從[sql server 範例](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/)

將運算子部署一個複本 Kubernetes 部署。

若要部署的運算子：

部署與運算子`kubectl apply`命令。

```azurecli
kubectl apply -f operator.yaml
```

## <a name="create-the-sql-server-ag-deployment"></a>建立 SQL Server AG 部署

下一個步驟會建立一個 Kubernetes 部署中的 SQL Server 執行個體和可用性群組。 此部署套用到叢集之後，操作員會作為 Docker 容器部署的 SQL Server 執行個體。 此部署將會導致三個 StatefulSets 與一個 pod。 每個 pod，會包含兩個容器：

* SQL Server 執行個體根據`mssql-server`映像
* HA 監督員

此外，部署描述可用性群組接聽程式的負載平衡器服務

若要部署 mssql server:

1. 複製[sqlserver.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/sqlserver.yaml)到您的電腦。
2. 更新`sqlserver.yaml`為您的環境。


若要部署的 SQL Server 執行個體，並建立可用性群組，請執行下列命令。

```azurecli
kubectl apply -f sqlserver.yaml
```

## <a name="deploy-ag-services"></a>部署 AG 服務

在 Kubernetes 叢集中建立可用性群組之複本的直接呼叫負載平衡器服務。

[ag services.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)會建立四個服務。

* ag1 主要會連接到主要複本。
* ag1 次要同步會連線到同步的次要複本。
* ag1 非同步次要複本會連接到在非同步次要複本。
* ag1 次要複本設定連接至僅限設定的複本。 

  >[!NOTE]
  >這些負載平衡器服務，提供範例。 在本教學課程沒有僅設定的複本。


部署負載平衡器服務，可讓您可以連接到可用性群組。

若要部署的服務，請執行下列命令。

```azurecli
kubectl apply -f ag-services.yaml
```

### <a name="monitor-the-deployment"></a>監視部署

您可以使用[Kubernetes 儀表板與 Azure Kubernetes Service (AKS)](https://docs.microsoft.com/en-us/azure/aks/kubernetes-dashboard)來監視部署。 

使用`az aks browse`啟動儀表板。 

部署之後，您可以更新唯一 AG 成員資格清單和 post init T-SQL 指令碼。 無法更新其他屬性-資源必須刪除並重新建立。 認證自動產生的使用者可以使用旋轉`mssql-server-k8s-rotate-creds`作業。

## <a name="connect-to-the-sql-server-instance-hosting-the-primary-replica"></a>連接到裝載主要複本的 SQL Server 執行個體

`ag-services.yaml`說明為 Kubernetes 服務名稱`ag1-primary`。 `ag1-primary` 建立 Azure load balancer，並指向裝載主要複本的 SQL Server 執行個體。 使用服務的外部 IP 位址為目標伺服器`sa`身分的帳戶，以及密碼您稍早建立的`mssql secret`的密碼。

使用`kubectl get services`以取得此 IP 位址。

例如：

![取得服務範例](media\tutorial-sql-server-ag-containers-kubernetes\KubernetesGetServices.png)

在上圖中，`ag1-primary`服務會有外部 IP 位址的`104.42-50.138`。 

若要使用 SQL 驗證，以連線到 SQL Server，請使用`sa`帳戶、 值`sapassword`您所建立的密碼與此 IP 位址。

例如：

```cmd
sqlcmd -S 104.42.50.138 -U sa -P "MyC0m9l&xP@ssw0rd"
```

![使用 sqlcmd 連接](./media/tutorial-sql-server-ag-containers-kubernetes/sqlcmdConnect.png)

您也可以使用連接[SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。

若要確認您的連線，若要裝載主要複本的 SQL Server 執行個體執行下列查詢：

```sql
SELECT @@SERVERNAME;
```

查詢會傳回裝載主要複本的 SQL Server 執行個體的名稱。

此時，Kubernetes 叢集有三個 docker 容器中的 SQL Server 執行個體。 可用性群組跨越所有三個 SQL Server 執行個體，但沒有資料庫是可用性群組中。 下一個步驟是將資料庫加入可用性群組。

## <a name="add-a-database-to-the-availability-group"></a>將資料庫新增至可用性群組

將資料庫加入至可用性群組：

1. 建立資料庫

  ```sql
  CREATE DATABASE [DemoDB]
  ```

1. 進行完整備份的資料庫啟動的交易記錄鏈結

  ```sql
  BACKUP DATABASE [DemoDB] 
  TO  DISK = N'/var/opt/mssql/data/DemoDB.bak' 
    WITH NOFORMAT, 
    NOINIT,  
    NAME = N'DemoDB-Full Database Backup', 
    SKIP, 
    NOREWIND, 
    NOUNLOAD,  
    STATS = 10;
  GO
  ```

1. 將資料庫加入可用性群組

  ```sql
  ALTER AVAILABILITY GROUP ag1 ADD DATABASE [DemoDB]; 
  ```

讓可用性群組植入次要複本上的資料庫，複本會自動設定與自動植入模式。

在 SQL Server Management Studio，您可以連接到主要複本，並查看在儀表板的可用性群組。

下列範例會示範設定儀表板中的三個節點上之可用性群組的複本。

![AG1 儀表板](./media/tutorial-sql-server-ag-containers-kubernetes/ssms_AG1.png)

## <a name="verify-failure-and-recovery"></a>確認失敗與復原

若要確認失敗偵測和容錯移轉中，您可以刪除裝載主要複本的 pod。 Kubernetes 會選擇新的主要複本，並重新導向的接聽程式。 然後它會重新建立已刪除的 pod。 

為了示範此程序，執行下列步驟：

1. 列出執行 SQL Server 的 pod。

   ```azurecli
   kubectl get pods
   ```

2. 識別執行主要複本的 pod。

   其中一個連接到主要複本使用的外部 IP 和查詢`@@servername`或使用`kubectl`取得適當的 pod。 此命令會傳回包含執行 AG 的主要複本之容器的 pod 的名稱：

   ```azurecli
   kubectl get pods --selector="role.ag.mssql.microsoft.com/ag1"="primary" --output=jsonpath={.items..metadata.name}
   ```

3. 刪除 pod。

   ```azurecli
   kubectl delete pod <podName>
   ```

取代`<podName>`pod 名稱在上一個步驟傳回的值。 

Kubernetes 自動容錯移轉到其中一個可用的同步處理次要複本，以及重新建立已刪除的 pod。

## <a name="clean-up-resources"></a>清除資源

當不再需要刪除資源群組和所有相關的資源。 執行下列命令：
>[!WARNING]
>此命令會完全刪除資源群組中的所有項目。 當您刪除資源群組之後，沒有任何 Kubernetes 叢集的元件會提供。

```azurecli
az group delete --name <MyResourceGroup>
```

若要執行上述命令，取代`<MyResourceGroup>`與您的資源群組名稱。 

Azure 會刪除資源群組。

## <a name="summary"></a>總結

在本教學課程中，您已了解如何：  

> [!div class="checklist"]
> * 建立儲存體
> * 部署至 Kubernetes 叢集的 SQL Server 運算子 
> * 建立 Kubernetes 祕密
> * 部署 SQL Server 執行個體和健康情況代理程式
> * 連接到主要複本
> * 將資料庫新增至可用性群組

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
>[Kubernetes 的簡介](http://docs.microsoft.com/azure/aks/intro-kubernetes)
>[管理的 Kubernetes 上的 SQL Server](sql-server-linux-kubernetes-manage.md)