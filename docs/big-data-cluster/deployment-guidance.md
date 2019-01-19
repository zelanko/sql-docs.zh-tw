---
title: 如何部署
titleSuffix: SQL Server 2019 big data clusters
description: 了解如何部署在 Kubernetes 上的 SQL Server 2019 巨量資料叢集 （預覽）。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/07/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 900bd5fea075e304dae73a20168da952433f20be
ms.sourcegitcommit: 2e8783e6bedd9597207180941be978f65c2c2a2d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2019
ms.locfileid: "54405818"
---
# <a name="how-to-deploy-sql-server-big-data-clusters-on-kubernetes"></a>如何部署 SQL Server 在 Kubernetes 上的巨量資料叢集

SQL Server 的巨量資料叢集可以部署為 docker 容器的 Kubernetes 叢集。 這是安裝和設定步驟的概觀：

- 設定在單一 VM 的 Vm，或在 Azure Kubernetes Service (AKS) 叢集上的 Kubernetes 叢集。
- 安裝叢集的設定工具**mssqlctl**用戶端電腦上。
- 部署 SQL Server 在 Kubernetes 叢集中的巨量資料叢集。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="prereqs"></a> Kubernetes 叢集的先決條件

SQL Server 的巨量資料叢集至少需要的最小的 Kubernetes 版本 v1.10 伺服器和用戶端 (kubectl)。

> [!NOTE]
> 請注意，用戶端和伺服器的 Kubernetes 版本應該是 + 1，則為-1 的次要版本。 如需詳細資訊，請參閱 < [Kubernetes 支援的版本和元件扭曲](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew)。

## <a id="kubernetes"></a> Kubernetes 叢集設定

