---
title: 部署 Kubernetes 使用 Azure Kubernetes Service (AKS) 中的 SQL Server 容器
description: 本教學課程會示範如何部署 SQL Server 高可用性解決方案使用 Azure Kubernetes Service 上的 Kubernetes。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 01/10/2018
ms.topic: tutorial
ms.prod: sql
ms.custom: mvc
ms.technology: linux
ms.openlocfilehash: 76c4003398368a1cdbadb257165dab6b048ebced
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67832993"
---
# <a name="deploy-a-sql-server-container-in-kubernetes-with-azure-kubernetes-services-aks"></a>部署 Kubernetes 使用 Azure Kubernetes Service (AKS) 中的 SQL Server 容器

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

了解如何設定 SQL Server 執行個體，Kubernetes Azure Kubernetes Service (AKS) 中，具有高可用性 (HA) 的永續性儲存體。 此解決方案提供恢復功能。 如果 SQL Server 執行個體失敗，Kubernetes 會自動重新建立它的新的 pod 中。 Kubernetes 也會提供節點失敗時恢復運作。

本教學課程會示範如何在 AKS 的容器中設定高可用性的 SQL Server 執行個體。 您也可以建立[Always On 可用性群組的 SQL Server 容器](sql-server-ag-kubernetes.md)。 若要比較兩個不同的 Kubernetes 解決方案，請參閱[高可用性 SQL Server 容器](sql-server-linux-container-ha-overview.md)。

> [!div class="checklist"]
> * 建立的 SA 密碼
> * 建立儲存體
> * 建立部署
> * 使用 SQL Server Management Studio (SSMS) 連接
> * 確認失敗與復原

## <a name="ha-solution-on-kubernetes-running-in-azure-kubernetes-service"></a>在 Azure Kubernetes Service 中執行的 Kubernetes 上的 HA 解決方案

