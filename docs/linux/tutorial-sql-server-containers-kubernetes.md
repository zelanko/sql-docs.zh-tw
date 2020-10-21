---
title: 使用 Azure Kubernetes Service (AKS) 部署 SQL Server 容器
description: 本教學課程說明如何使用 Azure Kubernetes Service 中的 Kubernetes 部署 SQL Server 高可用性解決方案。
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 09/01/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: c8563738c8d1465c6573ca2a92f0839f54c8e29c
ms.sourcegitcommit: 43b92518c5848489d03c68505bd9905f8686cbc0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/17/2020
ms.locfileid: "92155102"
---
# <a name="deploy-a-sql-server-container-in-kubernetes-with-azure-kubernetes-services-aks"></a>使用 Azure Kubernetes Service (AKS) 在 Kubernetes 中部署 SQL Server 容器

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

了解如何在 Azure Kubernetes Service (AKS) 的 Kubernetes 上設定 SQL Server 執行個體，以提供高可用性 (HA) 的永續性儲存體。 解決方案會提供復原功能。 如果 SQL Server 執行個體失敗，則會在新的 Pod 中自動重新建立 Kubernetes。 Kubernetes 也會針對節點失敗提供復原功能。

本教學課程示範如何在 AKS 的容器中設定高可用性 SQL Server 執行個體。

> [!div class="checklist"]
> * 建立 SA 密碼
> * 建立儲存體
> * 建立部署
> * 使用 SQL Server Management Studio (SSMS) 連線
> * 驗證失敗和復原

## <a name="ha-solution-on-kubernetes-running-in-azure-kubernetes-service"></a>在 Azure Kubernetes Service 中執行的 Kubernetes HA 解決方案

