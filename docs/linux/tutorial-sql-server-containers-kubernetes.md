---
title: "針對高可用性設定 SQL Server 容器中 Kubernetes |Microsoft 文件"
description: "本教學課程會示範如何部署與 Kubernetes Azure 容器服務上的 SQL Server 高可用性解決方案。"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 01/10/2018
ms.topic: tutorial
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: mvc
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: 5055a5956ce83dadae3cef13f0855db02a61d01b
ms.sourcegitcommit: 06131936f725a49c1364bfcc2fccac844d20ee4d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2018
---
# <a name="configure-sql-server-container-in-kubernetes-for-high-availability"></a>設定高可用性 Kubernetes 中的 SQL Server 容器

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

請遵循本文章 Kubernetes Azure 容器服務 (AKS) 上設定 SQL Server 執行個體，以提供高可用性的永續性儲存體。 方案提供恢復功能。 如果 SQL Server 執行個體失敗，Kubernetes 自動重新建立，並在新的 pod。 AKS 提供 Kubernetes 節點發生故障的恢復功能。 

本教學課程會示範如何使用 AKS 容器中設定高可用性的 SQL Server 執行個體。 

> [!div class="checklist"]
> * 建立 SA 密碼
> * 建立儲存體
> * 建立部署
> * 與 SQL Server Management Studio (SSMS) 連接
> * 確認失敗與復原

### <a name="ha-solution-using-kubernetes-running-in-azure-container-service"></a>使用 Kubernetes Azure 容器服務中執行的 HA 解決方案