Kubernetes 1.6 和更新版本可支援[儲存類別](https://kubernetes.io/docs/concepts/storage/storage-classes/)，[永續性磁碟區宣告](https://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims)，而[Azure 磁碟的磁碟區類型](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk)。 您可以建立和管理 Kubernetes 中的原生的 SQL Server 執行個體。 這篇文章中的範例示範如何建立[部署](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)以達到類似的共用的磁碟容錯移轉叢集執行個體的高可用性組態。 在此組態中，Kubernetes 會扮演的角色叢集 orchestrator。 當容器中的 SQL Server 執行個體失敗時，協調器會啟動另一個執行個體附加至相同的永續性儲存體的容器。

![Kubernetes SQL Server 叢集的圖表](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

在上圖中，`mssql-server`是中的容器[pod](https://kubernetes.io/docs/concepts/workloads/pods/pod/)。 Kubernetes 會協調在叢集中的資源。 A[複本集](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)可確保 pod，節點失敗後自動復原。 應用程式連接至服務。 在此情況下，服務會代表裝載失敗後會保持相同的 IP 位址的負載平衡器`mssql-server`。

在下列圖表中，`mssql-server`容器失敗。 作為協調者，Kubernetes 會保證正確的複本中狀況良好的執行個體計數設定，並啟動新的容器，根據組態。 Orchestrator 的相同節點上，啟動新的 pod 和`mssql-server`重新連線至相同的永續性儲存體。 服務連接到重新建立`mssql-server`。

![Kubernetes SQL Server 叢集的圖表](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-pod-fail.png)

在下列圖表中，節點裝載`mssql-server`容器失敗。 Orchestrator 的不同節點上，啟動新的 pod 和`mssql-server`重新連線至相同的永續性儲存體。 服務連接到重新建立`mssql-server`。

![Kubernetes SQL Server 叢集的圖表](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-node-fail.png)

## <a name="prerequisites"></a>先決條件

* **Kubernetes 叢集**
   - 本教學課程需要一個 Kubernetes 叢集。 步驟會使用[kubectl](https://kubernetes.io/docs/user-guide/kubectl/)來管理叢集。 

   - 請參閱[部署 Azure Container Service (AKS) 叢集](https://docs.microsoft.com/azure/aks/tutorial-kubernetes-deploy-cluster)來建立並連接到在 AKS 中使用的單一節點 Kubernetes 叢集`kubectl`。 

   >[!NOTE]
   >若要防止節點失敗，Kubernetes 叢集需要一個以上的節點。

* **Azure CLI 2.0.23**
   - 在本教學課程的指示已針對 Azure CLI 2.0.23 已驗證。

## <a name="create-an-sa-password"></a>建立的 SA 密碼

在 Kubernetes 叢集中建立的 SA 密碼。 Kubernetes 可管理敏感的組態資訊，例如密碼[祕密](https://kubernetes.io/docs/concepts/configuration/secret/)。

下列命令會建立 SA 帳戶的密碼：

   ```azurecli
   kubectl create secret generic mssql --from-literal=SA_PASSWORD="MyC0m9l&xP@ssw0rd"
   ```  

   取代`MyC0m9l&xP@ssw0rd`使用的複雜密碼。

   若要建立名為 Kubernetes 中的祕密`mssql`保存的值`MyC0m9l&xP@ssw0rd`如`SA_PASSWORD`，執行命令。


## <a name="create-storage"></a>建立儲存體

設定[永續性磁碟區](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)並[永續性磁碟區宣告](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistent-volume-claim-protection)的 Kubernetes 叢集中。 完成下列步驟： 

1. 建立資訊清單來定義的儲存體類別和永續性磁碟區宣告。  資訊清單會指定儲存體佈建程式，參數，並[收回原則](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#reclaiming)。 Kubernetes 叢集會使用此資訊清單，來建立永續性儲存體。 

   下列 yaml 範例會定義儲存類別和永續性磁碟區宣告。 儲存體類別佈建程式是`azure-disk`，因為此 Kubernetes 叢集是在 Azure 中。 儲存體帳戶類型是`Standard_LRS`。 永續性磁碟區宣告名為`mssql-data`。 永續性磁碟區宣告中繼資料包括： 註釋連接回儲存體類別。 

   ```yaml
   kind: StorageClass
   apiVersion: storage.k8s.io/v1beta1
   metadata:
        name: azure-disk
   provisioner: kubernetes.io/azure-disk
   parameters:
     storageaccounttype: Standard_LRS
     kind: Managed
   ---
   kind: PersistentVolumeClaim
   apiVersion: v1
   metadata:
     name: mssql-data
     annotations:
       volume.beta.kubernetes.io/storage-class: azure-disk
   spec:
     accessModes:
     - ReadWriteOnce
     resources:
       requests:
         storage: 8Gi
   ```

   儲存檔案 (例如**pvc.yaml**)。

1. 在 Kubernetes 中建立的永續性磁碟區宣告。

   ```azurecli
   kubectl apply -f <Path to pvc.yaml file>
   ```

   `<Path to pvc.yaml file>` 是您用來儲存檔案的位置。

   永續性磁碟區會自動建立為 Azure 儲存體帳戶，並繫結至永續性磁碟區宣告。 

    ![永續性磁碟區宣告命令的螢幕擷取畫面](media/tutorial-sql-server-containers-kubernetes/02_pvc_cmd.png)

1. 請確認永續性磁碟區宣告。

   ```azurecli
   kubectl describe pvc <PersistentVolumeClaim>
   ```

   `<PersistentVolumeClaim>` 是永續性磁碟區宣告的名稱。

   在上述步驟中，名為永續性磁碟區宣告`mssql-data`。 若要查看的永續性磁碟區宣告的相關中繼資料，請執行下列命令：

   ```azurecli
   kubectl describe pvc mssql-data
   ```

   傳回的中繼資料包含一個值，稱為`Volume`。 這個值會對應至 blob 的名稱。

   ![傳回的中繼資料，包括磁碟區的螢幕擷取畫面](media/tutorial-sql-server-containers-kubernetes/describe-volume.png)

   磁碟區的值符合下列映像從 Azure 入口網站中的 blob 名稱的一部分： 

   ![螢幕擷取畫面的 Azure 入口網站的 blob 名稱](media/tutorial-sql-server-containers-kubernetes/describe-volume-portal.png)

1. 請確認永續性磁碟區。

   ```azurecli
   kubectl describe pv
   ```

   `kubectl` 傳回自動建立和繫結至永續性磁碟區宣告的永續性磁碟區相關的中繼資料。 

## <a name="create-the-deployment"></a>建立部署

在此範例中，裝載 SQL Server 執行個體的容器會描述為 Kubernetes 部署物件。 部署會建立在複本集。 複本集所建立的 pod。 

在此步驟中，會建立資訊清單，以描述 SQL Server 為基礎的容器[mssql server linux](https://hub.docker.com/_/microsoft-mssql-server) Docker 映像。 資訊清單參考`mssql-server`永續性磁碟區宣告，而`mssql`已經套用到 Kubernetes 叢集的密碼。 資訊清單也會說明[服務](https://kubernetes.io/docs/concepts/services-networking/service/)。 此服務是負載平衡器。 負載平衡器可保證在復原 SQL Server 執行個體之後，仍然存在的 IP 位址。 

1. 建立要描述的部署資訊清單 （YAML 檔案）。 下列範例說明的部署，包括 SQL Server 容器映像為基礎的容器。

   ```yaml
   apiVersion: apps/v1beta1
   kind: Deployment
   metadata:
     name: mssql-deployment
   spec:
     replicas: 1
     template:
       metadata:
         labels:
           app: mssql
       spec:
         terminationGracePeriodSeconds: 10
         containers:
         - name: mssql
           image: mcr.microsoft.com/mssql/server:2017-latest
           ports:
           - containerPort: 1433
           env:
           - name: MSSQL_PID
             value: "Developer"
           - name: ACCEPT_EULA
             value: "Y"
           - name: MSSQL_SA_PASSWORD
             valueFrom:
               secretKeyRef:
                 name: mssql
                 key: SA_PASSWORD 
           volumeMounts:
           - name: mssqldb
             mountPath: /var/opt/mssql
         volumes:
         - name: mssqldb
           persistentVolumeClaim:
             claimName: mssql-data
   ---
   apiVersion: v1
   kind: Service
   metadata:
     name: mssql-deployment
   spec:
     selector:
       app: mssql
     ports:
       - protocol: TCP
         port: 1433
         targetPort: 1433
     type: LoadBalancer
   ```

   將上述程式碼複製到新的檔案，名為`sqldeployment.yaml`。 更新下列值： 

   * MSSQL_PID `value: "Developer"`:設定要執行的 SQL Server Developer edition 的容器。 開發人員版本未授權用於生產環境的資料。 如果是部署用於生產環境中，設定適當的版本 (`Enterprise`， `Standard`，或`Express`)。 

      >[!NOTE]
      >如需詳細資訊，請參閱 < [SQL Server 授權如何](https://www.microsoft.com/sql-server/sql-server-2017-pricing)。

   * `persistentVolumeClaim`:此值需要的項目`claimName:`對應至用於永續性磁碟區宣告的名稱。 本教學課程使用`mssql-data`。 

   * `name: SA_PASSWORD`:設定容器映像設定 SA 密碼，這一節中所定義。

     ```yaml
     valueFrom:
       secretKeyRef:
         name: mssql
         key: SA_PASSWORD 
     ```

     當 Kubernetes 部署容器時，它會參考名為祕密`mssql`以取得此值的密碼。 

   >[!NOTE]
   >使用`LoadBalancer`服務型別，SQL Server 執行個體是可從遠端 （透過網際網路） 存取連接埠 1433年。

   儲存檔案 (例如**sqldeployment.yaml**)。

1. 建立部署。

   ```azurecli
   kubectl apply -f <Path to sqldeployment.yaml file>
   ```

   `<Path to sqldeployment.yaml file>` 是您用來儲存檔案的位置。

   ![部署命令的螢幕擷取畫面](media/tutorial-sql-server-containers-kubernetes/04_deploy_cmd.png)

   建立部署和服務。 SQL Server 執行個體是在容器中，連接到永續性儲存體。

   若要檢視 pod 的狀態，請輸入`kubectl get pod`。

   ![Get pod 命令的螢幕擷取畫面](media/tutorial-sql-server-containers-kubernetes/05_get_pod_cmd.png)

   在上述影像中，pod 的狀態已`Running`。 此狀態指出容器已就緒。 這可能需要幾分鐘的時間。

   >[!NOTE]
   >建立部署之後，可能需要幾分鐘的時間之前是可見的 pod。 延遲是因為叢集會提取[mssql server linux](https://hub.docker.com/_/microsoft-mssql-server)從 Docker hub 映像。 第一次它提取映像之後，後續的部署可能會比較快，如果部署至已有映像快取於其中的節點。 

1. 確認服務正在執行。 執行下列命令：

   ```azurecli
   kubectl get services 
   ```

   此命令會傳回正在執行的服務，以及服務的內部和外部 IP 位址。 請記下外部 IP 位址的`mssql-deployment`服務。 若要連接到 SQL Server 中使用此 IP 位址。 

   ![Get service 命令的螢幕擷取畫面](media/tutorial-sql-server-containers-kubernetes/06_get_service_cmd.png)

   如需詳細的 Kubernetes 叢集中的物件狀態的相關資訊，請執行：

   ```azurecli
   az aks browse --resource-group <MyResourceGroup> --name <MyKubernetesClustername>
   ```  

## <a name="connect-to-the-sql-server-instance"></a>連接到 SQL Server 執行個體

如果如所述，您可以設定容器，您可以使用應用程式從 Azure 虛擬網路外部進行連線。 使用`sa`帳戶和外部 IP 位址的服務。 使用您設定為 Kubernetes 祕密的密碼。 

您可以使用下列應用程式連接到 SQL Server 執行個體。 

* [SSMS](https://docs.microsoft.com/sql/linux/sql-server-linux-manage-ssms)

* [SSDT](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-ssdt)

* sqlcmd
   
   與連線`sqlcmd`，執行下列命令：

   ```cmd
   sqlcmd -S <External IP Address> -U sa -P "MyC0m9l&xP@ssw0rd"
   ```

   取代下列值：
      
    - `<External IP Address>` 使用的 IP 位址`mssql-deployment`服務 
    - `MyC0m9l&xP@ssw0rd` 使用您的密碼

## <a name="verify-failure-and-recovery"></a>確認失敗與復原

若要驗證的失敗與復原，您可以刪除 pod。 執行下列步驟：

1. 列出執行 SQL Server 的 pod。

   ```azurecli
   kubectl get pods
   ```

   記下執行 SQL Server 的 pod 的名稱。

1. 刪除 pod。

   ```azurecli
   kubectl delete pod mssql-deployment-0
   ```
   `mssql-deployment-0` 從上一個步驟的 pod 名稱傳回的值。 

Kubernetes 時，會自動重新建立的 pod 來復原 SQL Server 執行個體，並連接到永續性儲存體。 使用`kubectl get pods`來確認已部署新的 pod。 使用`kubectl get services`來確認新的容器的 IP 位址相同。 

## <a name="summary"></a>總結

在本教學課程中，您已了解如何將 SQL Server 容器部署至 Kubernetes 叢集的高可用性。 

> [!div class="checklist"]
> * 建立的 SA 密碼
> * 建立儲存體
> * 建立部署
> * 使用 SQL Server Management Studio (SSMS) 連線
> * 確認失敗與復原

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
>[Kubernetes 的簡介](https://docs.microsoft.com/azure/aks/intro-kubernetes)


