---
title: 如何部署 SQL Server 的巨量資料叢集的 Kubernetes |Microsoft Docs
description: 了解如何部署在 Kubernetes 上的 SQL Server 2019 巨量資料叢集 （預覽）。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/08/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: de19577b4a83bc10875bf56f4c0f2924828a00ea
ms.sourcegitcommit: 182d77997133a6e4ee71e7a64b4eed6609da0fba
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2018
ms.locfileid: "50051180"
---
# <a name="how-to-deploy-sql-server-big-data-cluster-on-kubernetes"></a>如何部署巨量資料叢集的 Kubernetes 的 SQL Server

SQL Server 的巨量資料叢集可以部署為 docker 容器的 Kubernetes 叢集。 這是安裝和設定步驟的概觀：

- 設定在單一 VM 的 Vm，或在 Azure Kubernetes Service (AKS) 叢集上的 Kubernetes 叢集。
- 安裝叢集的設定工具**mssqlctl**用戶端電腦上。
- 部署 SQL Server 在 Kubernetes 叢集中的巨量資料叢集。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="prereqs"></a> Kubernetes 叢集的先決條件

SQL Server 的巨量資料叢集需要最小 v1.10 版本，如 Kubernetes、 伺服器和用戶端。 若要安裝 kubectl 用戶端上的特定版本，請參閱[安裝 kubectl 二進位透過 curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl)。  最新版的 minikube 和 AKS 是至少 1.10。 Aks，您必須使用`--kubernetes-version`參數來指定預設值不同的版本。

> [!NOTE]
> 請注意，用戶端和伺服器的 Kubernetes 版本應該是 + 1，則為-1 的次要版本。 如需詳細資訊，請參閱 < [Kubernetes 支援的版本和元件扭曲](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew)。

## <a id="kubernetes"></a> Kubernetes 叢集設定