支援的 Kubernetes 1.6 +[儲存類別](http://kubernetes.io/docs/concepts/storage/storage-classes/)，[永續性磁碟區宣告](http://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims)，和[Azure 磁碟的磁碟區的驅動程式](http://github.com/Azure/azurefile-dockervolumedriver)。 您可以建立及管理原生中 Kubernetes 的 SQL Server 執行個體。 這篇文章中的範例示範如何建立[部署](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)達到高可用性組態類似於共用的磁碟容錯移轉叢集執行個體。 此設定會 Kubernetes 扮演叢集 orchestrator 的角色。 當容器中的 SQL Server 執行個體失敗時，orchestrator bootstraps 附加至相同的永續性儲存體容器的另一個執行個體。

![Kubernetes SQL Server 叢集](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

在上圖中，`mssql-server`是中的容器[pod](http://kubernetes.io/docs/concepts/workloads/pods/pod/)。 Kubernetes 會協調叢集中的資源。 A[複本集](http://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)可確保在節點失敗之後會自動復原 pod。 應用程式連接至服務。 在此情況下，服務會代表裝載失敗後會保持相同的 IP 位址的負載平衡器`mssql-server`。

在下列圖表中，`mssql-server`容器失敗。 為 orchestrator Kubernetes 可確保正確的複本中處於狀況良好的執行個體計數設定並啟動新的容器，根據組態。 Orchestrator 的相同節點上，啟動新的 pod 和`mssql-server`重新連線到相同的永續性儲存體。 此服務會連接到重新建立`mssql-server`。

![Kubernetes SQL Server 叢集之後](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-pod-fail.png)

在下列圖表中，節點裝載`mssql-server`容器失敗。 Orchestrator 的不同節點上，啟動新的 pod 和`mssql-server`重新連線到相同的永續性儲存體。 此服務會連接到重新建立`mssql-server`。

![Kubernetes SQL Server 叢集之後](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-node-fail.png)

## <a name="prerequisites"></a>필수 구성 요소

* **Kubernetes 叢集**
   - 此教學課程需要 Kubernetes 叢集。 這些步驟使用[kubectl](https://kubernetes.io/docs/user-guide/kubectl/)來管理叢集。 

   - 您可以遵循的指示[部署 Azure 容器服務 (AKS) 叢集](http://docs.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-cluster)建立，並連接到單一節點 Kubernetes 叢集在與 AKS `kubectl`。 

   >[!NOTE]
   >若要保護節點發生故障，Kubernetes 叢集需要一個以上的節點。

* **Azure CLI 2.0.23**
   - 本教學課程中的指示已針對 Azure CLI 2.0.23 已驗證。

## <a name="create-sa-password"></a>建立 SA 密碼

Kubernetes 叢集中建立 SA 密碼。 Kubernetes 可以管理等做為密碼的敏感的組態資訊[密碼](http://kubernetes.io/docs/concepts/configuration/secret/)。

El comando siguiente crea SA 帳戶的密碼：

   ```azurecli
   kubectl create secret generic mssql --from-literal=SA_PASSWORD="MyC0m9l&xP@ssw0rd"
   ```  

   取代`MyC0m9l&xP@ssw0rd`使用複雜密碼。

   若要建立名為 Kubernetes 密碼`mssql`保存之值`MyC0m9l&xP@ssw0rd`如`SA_PASSWORD`，執行命令。


## <a name="create-storage"></a>建立儲存體

設定[永續性磁碟區](http://kubernetes.io/docs/concepts/storage/persistent-volumes/)，和[永續性磁碟區宣告](http://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistent-volume-claim-protection)Kubernetes 叢集中。 完成下列步驟： 

1. 建立要定義的儲存類別和永續性磁碟區的資訊清單宣告。  資訊清單會指定儲存體佈建程式，參數，而[收回原則](http://kubernetes.io/docs/concepts/storage/persistent-volumes/#reclaiming)。 Kubernetes 叢集會使用此資訊清單建立永續性儲存體。 

   下例會 yaml 定義儲存類別和永續性磁碟區的宣告。 儲存類別 provisioner 是`azure-disk`因為此 Kubernetes 叢集是在 Azure 中。 儲存體帳戶類型是`Standard_LRS`。 永續性磁碟區宣告名為`mssql-data`。 永續性磁碟區宣告中繼資料包括： 註解連接回儲存類別。 

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

   儲存檔案，例如**pvc.yaml**。

1. Kubernetes 中建立的永續性磁碟區的宣告。

   ```azurecli
   kubectl apply -f <Path to pvc.yaml file>
   ```

   * `<Path to pvc.yaml file>`
      * 儲存檔案的位置。

   永續性磁碟區自動建立的 Azure 儲存體帳戶，及繫結至永續性磁碟區宣告。 

    ![永續性磁碟區宣告命令](media/tutorial-sql-server-containers-kubernetes/02_pvc_cmd.png)

1. 確認持續性磁碟區宣告。

   ```azurecli
   kubectl describe pvc <PersistentVolumeClaim>
   ```

   * `<PersistentVolumeClaim>`
      * 永續性磁碟區宣告的名稱。

    在前述步驟中，名為永續性磁碟區宣告`mssql-data`。 若要查看持續性磁碟區宣告的相關中繼資料，請執行下列命令：

    ```azurecli
    kubectl describe pvc mssql-data
    ```

    傳回的中繼資料包含一個值，稱為`Volume`。 這個值會對應至 blob 的名稱。

    ![描述磁碟區](media/tutorial-sql-server-containers-kubernetes/describe-volume.png)

    磁碟區，在下列映像，從 Azure 入口網站中的 blob 名稱的相符項目一部分的值： 

    ![描述磁碟區入口網站](media/tutorial-sql-server-containers-kubernetes/describe-volume-portal.png)

1. 確認持續性磁碟區。

   ```azurecli
   kubectl describe pv
   ```

   `kubectl`傳回中繼資料持續性磁碟區的自動建立及繫結至永續性磁碟區宣告。 

## <a name="create-the-deployment"></a>建立部署

在此範例中，裝載 SQL Server 執行個體的容器會描述為 Kubernetes 部署物件。 部署會建立複本集。 複本集建立 pod。 

在此步驟中，建立資訊清單，以描述 Microsoft SQL Server 基礎容器[mssql-伺服器-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/) Docker 映像。 資訊清單參考`mssql-server`永續性磁碟區的宣告，而`mssql`密碼已經套用到 Kubernetes 叢集。 資訊清單也會描述[服務](http://kubernetes.io/docs/concepts/services-networking/service/)。 此服務是負載平衡器。 負載平衡器可保證復原 SQL Server 執行個體之後，仍然存在的 IP 位址。 

1. 建立要說明部署資訊清單-yaml 檔案。 下列範例會說明部署，包括容器，根據 SQL Server 的容器映像。

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
           image: microsoft/mssql-server-linux
           ports:
           - containerPort: 1433
           env:
           - name: ACCEPT_EULA
             value: "Y"
           - name: SA_PASSWORD
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

   * `value: "Developer"`
     * 設定執行 SQL Server Developer edition 的容器。 開發人員版本未獲得授權的實際執行資料。 如果是部署用於實際執行環境中，設定適當的版本。 可以是其中一個`Enterprise`， `Standard`，或`Express`。 

      >[!NOTE]
      >如需詳細資訊，請參閱[授權 SQL Server 如何](http://www.microsoft.com/sql-server/sql-server-2017-pricing)。

   * `persistentVolumeClaim`
     * 這個值會要求的項目`claimName:`對應至用於永續性磁碟區宣告的名稱。 本文使用`mssql-data`。 

   * `name: SA_PASSWORD`
      * 設定容器映像設定此區段中定義的 SA 密碼。

      ```yaml
      valueFrom:
        secretKeyRef:
          name: mssql
          key: SA_PASSWORD 
      ```

       當 Kubernetes 部署容器時，則是指密碼名為`mssql`取得密碼值。 

   >[!NOTE]
   >使用`LoadBalancer`服務類型，SQL Server 執行個體是透過遠端 （網際網路） 連接埠 1433年。

    儲存檔案，例如**sqldeployment.yaml**。

1. 建立部署。

   ```azurecli
   kubectl apply -f <Path to sqldeployment.yaml file>
   ```

   * `<Path to sqldeployment.yaml file>`
      * 儲存檔案的位置。

   ![部署命令](media/tutorial-sql-server-containers-kubernetes/04_deploy_cmd.png)

   建立的部署和服務。 SQL Server 執行個體是在容器的永續性儲存體連接。

   若要檢視 pod 的狀態，請輸入`kubectl get pod`。

   ![取得 pod 命令](media/tutorial-sql-server-containers-kubernetes/05_get_pod_cmd.png)

   >[!NOTE]
   >在建立部署之後，可能需要幾分鐘的時間才看到 pod。 延遲是因為叢集中需要提取[mssql-伺服器-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/)從 Docker hub 的映像。 第一次提取之後，後續部署可能更快-如果部署至已使用的映像快取於其中的節點。 

1. 請確認服務正在執行。 執行下列命令：

   ```azurecli
   kubectl get services 
   ```

   此命令會傳回正在執行的服務，以及服務的內部和外部 IP 位址。 請注意的外部 IP 位址`mssql-deployment`服務。  若要連接到 SQL Server 中使用此 IP 位址。 

   ![取得服務命令](media/tutorial-sql-server-containers-kubernetes/06_get_service_cmd.png)

   如需有關狀態 Kubernetes 叢集中的物件的詳細資訊，請執行：

   ```azurecli
   az aks browse --resource-group <MyResourceGroup> --name <MyKubernetesClustername>
   ```  

## <a name="connect-to-the-sql-server-instance"></a>連接到 SQL Server 執行個體

如果所述，您可以設定容器，您可以使用外部應用程式從 Azure 虛擬網路進行連接。 使用`sa`帳戶和外部 IP 位址的服務。 使用您設定為 Kubernetes 密碼的密碼。 

您可以使用下列應用程式連接到 SQL Server 執行個體。 

* [SSMS](http://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-ssms)

* [SSDT](http://docs.microsoft.com/en-us/sql/linux/sql-server-linux-develop-use-ssdt)

* 要用來連接的 sqlcmd `sqlcmd`，執行下列命令：

   ```cmd
   sqlcmd -S <External IP Address> -U sa -P "MyC0m9l&xP@ssw0rd"
   ```

   取代下列值：
      - `<External IP Address>`IP 位址`mssql-deployment`服務 
      - `MyC0m9l&xP@ssw0rd`您的密碼

## <a name="verify-failure-and-recovery"></a>確認失敗與復原

若要確認失敗與復原作業中，您可以刪除 pod。 執行下列步驟：

1. 列出執行 SQL Server 的 pod。

   ```azurecli
   kubectl get pods
   ```

   請注意 pod 執行 SQL Server 的名稱。

1. 刪除 pod。

   ```azurecli
   kubectl delete pod mssql-deployment-0
   ```
   `mssql-deployment-0`從 pod 名稱的前一個步驟傳回的值。 

Kubernetes 自動重新建立復原 SQL Server 執行個體，並連接至永續性儲存體 pod。 使用`kubectl get pods`確認部署新的 pod。 使用`kubectl get services`來確認新的容器的 IP 位址相同。 

## <a name="summary"></a>摘要

在本教學課程中，您將學會如何將 SQL Server 容器部署至高可用性的 Kubernetes 叢集中。 

> [!div class="checklist"]
> * 建立 SA 密碼
> * 建立儲存體
> * 建立部署
> * 與 SQL Server Management Studio (SSMS) 連接
> * 確認失敗與復原

## <a name="next-steps"></a>後續的步驟

> [!div class="nextstepaction"]
>[簡介-Kubernetes](http://docs.microsoft.com/en-us/azure/aks/intro-kubernetes)