Kubernetes 1.6 和更新版本支援[儲存體類別](https://kubernetes.io/docs/concepts/storage/storage-classes/)、[永續性磁碟區宣告](https://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims)，以及 [Azure 磁碟區類型](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk)。 您可以在 Kubernetes 中以原生方式建立並管理您的 SQL Server 執行個體。 本文中的範例說明如何建立[部署](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)，以達成類似於共用磁碟容錯移轉叢集執行個體的高可用性設定。 在此設定中，Kubernetes 扮演叢集協調器的角色。 當容器中的 SQL Server 執行個體失敗時，協調器會啟動附加至相同永續性儲存體的其他容器執行個體。

![Kubernetes 叢集上的 SQL Server 容器](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

在上圖中，`mssql-server` 是 [Pod](https://kubernetes.io/docs/concepts/workloads/pods/pod/) 中的容器。 Kubernetes 會協調叢集中的資源。 [複本集](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)可確保 Pod 會在節點失敗後自動復原。 應用程式會連線至服務。 在此情況下，服務代表的負載平衡器會在 `mssql-server` 失敗後維持相同 IP 位址。

在下圖中，`mssql-server` 容器已失敗。 作為協調器，Kubernetes 可保證複本集中狀態良好的執行個體正確計數，並根據設定啟動新的容器。 協調器會在相同節點上啟動新的 Pod，而 `mssql-server` 會重新連接到相同的永續性儲存體。 服務會連接到重新建立的 `mssql-server`。

![Kubernetes 叢集上的 SQL Server Pod 失敗](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-pod-fail.png)

在下圖中，裝載 `mssql-server` 容器的節點已失敗。 協調器會在不同節點上啟動新的 Pod，而 `mssql-server` 會重新連接到相同的永續性儲存體。 服務會連接到重新建立的 `mssql-server`。

![Kubernetes 叢集上的 SQL Server Pod 復原](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-node-fail.png)

## <a name="prerequisites"></a>Prerequisites

* **Kubernetes 叢集**
   - 本教學課程需要使用 Kubernetes 叢集。 這些步驟會使用 [kubectl](https://kubernetes.io/docs/user-guide/kubectl/) 來管理叢集。 

   - 請參閱[部署 Azure Kubernetes Service (AKS) 叢集](/azure/aks/tutorial-kubernetes-deploy-cluster)，以使用 `kubectl` 在 AKS 中建立單一節點 Kubernetes 叢集並進行連線。 

   >[!NOTE]
   >為了防止節點失敗，Kubernetes 叢集需要一個以上的節點。

* **Azure CLI 2.0.23**
   - 本教學課程中的指示已經過 Azure CLI 2.0.23 驗證。

## <a name="create-an-sa-password"></a>建立 SA 密碼

在 Kubernetes 叢集中建立 SA 密碼。 Kubernetes 可以管理敏感性設定資訊，例如作為 [Secret](https://kubernetes.io/docs/concepts/configuration/secret/) 的密碼。

下列命令會建立 SA 帳戶的密碼：

   ```azurecli
   kubectl create secret generic mssql --from-literal=SA_PASSWORD="MyC0m9l&xP@ssw0rd"
   ```  

   請將 `MyC0m9l&xP@ssw0rd` 取代為複雜密碼。

   若要在名為 `mssql` 的 Kubernetes 中建立 Secret，以保存 `SA_PASSWORD` 的 `MyC0m9l&xP@ssw0rd` 值，請執行此命令。


## <a name="create-storage"></a>建立儲存體

在 Kubernetes 叢集中，設定[永續性磁碟區](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)和[永續性磁碟區宣告](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistent-volume-claim-protection)。 完成下列步驟： 

1. 建立資訊清單，以定義儲存體類別和永續性磁碟區宣告。  資訊清單會指定儲存體佈建程式、參數和[回收原則](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#reclaiming)。 Kubernetes 叢集會使用這個資訊清單來建立永續性儲存體。 

   下列 YAML 範例會定義儲存體類別和永續性磁碟區宣告。 儲存類別佈建程式是 `azure-disk`，因為此 Kubernetes 叢集位於 Azure 中。 儲存體帳戶類型為 `Standard_LRS`。 永續性磁碟區宣告名為 `mssql-data`。 永續性磁碟區宣告中繼資料包含可將其連接回儲存體類別的注釋。 

   ```yaml
   kind: StorageClass
   apiVersion: storage.k8s.io/v1
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

   儲存檔案 (例如 **pvc.yaml**)。

1. 在 Kubernetes 中建立永續性磁碟區宣告。

   ```azurecli
   kubectl apply -f <Path to pvc.yaml file>
   ```

   `<Path to pvc.yaml file>` 是您儲存檔案的位置。

   系統會自動將永續性磁碟區建立為 Azure 儲存體帳戶，並繫結至永續性磁碟區宣告。 

    ![永續性磁碟區宣告命令的螢幕擷取畫面](media/tutorial-sql-server-containers-kubernetes/02_pvc_cmd.png)

1. 驗證永續性磁碟區宣告。

   ```azurecli
   kubectl describe pvc <PersistentVolumeClaim>
   ```

   `<PersistentVolumeClaim>` 是永續性磁碟區宣告的名稱。

   在先前的步驟中，永續性磁碟區宣告名為 `mssql-data`。 若要查看永續性磁碟區宣告的相關中繼資料，請執行下列命令：

   ```azurecli
   kubectl describe pvc mssql-data
   ```

   所傳回中繼資料包含名為 `Volume` 的值。 這個值會對應至 Blob 的名稱。

   ![傳回的中繼資料 (包括磁碟區) 螢幕擷取畫面](media/tutorial-sql-server-containers-kubernetes/describe-volume.png)

   磁碟區值符合下圖 Azure 入口網站中 Blob 的名稱部分： 

   ![Azure 入口網站 Blob 名稱的螢幕擷取畫面](media/tutorial-sql-server-containers-kubernetes/describe-volume-portal.png)

1. 驗證永續性磁碟區。

   ```azurecli
   kubectl describe pv
   ```

   `kubectl` 會傳回永續性磁碟區 (之前由系統自動建立並繫結至永續性磁碟區宣告) 的相關中繼資料。 

## <a name="create-the-deployment"></a>建立部署

此範例會將裝載 SQL Server 執行個體的容器描述為 Kubernetes 部署物件。 部署會建立複本集。 複本集會建立 Pod。 

在此步驟中，請建立資訊清單，以根據 SQL Server [mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server) Docker 映像來描述容器。 資訊清單會參考 `mssql-server` 永續性磁碟區宣告，以及您已套用至 Kubernetes 叢集的 `mssql` Secret。 資訊清單也會描述[服務](https://kubernetes.io/docs/concepts/services-networking/service/)。 此服務是負載平衡器。 負載平衡器可確保在 SQL Server 執行個體復原之後，IP 位址會持續保留。 

1. 建立資訊清單 (YAML 檔案) 來描述部署。 下列為描述部署的範例，包括以 SQL Server 容器映像為基礎的容器。

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: mssql-deployment
   spec:
     replicas: 1
     selector:
        matchLabels:
          app: mssql
     template:
       metadata:
         labels:
           app: mssql
       spec:
         terminationGracePeriodSeconds: 30
         hostname: mssqlinst
         securityContext:
           fsGroup: 10001
         containers:
         - name: mssql
           image: mcr.microsoft.com/mssql/server:2019-latest
           ports:
           - containerPort: 1433
           env:
           - name: MSSQL_PID
             value: "Developer"
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

   將上述程式碼複製到名為 `sqldeployment.yaml` 的新檔案中。 更新下列值： 

   * MSSQL_PID `value: "Developer"`：設定容器以執行 SQL Server Developer 版本。 Developer 版本未獲授權用於生產環境資料。 如果部署是供生產環境使用，請設定適當的版本 (`Enterprise`、`Standard` 或 `Express`)。 

      >[!NOTE]
      >如需詳細資訊，請參閱[如何授權 SQL Server](https://www.microsoft.com/sql-server/sql-server-2017-pricing)。

   * `persistentVolumeClaim`:此值需要使用與永續性磁碟區宣告所用名稱對應的 `claimName:` 項目。 本教學課程使用 `mssql-data`。 

   * `name: SA_PASSWORD`:設定容器映像以設定 SA 密碼，如本節中所定義。

     ```yaml
     valueFrom:
       secretKeyRef:
         name: mssql
         key: SA_PASSWORD
     ```

    當 Kubernetes 部署容器時，它會參考名為 `mssql` 的 Secret，以取得密碼的值。

   * `securityContext`：securityContext 會定義 Pod 或容器的權限和存取控制設定，在此案例中由於其會在 Pod 層級指定，因此所有容器 (在此案例中只有一個) 都會遵循該安全性內容。 在安全性內容中會使用值 10001 (mssql 群組的 GID) 來定義 fsGroup，這表示容器其所有處理序都是增補群組識別碼 10001 (mssql) 的一部分。 /var/opt/mssql 磁碟區的擁有者和在該磁碟區中所建立任何檔案都會是群組識別碼 10001 (mssql 群組)。

   >[!NOTE]
   >藉由使用 `LoadBalancer` 服務類型，您可以在連接埠 1433 遠端存取 (透過網際網路) SQL Server 執行個體。

   儲存檔案 (例如 **sqldeployment.yaml**)。

1. 建立部署。

   ```azurecli
   kubectl apply -f <Path to sqldeployment.yaml file>
   ```

   `<Path to sqldeployment.yaml file>` 是您儲存檔案的位置。

   ![部署命令的螢幕擷取畫面](media/tutorial-sql-server-containers-kubernetes/04_deploy_cmd.png)

   您已建立部署和服務。 SQL Server 執行個體所在的容器已連線至永續性儲存體。

   若要檢視 Pod 的狀態，請鍵入 `kubectl get pod`。

   ![get pod 命令的螢幕擷取畫面](media/tutorial-sql-server-containers-kubernetes/05_get_pod_cmd.png)

   在上圖中，Pod 的狀態為 `Running`。 此狀態表示容器已就緒。 這可能需要幾分鐘的時間。

   >[!NOTE]
   >建立部署之後，可能需要幾分鐘的時間才能顯示 Pod。 因為叢集是從 Docker Hub 提取 [mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server) 映像，所以會導致這個延遲。 第一次提取映像之後，如果部署抵達的節點中已經快取映像，則後續部署可能會更快速。 

1. 驗證服務是否正在執行。 執行以下命令：

   ```azurecli
   kubectl get services 
   ```

   此命令會傳回正在執行的服務，以及服務的內部和外部 IP 位址。 記下 `mssql-deployment` 服務的外部 IP 位址。 使用此 IP 位址連接到 SQL Server。 

   ![get service 命令的螢幕擷取畫面](media/tutorial-sql-server-containers-kubernetes/06_get_service_cmd.png)

   如需 Kubernetes 叢集中的物件狀態詳細資訊，請執行：

   ```azurecli
   az aks browse --resource-group <MyResourceGroup> --name <MyKubernetesClustername>
   ```

1. 您也可以透過執行下列命令來驗證容器是以非根使用者的身分執行：

    ```azurecli
    kubectl.exe exec <name of SQL POD> -it -- /bin/bash 
    ```

    然後執行 'whoami'，即應看到使用者名稱為 mssql。 這是非根使用者。

    ```azurecli
    whoami
    ```

## <a name="connect-to-the-sql-server-instance"></a>連接到 SQL Server 執行個體

如果您已如所述設定容器，即可從 Azure 虛擬網路外部連線到應用程式。 使用 `sa` 帳戶和服務的外部 IP 位址。 使用您設定為 Kubernetes Secret 的密碼。 

您可以使用下列應用程式來連接到 SQL Server 執行個體。 

* [SSMS](./sql-server-linux-manage-ssms.md)

* [SSDT](./sql-server-linux-develop-use-ssdt.md)

* sqlcmd

   若要與 `sqlcmd` 連線，請執行下列命令：

   ```cmd
   sqlcmd -S <External IP Address> -U sa -P "MyC0m9l&xP@ssw0rd"
   ```

   取代下列值：

  * 將 `<External IP Address>` 取代為 `mssql-deployment` 服務的 IP 位址 
  * 將 `MyC0m9l&xP@ssw0rd` 取代為您的密碼

## <a name="verify-failure-and-recovery"></a>驗證失敗和復原

若要驗證失敗和復原，您可以刪除 Pod。 請執行下列步驟：

1. 列出執行 SQL Server 的 Pod。

   ```azurecli
   kubectl get pods
   ```

   記下執行 SQL Server 的 Pod 名稱。

1. 刪除 Pod。

   ```azurecli
   kubectl delete pod mssql-deployment-0
   ```

   `mssql-deployment-0` 即為上一個步驟傳回的 Pod 名稱值。 

Kubernetes 會自動重新建立 Pod，以復原 SQL Server 執行個體，並連接永續性儲存體。 使用 `kubectl get pods` 來驗證是否已部署新的 Pod。 使用 `kubectl get services` 來驗證新容器的 IP 位址是否相同。 

## <a name="summary"></a>摘要

在這個教學課程中，您已了解如何將 SQL Server 容器部署至 Kubernetes 叢集以確保高可用性。 

> [!div class="checklist"]
> * 建立 SA 密碼
> * 建立儲存體
> * 建立部署
> * 使用 SQL Server Management Studio (SSMS) 連線
> * 驗證失敗和復原

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
>[Kubernetes 簡介](/azure/aks/intro-kubernetes)