如果您已經有符合上述必要條件，Kubernetes 叢集，則您可以直接跳到[部署步驟](#deploy)。 本節假設 Kubernetes 概念的基本知識。  如需 Kubernetes 的詳細資訊，請參閱[Kubernetes 文件](https://kubernetes.io/docs/home)。

您可以選擇部署 Kubernetes 中任何一種方式：

| 部署 Kubernetes 上： | 描述 |
|---|---|
| **Minikube** | 在 VM 中單一節點 Kubernetes 叢集。 |
| **Azure Kubernetes 服務 (AKS)** | 在 Azure 中受控的 Kubernetes 容器服務。 |
| **多部電腦** | 部署實體或虛擬機器上的 Kubernetes 叢集**kubeadm** |

設定其中一個 SQL Server 的巨量資料叢集的 Kubernetes 叢集選項的指引，請參閱下列文章：

   - [設定 Minikube](deploy-on-minikube.md)
   - [設定 Azure Kubernetes Service 上的 Kubernetes](deploy-on-aks.md)
   - [設定與 kubeadm 的多部電腦上的 Kubernetes](deploy-with-kubeadm.md)
   
> [!TIP]
> 部署 AKS 和 SQL Server 的巨量資料叢集的範例 python 指令碼，請參閱[部署巨量資料叢集的 Azure Kubernetes Service (AKS) 上的 SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/aks)。

## <a id="deploy"></a> 部署 SQL Server 的巨量資料叢集

您已設定您的 Kubernetes 叢集之後，您可以繼續使用巨量資料的 SQL Server 叢集的部署。 若要部署的開發/測試環境的所有預設設定在 Azure 中的巨量資料叢集，請遵循這篇文章中的指示：

[快速入門： 部署 Kubernetes 上的 SQL Server 巨量資料叢集](quickstart-big-data-cluster-deploy.md)

如果您想要自訂您的巨量資料叢集組態，根據您的工作負載需求，請遵循下的一組指示。

## <a name="verify-kubernetes-configuration"></a>確認 kubernetes 組態

執行**kubectl**命令來檢視叢集組態。 請確定該 kubectl 指向正確的叢集內容。

```bash
kubectl config view
```

## <a id="mssqlctl"></a> 安裝 mssqlctl

**mssqlctl**是命令列公用程式，可讓叢集系統管理員啟動及管理巨量資料叢集，透過 REST Api 以 Python 所撰寫。 最小所需的 Python 版本為 3.5 版。 您也必須擁有`pip`用來下載並安裝**mssqlctl**工具。 

### <a name="windows-mssqlctl-installation"></a>Windows mssqlctl 安裝

1. Windows 用戶端上下載所需的 Python 套件，從[ https://www.python.org/downloads/ ](https://www.python.org/downloads/)。 Python3.5.3 和更新版本，則當您安裝 Python 時也會安裝 pip3。 

   > [!TIP] 
   > 當安裝 Python3，選取要將 Python 新增至您的路徑。 如果您不這樣做，您可以稍後找出 pip3 所在的位置，並以手動方式將它新增至您的路徑。

1. 請確定您有最新**要求**封裝。

   ```cmd
   python -m pip install requests
   python -m pip install requests --upgrade
   ```

1. 安裝**mssqlctl**使用下列命令：

   ```bash
   pip3 install --index-url https://private-repo.microsoft.com/python/ctp-2.0 mssqlctl
   ```

### <a name="linux-mssqlctl-installation"></a>Linux mssqlctl 安裝

在 Linux 上，您必須安裝**python3**並**python3-pip**封裝，然後執行`sudo pip3 install --upgrade pip`。 這會安裝 Python 和 pip 的最新的 3.5 版。 下列範例示範這些命令會適用於 Ubuntu 的運作方式 （如果您使用另一個平台，修改命令的套件管理員）：

1. 安裝所需的 Python 套件：

   ```bash
   sudo apt-get update && /
   sudo apt-get install -y python3 && /
   sudo apt-get install -y python3-pip && /
   sudo -H pip3 install --upgrade pip
   ```

1. 請確定您有最新**要求**封裝。

   ```bash
   sudo -H python3 -m pip install requests
   sudo -H python3 -m pip install requests --upgrade
   ```

1. 安裝**mssqlctl**使用下列命令：

   ```bash
   pip3 install --index-url https://private-repo.microsoft.com/python/ctp-2.0 mssqlctl
   ```

## <a name="define-environment-variables"></a>定義環境變數

可以使用一組環境變數傳遞給自訂叢集設定`mssqlctl create cluster`命令。 大部分的環境變數是使用如下的預設值為每個選擇性的。 請注意，環境變數，例如需要使用者輸入的認證。

| 環境變數 | 必要項 | 預設值 | 描述 |
|---|---|---|---|
| **ACCEPT_EULA** | 是 | 不適用 | 接受 SQL Server 授權合約 (例如，' Y')。  |
| **CLUSTER_NAME** | 是 | 不適用 | 若要部署到叢集的巨量資料的 sql Server 的 Kubernetes 命名空間名稱。 |
| **CLUSTER_PLATFORM** | 是 | 不適用 | 部署 Kubernetes 叢集平台。 可以是`aks`， `minikube`， `kubernetes`|
| **CLUSTER_COMPUTE_POOL_REPLICAS** | 否 | 1 | 若要建置的計算集區複本數目。在 CTP2.0 只值允許為 1。 |
| **CLUSTER_DATA_POOL_REPLICAS** | 否 | 2 | 數目的資料集區來建置的複本。 |
| **CLUSTER_STORAGE_POOL_REPLICAS** | 否 | 2 | 若要建置的儲存體集區複本數目。 |
| **DOCKER_REGISTRY** | 是 | TBD | 私用登錄中儲存用來部署叢集的映像。 |
| **DOCKER_REPOSITORY** | 是 | TBD | 上述的登錄，影像都會儲存在私人存放庫。  它是需要閘道公開預覽版的持續期間。 |
| **DOCKER_USERNAME** | 是 | 不適用 | 存取容器映像，如果它們儲存在私人存放庫的使用者名稱。 它是需要閘道公開預覽版的持續期間。 |
| **DOCKER_PASSWORD** | 是 | 不適用 | 存取上述的私人存放庫的密碼。 它是需要閘道公開預覽版的持續期間。|
| **DOCKER_EMAIL** | 是 | 不適用 | 上述的私人存放庫相關聯的電子郵件。 它是必要的閘道的私人預覽期間。 |
| **DOCKER_IMAGE_TAG** | 否 | 最新 | 用來標記映像的標籤。 |
| **DOCKER_IMAGE_POLICY** | 否 | 永遠 | 永遠強制映像提取。  |
| **DOCKER_PRIVATE_REGISTRY** | 是 | 1 | 閘道的公開預覽版的時間範圍，這個值必須設為 1。 |
| **CONTROLLER_USERNAME** | 是 | 不適用 | 針對叢集系統管理員使用者名稱。 |
| **CONTROLLER_PASSWORD** | 是 | 不適用 | 針對叢集系統管理員密碼。 |
| **KNOX_PASSWORD** | 是 | 不適用 | Knox 使用者的密碼。 |
| **MSSQL_SA_PASSWORD** | 是 | 不適用 | SQL master 執行個體的 SA 使用者的密碼。 |
| **USE_PERSISTENT_VOLUME** | 否 | true | `true` 若要使用 Kubernetes 永續性磁碟區宣告 pod 儲存體。  `false` 要用於 pod 儲存體中的暫時主機儲存體。 請參閱[資料持續性](concept-data-persistence.md)文章以取得詳細資料。 如果您部署在 minikube 叢集化巨量資料的 SQL Server 和 USE_PERSISTENT_VOLUME = true，您必須設定的值`STORAGE_CLASS_NAME=standard`。 |
| **STORAGE_CLASS_NAME** | 否 | 預設 | 如果`USE_PERSISTENT_VOLUME`是`true`這表示 Kubernetes 儲存體類別使用的名稱。 請參閱[資料持續性](concept-data-persistence.md)文章以取得詳細資料。 如果您部署在 minikube 叢集化巨量資料的 SQL Server 時，預設儲存體類別名稱都不同，您必須藉由設定覆寫它`STORAGE_CLASS_NAME=standard`。 |
| **MASTER_SQL_PORT** | 否 | 31433 | 主要的 SQL 執行個體接聽公用網路的 TCP/IP 通訊埠。 |
| **KNOX_PORT** | 否 | 30443 | 公用網路的 Apache Knox 接聽的 TCP/IP 通訊埠。 |
| **GRAFANA_PORT** | 否 | 30888 | 公用網路的 Grafana 監視應用程式會接聽 TCP/IP 通訊埠。 |
| **KIBANA_PORT** | 否 | 30999 | 公用網路的 Kibana 的記錄檔搜尋應用程式會接聽 TCP/IP 通訊埠。 |

> [!IMPORTANT]
>1. 在有限的私人預覽期間，私用 Docker 登錄的認證會提供給您時分級您[EAP 註冊](https://aka.ms/eapsignup)。
>1. 對於使用內建的內部部署叢集**kubeadm**，環境變數的值`CLUSTER_PLATFORM`是`kubernetes`。 也，當`USE_PERSISTENT_VOLUME=true`，您必須預先佈建 Kubernetes 儲存體類別，並將它傳遞到使用`STORAGE_CLASS_NAME`。
>1. 請確定您將包裝密碼雙引號括住，如果它包含任何特殊字元。 您可以設定 MSSQL_SA_PASSWORD 為任何您喜歡，但請確定它們已夠複雜，而且不使用`!`，`&`或`‘`字元。 請注意，雙引號括住分隔符號僅適用於 bash 命令。
>1. 您名稱必須是叢集的只有大小寫英數字元，不含空格。 所有 Kubernetes 成品容器、 pod，具狀態設定 （服務） 叢集將會都建立與叢集名稱相同的命名空間中指定的名稱。
>1. **SA**帳戶是在安裝期間建立的 SQL Server Master 執行個體上的系統管理員。 建立您的 SQL Server 容器，您所指定的 MSSQL_SA_PASSWORD 環境變數設定為可探索執行後回應在容器中的 $MSSQL_SA_PASSWORD。 基於安全考量，變更您的 SA 密碼，根據所述的最佳作法[此處](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker?view=sql-server-2017#change-the-sa-password)。

設定部署巨量資料叢集所需的環境變數，端視您是否使用 Windows 或 Linux 用戶端而有所不同。  選擇執行下列步驟根據哪一個作業系統使用。

初始化下列環境變數，它們也需要部署叢集：

### <a name="windows"></a>Windows

使用命令提示字元 視窗 (非 PowerShell)，設定下列環境變數。 請勿使用引號括住的值。

```cmd
SET ACCEPT_EULA=Y
SET CLUSTER_PLATFORM=<minikube or aks or kubernetes>

SET CONTROLLER_USERNAME=<controller_admin_name – can be anything>
SET CONTROLLER_PASSWORD=<controller_admin_password – can be anything, password complexity compliant>
SET KNOX_PASSWORD=<knox_password – can be anything, password complexity compliant>
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

export CONTROLLER_USERNAME="<controller_admin_name – can be anything>"
export CONTROLLER_PASSWORD="<controller_admin_password – can be anything, password complexity compliant>"
export KNOX_PASSWORD="<knox_password – can be anything, password complexity compliant>"
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

## <a name="deploy-sql-server-big-data-cluster"></a>部署 SQL Server 的巨量資料叢集

建立叢集 API 用來初始化 Kubernetes 命名空間，並部署到命名空間的所有應用程式 pod。 若要部署 Kubernetes 叢集上的 SQL Server 巨量資料叢集，請執行下列命令：

```bash
mssqlctl create cluster <name of your cluster>
```

在叢集啟動程序，用戶端的 [命令] 視窗會將輸出的部署狀態。 您也可以在不同的 cmd 視窗執行下列命令來檢查部署狀態：

```bash
kubectl get all -n <name of your cluster>
kubectl get pods -n <name of your cluster>
kubectl get svc -n <name of your cluster>
```

您可以執行，以查看更細微的 「 狀態 」 和 「 每個 pod 的組態：
```bash
kubectl describe pod <pod name> -n <name of your cluster>
```

當控制器 pod 執行時，您可以利用叢集系統管理入口網站來監視部署中的 [部署] 索引標籤。

## <a id="masterip"></a> 取得 SQL Server Master 執行個體和 SQL Server 巨量資料叢集 IP 位址

部署指令碼已順利完成之後，您可以取得使用下面所述的步驟在 SQL Server 主要執行個體的 IP 位址。 您將使用此 IP 位址和連接埠號碼 31433 連接到 SQL Server 的主要執行個體 (例如：  **\<ip 位址\>31433、**)。 同樣地，針對 SQL Server 的巨量資料叢集 IP。 所有的叢集端點所述在 叢集系統管理網站的 服務端點 索引標籤。 您可以使用叢集系統管理入口網站來監視部署。 您可以存取入口網站中使用的外部 IP 位址和連接埠號碼`service-proxy-lb`(例如： **https://\<ip 位址\>: 30777**)。 認證為存取管理員入口網站的值`CONTROLLER_USERNAME`和`CONTROLLER_PASSWORD`上面提供的環境變數。

### <a name="aks"></a>AKS

如果您使用 AKS，Azure 會提供 Azure 負載平衡器服務。 執行下列命令：

```bash
kubectl get svc service-master-pool-lb -n <name of your cluster>
kubectl get svc service-security-lb -n <name of your cluster>
kubectl get svc service-proxy-lb -n <name of your cluster>
```

尋求**EXTERNAL-IP**值，指派給服務。 然後，連接到 SQL Server 主要執行個體連接埠 31433 使用的 IP 位址 (例如：  **\<ip 位址\>、 31433**) 和 SQL Server 使用的外部 IP 的巨量資料叢集端點`service-security-lb`服務。 

### <a name="minikube"></a>Minikube

如果您使用 Minikube，您需要執行下列命令來取得 IP 位址需要連線到。 除了 IP，指定您要連接到端點的連接埠。 若要取得的所有服務端點 

```bash
minikube ip
```

無論平台 Kubernetes 叢集上執行，以取得部署的叢集，請執行下列命令的所有服務端點：
```bash
kubectl get svc -n <name of your cluster>
```

## <a name="next-steps"></a>後續步驟

已成功部署到 Kubernetes 叢集的巨量資料的 SQL Server 後[安裝的巨量資料 」 工具](deploy-big-data-tools.md)並試試看一些新功能，並了解[如何在 SQL Server 2019 預覽中使用 notebook](notebooks-guidance.md)。