如果您已經有符合上述必要條件，Kubernetes 叢集，則您可以直接跳到[部署步驟](#deploy)。 本節假設 Kubernetes 概念的基本知識。  如需 Kubernetes 的詳細資訊，請參閱[Kubernetes 文件](https://kubernetes.io/docs/home)。

您可以選擇部署 Kubernetes 中任何一種方式：

| 部署 Kubernetes 上： | 描述 | 連結 |
|---|---|---|
| **Minikube** | 在 VM 中單一節點 Kubernetes 叢集。 | [指示](deploy-on-minikube.md) |
| **Azure Kubernetes 服務 (AKS)** | 在 Azure 中受控的 Kubernetes 容器服務。 | [指示](deploy-on-aks.md) |
| **多部電腦** | 部署實體或虛擬機器上的 Kubernetes 叢集**kubeadm** | [指示](deploy-with-kubeadm.md) |
  
> [!TIP]
> 部署 AKS 和 SQL Server 的巨量資料叢集的範例 python 指令碼，請參閱[部署巨量資料叢集的 Azure Kubernetes Service (AKS) 上的 SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/aks)。

## <a name="deploy-sql-server-2019-big-data-tools"></a>部署 SQL Server 2019 巨量資料工具

第一次部署 SQL Server 2019 巨量資料叢集之前[安裝的巨量資料 」 工具](deploy-big-data-tools.md):
- **mssqlctl**
- **kubectl**
- **Azure Data Studio**
- **SQL Server 2019 延伸模組**

## <a id="deploy"></a> 部署 SQL Server 的巨量資料叢集

您已設定您的 Kubernetes 叢集之後，您可以繼續使用巨量資料的 SQL Server 叢集的部署。 

> [!NOTE]
> 如果您要從舊版升級，請參閱[升級一節](#upgrade)。

若要部署的開發/測試環境的所有預設設定在 Azure 中的巨量資料叢集，請遵循這篇文章中的指示：

[快速入門：部署在 Kubernetes 上的 SQL Server 巨量資料叢集](quickstart-big-data-cluster-deploy.md)

如果您想要自訂您的巨量資料叢集，根據您的工作負載的部署需求，請依照這篇文章其餘部分的指示。

## <a name="verify-kubernetes-configuration"></a>確認 kubernetes 組態

執行**kubectl**命令來檢視叢集組態。 請確定該 kubectl 指向正確的叢集內容。

```bash
kubectl config view
```

## <a id="env"></a> 定義環境變數

可以使用一組環境變數傳遞給自訂叢集設定`mssqlctl create cluster`命令。 大部分的環境變數是使用如下的預設值為每個選擇性的。 請注意，環境變數，例如需要使用者輸入的認證。

| 環境變數 | 必要項 | 預設值 | 描述 |
|---|---|---|---|
| **ACCEPT_EULA** | 是 | N/A | 接受 SQL Server 授權合約 (例如，' Y')。  |
| **CLUSTER_NAME** | 是 | N/A | 若要部署到叢集的巨量資料的 sql Server 的 Kubernetes 命名空間名稱。 |
| **CLUSTER_PLATFORM** | 是 | N/A | 部署 Kubernetes 叢集平台。 可以是`aks`， `minikube`， `kubernetes`|
| **CLUSTER_COMPUTE_POOL_REPLICAS** | 否 | 1 | 若要建置的計算集區複本數目。在允許的 CTP 2.2 只有值為 1。 |
| **CLUSTER_DATA_POOL_REPLICAS** | 否 | 2 | 數目的資料集區來建置的複本。 |
| **CLUSTER_STORAGE_POOL_REPLICAS** | 否 | 2 | 若要建置的儲存體集區複本數目。 |
| **DOCKER_REGISTRY** | 是 | TBD | 私用登錄中儲存用來部署叢集的映像。 |
| **DOCKER_REPOSITORY** | 是 | TBD | 上述的登錄，影像都會儲存在私人存放庫。  它是需要閘道公開預覽版的持續期間。 |
| **DOCKER_USERNAME** | 是 | N/A | 存取容器映像，如果它們儲存在私人存放庫的使用者名稱。 它是需要閘道公開預覽版的持續期間。 |
| **DOCKER_PASSWORD** | 是 | N/A | 存取上述的私人存放庫的密碼。 它是需要閘道公開預覽版的持續期間。|
| **DOCKER_EMAIL** | 是 | N/A | 上述的私人存放庫相關聯的電子郵件。 它是必要的閘道的私人預覽期間。 |
| **DOCKER_IMAGE_TAG** | 否 | 最新 | 用來標記映像的標籤。 |
| **DOCKER_IMAGE_POLICY** | 否 | 永遠 | 永遠強制映像提取。  |
| **DOCKER_PRIVATE_REGISTRY** | 是 | 1 | 閘道的公開預覽版的時間範圍，這個值必須設為 1。 |
| **CONTROLLER_USERNAME** | 是 | N/A | 針對叢集系統管理員使用者名稱。 |
| **CONTROLLER_PASSWORD** | 是 | N/A | 針對叢集系統管理員密碼。 |
| **KNOX_PASSWORD** | 是 | N/A | Knox 使用者的密碼。 |
| **MSSQL_SA_PASSWORD** | 是 | N/A | SQL master 執行個體的 SA 使用者的密碼。 |
| **USE_PERSISTENT_VOLUME** | 否 | true | `true` 若要使用 Kubernetes 永續性磁碟區宣告 pod 儲存體。  `false` 要用於 pod 儲存體中的暫時主機儲存體。 請參閱[資料持續性](concept-data-persistence.md)文章以取得詳細資料。 如果您部署在 minikube 叢集化巨量資料的 SQL Server 和 USE_PERSISTENT_VOLUME = true，您必須設定的值`STORAGE_CLASS_NAME=standard`。 |
| **STORAGE_CLASS_NAME** | 否 | 預設 | 如果`USE_PERSISTENT_VOLUME`是`true`這表示 Kubernetes 儲存體類別使用的名稱。 請參閱[資料持續性](concept-data-persistence.md)文章以取得詳細資料。 如果您部署在 minikube 叢集化巨量資料的 SQL Server 時，預設儲存體類別名稱都不同，您必須藉由設定覆寫它`STORAGE_CLASS_NAME=standard`。 |
| **MASTER_SQL_PORT** | 否 | 31433 | 主要的 SQL 執行個體接聽公用網路的 TCP/IP 通訊埠。 |
| **KNOX_PORT** | 否 | 30443 | 公用網路的 Apache Knox 接聽的 TCP/IP 通訊埠。 |
| **GRAFANA_PORT** | 否 | 30888 | 公用網路的 Grafana 監視應用程式會接聽 TCP/IP 通訊埠。 |
| **KIBANA_PORT** | 否 | 30999 | 公用網路的 Kibana 的記錄檔搜尋應用程式會接聽 TCP/IP 通訊埠。 |

> [!IMPORTANT]
>1. 在有限的私人預覽期間，私用 Docker 登錄的認證會提供給您時分級您[EAP 註冊](https://aka.ms/eapsignup)。
>1. 對於使用內建的內部部署叢集**kubeadm**，環境變數的值`CLUSTER_PLATFORM`是`kubernetes`。 也，當`USE_PERSISTENT_VOLUME=true`，您必須預先佈建 Kubernetes 儲存體類別，並將它傳遞到使用`STORAGE_CLASS_NAME`。
>1. 請確定您將包裝密碼雙引號括住，如果它包含任何特殊字元。 您可以設定 MSSQL_SA_PASSWORD 為任何您喜歡，但請確定它們已夠複雜，而且不使用`!`，`&`或`'`字元。 請注意，雙引號括住分隔符號僅適用於 bash 命令。
>1. 您名稱必須是叢集的只有大小寫英數字元，不含空格。 所有 Kubernetes 成品容器、 pod，具狀態設定 （服務） 叢集將會都建立與叢集名稱相同的命名空間中指定的名稱。
>1. **SA**帳戶是在安裝期間建立的 SQL Server Master 執行個體上的系統管理員。 建立您的 SQL Server 容器，您所指定的 MSSQL_SA_PASSWORD 環境變數設定為可探索執行後回應在容器中的 $MSSQL_SA_PASSWORD。 基於安全考量，變更您的 SA 密碼，根據所述的最佳作法[此處](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker?view=sql-server-2017#change-the-sa-password)。

設定部署巨量資料叢集所需的環境變數，端視您是否使用 Windows 或 Linux 用戶端而有所不同。  選擇執行下列步驟根據哪一個作業系統使用。

初始化下列環境變數，它們也需要部署叢集：

### <a name="windows"></a>視窗

使用命令提示字元 視窗 (非 PowerShell)，設定下列環境變數。 請勿使用引號括住的值。

```cmd
SET ACCEPT_EULA=Y
SET CLUSTER_PLATFORM=<minikube or aks or kubernetes>

SET CONTROLLER_USERNAME=<controller_admin_name - can be anything>
SET CONTROLLER_PASSWORD=<controller_admin_password - can be anything, password complexity compliant>
SET KNOX_PASSWORD=<knox_password - can be anything, password complexity compliant>
SET MSSQL_SA_PASSWORD=<sa_password_of_master_sql_instance, password complexity compliant>

SET DOCKER_REGISTRY=private-repo.microsoft.com
SET DOCKER_REPOSITORY=mssql-private-preview
SET DOCKER_USERNAME=<your username, credentials provided by Microsoft>
SET DOCKER_PASSWORD=<your password, credentials provided by Microsoft>
SET DOCKER_EMAIL=<your Docker email, use the username provided by Microsoft>
SET DOCKER_PRIVATE_REGISTRY="1"
```

### <a name="linux"></a>Linux

初始化下列環境變數。 在 bash 中，您可以使用用引號括住每個值。

```bash
export ACCEPT_EULA=Y
export CLUSTER_PLATFORM=<minikube or aks or kubernetes>

export CONTROLLER_USERNAME="<controller_admin_name - can be anything>"
export CONTROLLER_PASSWORD="<controller_admin_password - can be anything, password complexity compliant>"
export KNOX_PASSWORD="<knox_password - can be anything, password complexity compliant>"
export MSSQL_SA_PASSWORD="<sa_password_of_master_sql_instance, password complexity compliant>"

export DOCKER_REGISTRY="private-repo.microsoft.com"
export DOCKER_REPOSITORY="mssql-private-preview"
export DOCKER_USERNAME="<your username, credentials provided by Microsoft>"
export DOCKER_PASSWORD="<your password, credentials provided by Microsoft>"
export DOCKER_EMAIL="<your Docker email, use the username provided by Microsoft>"
export DOCKER_PRIVATE_REGISTRY="1"
```

### <a name="minikube-settings"></a>Minikube 設定

如果您要部署在 minikube 並`USE_PERSISTENT_VOLUME=true`（預設值），您也必須覆寫的預設值為`STORAGE_CLASS_NAME`環境變數。

使用下列命令在 Windows 上，minikube 部署：

```cmd
SET STORAGE_CLASS_NAME=standard
```

Minikube 部署，在 Linux 上使用下列命令：

```bash
export STORAGE_CLASS_NAME=standard
```

或者，您可以隱藏設定永續性磁碟區使用 minikube `USE_PERSISTENT_VOLUME=false`。

### <a name="kubadm-settings"></a>Kubadm 設定

如果您使用您自己的實體或虛擬機器上的 kubeadm 部署，您必須預先佈建 Kubernetes 儲存體類別，並將它傳遞到使用`STORAGE_CLASS_NAME`。 或者，您可以隱藏使用永續性磁碟區，藉由設定`USE_PERSISTENT_VOLUME=false`。 如需永續性儲存體的詳細資訊，請參閱[巨量資料叢集的 Kubernetes 上的 SQL server 的資料持續性](concept-data-persistence.md)。

## <a name="deploy-sql-server-big-data-cluster"></a>部署 SQL Server 巨量資料叢集

建立叢集 API 用來初始化 Kubernetes 命名空間，並部署到命名空間的所有應用程式 pod。 若要部署 Kubernetes 叢集上的 SQL Server 巨量資料叢集，請執行下列命令：

```bash
mssqlctl create cluster <your-cluster-name>
```

在叢集啟動程序，用戶端的 [命令] 視窗會將輸出的部署狀態。 在部署過程中，您應該會看到一系列的訊息，它正在等候控制器 pod:

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

在 10 到 20 分鐘後應該會通知您正在執行控制器 pod:

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.222.222.222:30080
```

> [!IMPORTANT]
> 整個部署可能需要很長的時間，因為下載的巨量資料叢集元件的容器映像所需的時間。 不過，它應該不需要數小時。 如果您遇到部署問題，請參閱[疑難排解](#troubleshoot)本文以了解如何監視，並檢查部署一節。

部署完成時，輸出會通知您成功：

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

## <a id="masterip"></a> 取得 SQL Server Master 執行個體和 SQL Server 巨量資料叢集 IP 位址

部署指令碼已順利完成之後，您可以取得使用下面所述的步驟在 SQL Server 主要執行個體的 IP 位址。 您將使用此 IP 位址和連接埠號碼 31433 連接到 SQL Server 的主要執行個體 (例如：  **\<ip 位址\>31433、**)。 同樣地，針對 SQL Server 的巨量資料叢集 IP。 所有的叢集端點所述在 叢集系統管理網站的 服務端點 索引標籤。 您可以使用叢集系統管理入口網站來監視部署。 您可以存取入口網站中使用的外部 IP 位址和連接埠號碼`service-proxy-lb`(例如： **https://\<ip 位址\>: 30777/入口網站**)。 認證為存取管理員入口網站的值`CONTROLLER_USERNAME`和`CONTROLLER_PASSWORD`上面提供的環境變數。

### <a name="aks"></a>AKS

如果您使用 AKS，Azure 會提供 Azure 負載平衡器服務。 執行下列命令：

```bash
kubectl get svc endpoint-master-pool -n <your-cluster-name>
kubectl get svc service-security-lb -n <your-cluster-name>
kubectl get svc service-proxy-lb -n <your-cluster-name>
```

尋求**EXTERNAL-IP**值，指派給服務。 然後，連接到 SQL Server 主要執行個體連接埠 31433 使用的 IP 位址 (例如：  **\<ip 位址\>、 31433**) 和 SQL Server 使用的外部 IP 的巨量資料叢集端點`service-security-lb`服務。 

### <a name="minikube"></a>Minikube

如果您使用 Minikube，您需要執行下列命令來取得 IP 位址需要連線到。 除了 IP，指定您要連接到端點的連接埠。 若要取得的所有服務端點 

```bash
minikube ip
```

無論平台 Kubernetes 叢集上執行，以取得部署的叢集，請執行下列命令的所有服務端點：
```bash
kubectl get svc -n <your-cluster-name>
```

## <a id="upgrade"></a> 升級至新的版本

目前，巨量資料叢集升級至新版本的唯一方式是以手動方式移除並重新建立叢集。 每個版本具有的唯一版本**mssqlctl**不與舊版相容。 此外，如果較舊的叢集，就必須下載新的節點上的影像，最新的映像可能無法相容於舊叢集上的映像。 若要升級至最新版本時，使用下列步驟：

1. 然後再刪除舊的叢集，請 HDFS 和 SQL Server 的主要執行個體上備份資料。 SQL Server 的主要執行個體，您可以使用[SQL Server 備份及還原](data-ingestion-restore-database.md)。 HDFS 中，為您[可以複製的資料與**curl**](data-ingestion-curl.md)。

1. 刪除舊的叢集使用`mssqlctl delete cluster`命令。

   ```bash
    mssqlctl delete cluster <old-cluster-name>
   ```

1. 安裝最新版**mssqlctl**。
   
   ```bash
   pip3 install --extra-index-url https://private-repo.microsoft.com/python/ctp-2.2 mssqlctl
   ```

   > [!IMPORTANT]
   > 每個發行的路徑**mssqlctl**變更。 即使您先前已安裝**mssqlctl**，您必須建立新的叢集之前重新安裝最新的路徑。

1. 安裝最新版的使用中的指示[部署區段](#deploy)這篇文章。 

## <a id="troubleshoot"></a> 監視和疑難排解

若要監視，或針對部署進行疑難排解，請使用**kubectl**檢查叢集狀態，並偵測潛在的問題。 在部署期間的任何時間，您可以開啟不同的命令視窗執行下列測試。

1. 檢查您的叢集中的 pod 的狀態。

   ```cmd
   kubectl get pods -n <your-cluster-name>
   ```

   在部署期間，pod 數與**狀態**的**ContainerCreating**仍即將推出。 如果部署停止回應，因為任何原因，這可讓您了解可能的問題。 也看看**準備**資料行。 這會告訴您的 pod 中啟動多少容器。 請注意，部署可能需要 30 分鐘以上，取決於您的組態和網路。 這個時間大部分都是花在下載不同元件的容器映像。 下表顯示在部署期間的兩個容器的編輯的範例輸出：

   ```output
   PS C:\> kubectl get pods -n sbdc8
   NAME                                     READY   STATUS              RESTARTS   AGE
   mssql-controller-h79ft                   4/4     Running             0          13m
   mssql-storage-pool-default-0             0/7     ContainerCreating   0          6m
   ```

1. 說明個別的 pod，如需詳細資訊。 下列命令會檢查`mssql-storage-pool-default-0`pod。

   ```cmd
   kubectl describe pod mssql-storage-pool-default-0 -n <your-cluster-name>
   ```

   這會輸出 pod，包括最新事件的詳細的資訊。 如果發生錯誤，您有時可能會找到的錯誤。

1. 擷取執行的 pod 中容器的記錄檔。 下列命令會擷取名為 pod 中執行的所有容器的記錄檔`mssql-storage-pool-default-0`並將其輸出的檔案名稱`pod-logs.txt`:

   ```cmd
   kubectl logs mssql-storage-pool-default-0 --all-containers=true -n <your-cluster-name> > pod-logs.txt
   ```

1. 使用下列命令部署期間及之後，請檢閱叢集服務：

   ```cmd
   kubectl get svc -n <your-cluster-name>
   ```

   這些服務支援巨量資料叢集內部和外部連接。 對於外部連線，請使用下列服務：

   | 服務 | 描述 |
   |---|---|
   | **endpoint-master-pool** | 提供存取權的主要執行個體。<br/>(**EXTERNAL-IP，31433**並**SA**使用者) |
   | **service-mssql-controller-lb**<br/>**service-mssql-controller-nodeport** | 支援工具和管理叢集的用戶端。 |
   | **service-proxy-lb**<br/>**service-proxy-nodeport** | 提供存取權[叢集管理網站](cluster-admin-portal.md)。<br/>(https://**EXTERNAL-IP**: 30777/入口網站)|
   | **service-security-lb**<br/>**service-security-nodeport** | 可存取 HDFS/Spark 閘道。<br/>(**EXTERNAL-IP**並**根**使用者) |

   > [!NOTE]
   > 根據您的 Kubernetes 環境而有所不同的服務名稱。 在部署 Azure Kubernetes Service (AKS) 上，服務名稱結尾 **-l b**。Minikube 和 kubeadm 部署的服務名稱的結尾 **-nodeport**。

1. 使用[叢集系統管理入口網站](cluster-admin-portal.md)若要監視部署上**部署** 索引標籤。您必須等到**lb-proxy 服務-** 服務存取此入口網站，讓其無法在部署開始之前啟動。

> [!TIP]
> 如需有關如何疑難排解在叢集的詳細資訊，請參閱[進行監視和疑難排解 SQL Server 的巨量資料叢集的 Kubectl 命令](cluster-troubleshooting-commands.md)。

## <a name="next-steps"></a>後續步驟

試試看一些新功能，並了解[如何在 SQL Server 2019 預覽中使用 notebook](notebooks-guidance.md)。
