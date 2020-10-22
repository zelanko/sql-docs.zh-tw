---
title: 部署指導
titleSuffix: SQL Server Big Data Clusters
description: 了解如何在 Kubernetes 上部署 SQL Server 巨量資料叢集。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 870ff07f771f06acfb24e9883477b177af36d425
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257208"
---
# <a name="how-to-deploy-big-data-clusters-2019-on-kubernetes"></a>如何在 Kubernetes 上部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

SQL Server 巨量資料叢集會部署為 Kubernetes 叢集上的 Docker 容器。 這是安裝和設定步驟的概觀：

- 在單一 VM、VM 叢集、Azure Kubernetes Service (AKS)、Red Hat OpenShift 或 Azure Red Hat OpenShift (ARO) 中設定 Kubernetes 叢集。
- 在您的用戶端電腦上安裝叢集設定工具 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]。
- 在 Kubernetes 叢集中部署 SQL Server 巨量資料叢集。

## <a name="supported-platforms"></a>支援的平台

如需經驗證可部署 SQL Server 巨量資料叢集其各種 Kubernetes 平台的完整清單，請參閱[支援的平台](release-notes-big-data-cluster.md#supported-platforms)。

### <a name="sql-server-editions"></a>SQL Server 版本

|版本|注意|
|---------|---------|
|Enterprise<br/>標準<br/>開發人員| 巨量資料叢集版本是由 SQL Server 主要執行個體版本所決定。 在部署時，預設會部署 Developer Edition。 在部署後可以變更此版本。 請參閱[設定 SQL Server 主要執行個體](./configure-sql-server-master-instance.md)。 |

## <a name="kubernetes"></a><a id="prereqs"></a> Kubernetes

### <a name="kubernetes-cluster-setup"></a><a id="kubernetes"></a> Kubernetes 叢集設定

如果您已經有滿足上述先決條件的 Kubernetes 叢集，則可直接跳到[部署步驟](#deploy)。 本節假設您對 Kubernetes 概念有基本瞭解。  如需 Kubernetes 的詳細資訊，請參閱 [Kubernetes 文件](https://kubernetes.io/docs/home) \(英文\)。

您可選擇使用下列方式來部署 Kubernetes：

| 在下列項目上部署 Kubernetes： | 描述 | 連結 |
|---|---|---|
| **Azure Kubernetes Service (AKS)** | Azure 中的受控 Kubernetes 容器服務。 | [指示](deploy-on-aks.md) |
| **單一或多部電腦 (`kubeadm`)** | 使用 `kubeadm`，在實體或虛擬機器上部署 Kubernetes 叢集 | [指示](deploy-with-kubeadm.md) |
|**Azure Red Hat OpenShift** | 在 Azure 中執行的受控 OpenShift 供應項目。 | [指示](deploy-openshift.md)|
|**Red Hat OpenShift**|混合式雲端的企業 Kubernetes 應用程式平台。| [指示](deploy-openshift.md)|

> [!TIP]
> 您也可以透過單一步驟編寫部署 AKS 和巨量資料叢集的指令碼。 如需詳細資訊，請參閱如何在 [Python 指令碼](quickstart-big-data-cluster-deploy.md)或 Azure Data Studio [筆記本](notebooks-deploy.md)中執行此動作。

### <a name="verify-kubernetes-configuration"></a>確認 Kubernetes 組態

執行 `kubectl` 命令來檢視叢集設定。 確定 kubectl 指向正確的叢集內容。

```bash
kubectl config view
```

> [!Important] 
> 如果您要在使用 `kubeadm` 所啟動的多節點 Kuberntes 叢集上部署，則在開始進行巨量資料叢集部署之前，請確定部署的所有目標 Kubernetes 節點上時鐘已同步。 巨量資料叢集針對仰賴正確時間的各項服務具有內建健全狀況屬性，而時鐘誤差可能會導致狀態不正確。

設定 Kubernetes 叢集之後，您可以繼續部署新的 SQL Server 巨量資料叢集。 如果您從前一個版本升級，請參閱[如何升級 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-upgrade.md)。

## <a name="ensure-you-have-storage-configured"></a>確定已設定儲存體

大多數的巨量資料叢集部署都應該擁有永續性儲存體。 此時，您需要先確定已為如何在 Kubernetes 叢集上提供永續性儲存體進行規劃，才能部署 BDC。

若您在 AKS 中進行部署，則不需要任何儲存體設定。 AKS 提供具備動態佈建的內建儲存類別。 您可以在部署設定檔中自訂儲存類別 (`default` 或 `managed-premium`)。 內建設定檔會使用 `default` 儲存類別。 若正在以使用 `kubeadm` 所部署的 Kubernetes 叢集上進行部署，則您將需要確定針對所需規模的叢集具備了足夠儲存體，且該儲存體已經設定且可供使用。 若要自訂儲存體的使用方式，建議在繼續前先執行此操作。 請參閱[在 Kubernetes 上使用 SQL Server 巨量資料叢集的資料持續性](concept-data-persistence.md)。

## <a name="install-sql-server-2019-big-data-tools"></a>安裝 SQL Server 2019 巨量資料工具

部署 SQL Server 2019 巨量資料叢集之前，請先[安裝巨量資料工具](deploy-big-data-tools.md)：

- [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]
- `kubectl`
- Azure Data Studio
- 適用於 Azure Data Studio 的[資料虛擬化延伸模組](../azure-data-studio/extensions/data-virtualization-extension.md)


## <a name="deployment-overview"></a><a id="deploy"></a> 部署概觀

大部分的巨量資料叢集設定都定義於 JSON 部署組態檔中。 您可以針對 AKS 和透過 `kubeadm` 所建立的 Kubernetes 叢集使用預設部署設定檔，或自訂自己的部署設定檔以在設定期間使用。 基於安全因素，驗證設定會透過環境變數來傳遞。

下列各節會提供更多有關如何設定巨量資料叢集部署的詳細資訊，以及一般自訂的範例。 此外，您一律可以使用 VS Code 之類的編輯器來編輯自訂部署組態檔。

## <a name="default-configurations"></a><a id="configfile"></a> 預設組態

巨量資料叢集部署選項均定義於 JSON 組態檔中。 您可以從 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] 中可用的內建部署設定檔開始自訂叢集部署。 

> [!NOTE]
> 巨量資料叢集部署所需容器映像會裝載於 Microsoft 容器登錄 (`mcr.microsoft.com`) 的 `mssql/bdc` 存放庫中。 根據預設，這些設定已包含在 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] 所隨附每個部署設定檔的 `control.json` 設定檔中。 此外，每個版本的容器映像標籤也會預先填入相同設定檔。 如果您需要將容器映像提取到自己的私人容器登錄中，以及/或修改容器登錄/存放庫設定，請遵循[＜離線安裝＞](deploy-offline.md)一文中的指示

執行此命令來尋找可用的範本：

```
azdata bdc config list -o table 
```

SQL Server 2019 CU5 提供下列範本： 

| 部署設定檔 | Kubernetes 環境 |
|---|---|
| `aks-dev-test` | 在 Azure Kubernetes Service (AKS) 上部署 SQL Server 巨量資料叢集|
| `aks-dev-test-ha` | 在 Azure Kubernetes Service (AKS) 上部署 SQL Server 巨量資料叢集。 這會設定任務關鍵性服務 (例如 SQL Server 主要和 HDFS 名稱節點) 以取得高可用性。|
| `aro-dev-test`|在 Azure Red Hat OpenShift 上部署 SQL Server 巨量資料叢集，以進行開發和測試。 <br/><br/>在 SQL Server 2019 CU5 中引進。|
| `aro-dev-test-ha`|在 Red Hat OpenShift 叢集上部署具有高可用性的 SQL Server 巨量資料叢集，以進行開發和測試。 <br/><br/>在 SQL Server 2019 CU5 中引進。|
| `kubeadm-dev-test` | 在使用單一或多部實體或虛擬機器來透過 kubeadm 建立的 Kubernetes 叢集上部署 SQL Server 巨量資料叢集。|
| `kubeadm-prod`| 在使用單一或多部實體或虛擬機器來透過 kubeadm 建立的 Kubernetes 叢集上部署 SQL Server 巨量資料叢集。 使用此範本可讓巨量資料叢集服務與 Active Directory 整合。 這會在高可用性設定中部署任務關鍵性服務 (例如 SQL Server 主要執行個體和 HDFS 名稱節點)。  |
| `openshift-dev-test`|在 Red Hat OpenShift 叢集上部署 SQL Server 巨量資料叢集，以進行開發和測試。 <br/><br/>在 SQL Server 2019 CU5 中引進。|
| `openshift-prod`|在 Red Hat OpenShift 叢集上部署具有高可用性的 SQL Server 巨量資料叢集。 <br/><br/>在 SQL Server 2019 CU5 中引進。|

您可以執行 `azdata bdc create` 來部署巨量資料叢集。 這會提示您選擇其中一個預設組態，然後引導您完成部署。

第一次執行 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] 時，您必須包含 `--accept-eula=yes` 以接受使用者授權合約 (EULA)。

```bash
azdata bdc create --accept-eula=yes
```

在此案例中，系統會提示您輸入任何不屬於預設組態 (例如密碼) 一部分的設定。 

> [!IMPORTANT]
> 巨量資料叢集的預設名稱為 `mssql-cluster`。 若要執行任何 `kubectl` 命令，以使用 `-n` 參數來指定 Kubernetes 命名空間，請務必了解這一點。

## <a name="custom-configurations"></a><a id="customconfig"></a> 自訂組態

您也可以自訂部署來容納正在規劃執行的工作負載。 您無法在巨量資料叢集服務部署後變更規模 (複本數目) 或儲存體設定，因此請務必謹慎規劃部署設定，以避免發生容量問題。 若要自訂部署，請遵循下列步驟：

1. 從符合您 Kubernetes 環境的其中一個標準部署設定檔開始。 您可以使用 `azdata bdc config list` 命令來列出這些設定檔：

   ```bash
   azdata bdc config list
   ```

1. 若要自訂部署，請使用 `azdata bdc config init` 命令來建立部署設定檔的複本。 例如，下列命令會在名為 `custom` 的目標目錄中建立 `aks-dev-test` 部署設定檔複本：

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

   >[!TIP]
   >`--target` 會根據 `--source` 參數來指定包含設定檔 (`bdc.json` 和 `control.json`) 的目錄。

1. 若要在您的部署組態設定檔中自訂設定，您可以在適用於編輯 JSON 檔案的工具 (例如 VS Code) 中編輯部署組態檔。 針對已編寫指令碼的自動化，您也可以使用 `azdata bdc config` 命令來編輯自訂部署設定檔。 例如，下列命令會改變自訂部署設定檔，以將部署的叢集名稱從預設值 (`mssql-cluster`) 變更為 `test-cluster`：  

   ```bash
   azdata bdc config replace --config-file custom/bdc.json --json-values "metadata.name=test-cluster"
   ```

   > [!TIP]
   > 您也可以使用 *azdata create bdc* 命令的 *--name* 參數，在部署期間傳入叢集名稱。 命令中的參數優先於組態檔中的值。
   >
   > 尋找 JSON 路徑的實用工具是 [JSONPath Online Evaluator](https://jsonpath.com/) \(英文\)。
   >
   除了傳遞索引鍵/值組，您也可以提供內嵌的 JSON 值，或傳遞 JSON 修補檔案。 如需詳細資訊，請參閱[針對巨量資料叢集設定部署設定](deployment-custom-configuration.md)。

1. 將自訂設定檔傳遞至 `azdata bdc create`。 請注意，您必須設定必要的[環境變數](#env)，否則終端會提示您輸入下列值：

   ```bash
   azdata bdc create --config-profile custom --accept-eula yes
   ```

> 如需部署組態檔結構的詳細資訊，請參閱[部署組態檔參考](reference-deployment-config.md)。 如需更多組態範例，請參閱[設定巨量資料叢集的部署設定](deployment-custom-configuration.md)。

## <a name="environment-variables"></a><a id="env"></a> 環境變數

下列環境變數用於不會儲存於部署組態檔中的安全性設定。 請注意，您可以在組態檔中設定認證以外的 Docker 設定。

| 環境變數 | 需求 |說明 |
|---|---|---|
| `AZDATA_USERNAME` | 必要 |SQL Server 巨量資料叢集管理員的使用者名稱。 SQL Server 主要執行個體中會建立具有相同名稱的系統管理員登入。 基於安全性最佳做法，`sa` 帳戶已停用。 <br/><br/>[!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]|
| `AZDATA_PASSWORD` | 必要 |以上所建立使用者帳戶的密碼。 在 SQL Server 2019 CU5 之前部署的叢集上，`root` 使用者會使用相同的密碼來保護 Knox 閘道和 HDFS。 |
| `ACCEPT_EULA`| 第一次使用 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] 時的必要項| 設定為 [是]。 設定為環境變數時，會將 EULA 套用至 SQL Server 和 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]。 如果未設定為環境變數，您可以在第一次使用 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] 命令時包含 `--accept-eula=yes`。|
| `DOCKER_USERNAME` | 選用 | 用來存取容器映像的使用者名稱，以防它們儲存於私人存放庫中。 如需如何使用私人 Docker 存放庫來進行巨量資料叢集部署的詳細資訊，請參閱[離線部署](deploy-offline.md)主題。|
| `DOCKER_PASSWORD` | 選用 |用來存取上述私人存放庫的密碼。 |

呼叫 `azdata bdc create` 之前，必須先設定這些環境變數。 如果未設定任何變數，系統就會提示您輸入。

下列範例示範如何設定適用於 Linux (Bash) 和 Windows (PowerShell) 的環境變數：

```bash
export AZDATA_USERNAME=admin
export AZDATA_PASSWORD=<password>
export ACCEPT_EULA=yes
```

```PowerShell
SET AZDATA_USERNAME=admin
SET AZDATA_PASSWORD=<password>
```

> [!NOTE]
> 在 SQL Server 2019 CU5 之前部署的叢集上，您必須針對 Knox 閘道使用 `root` 使用者搭配上述密碼。 `root` 是此基本驗證 (使用者名稱/密碼) 中唯一支援的使用者。
> [!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]
> 若要使用基本驗證連線到 SQL Server，請使用與 AZDATA_USERNAME 和 AZDATA_PASSWORD [環境變數](#env)相同的值。 

設定環境變數之後，您必須執行 `azdata bdc create` 來觸發部署。 此範例會使用上方所建立的叢集組態設定檔：

```bash
azdata bdc create --config-profile custom --accept-eula yes
```

請注意下列方針：

- 如果密碼包含任何特殊字元，請務必以雙引號括住密碼。 您可以將 `AZDATA_PASSWORD` 設定為您喜歡的任何內容，但請確定密碼夠複雜，且不要使用 `!`、`&` 或 `'` 字元。 請注意，雙引號分隔符號僅適用於 Bash 命令。
- `AZDATA_USERNAME` 登入是在設定期間所建立 SQL Server 主要執行個體上的系統管理員。 建立您的 SQL Server 容器之後，在容器中執行 `echo $AZDATA_PASSWORD`，即可探索您指定的 `AZDATA_PASSWORD` 環境變數。 基於安全性考量，最佳做法是變更密碼。

## <a name="unattended-install"></a><a id="unattended"></a> 自動安裝

針對自動部署，您必須設定所有必要的環境變數、使用組態檔，並使用 `--accept-eula yes` 參數來呼叫 `azdata bdc create` 命令。 上一節的範例會示範自動安裝的語法。

## <a name="monitor-the-deployment"></a><a id="monitor"></a> 監視部署

在叢集啟動程序期間，用戶端命令視窗會傳回部署狀態。 在部署程序中，您應該會看到一系列訊息，表示其正在等候控制器 Pod：

```output
Waiting for cluster controller to start.
```

在 15 到 30 分鐘內，您應該會收到控制器 Pod 正在執行的通知：

```output
Cluster controller endpoint is available at 11.111.111.11:30080.
Cluster control plane is ready.
```

> [!IMPORTANT]
> 由於下載巨量資料叢集元件的容器映像需要時間，因此整個部署可能會很費時。 不過，應該不會花費到數小時。 部署時若發生問題，請參閱[監視及疑難排解[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](cluster-troubleshooting-commands.md)。

完成部署時，輸出會通知您成功：

```output
Cluster deployed successfully.
```

> [!TIP]
> 除非是透過自訂組態來修改，否則所部署巨量資料叢集的預設名稱會是 `mssql-cluster`。

## <a name="retrieve-endpoints"></a><a id="endpoints"></a> 取出端點

成功完成部署指令碼之後，您可以使用下列步驟來取得巨量資料叢集的外部端點位址。

1. 部署之後，可從部署標準輸出來尋找控制器端點的 IP 位址，或查看下列 `kubectl` 命令的外部 IP 輸出來尋找該位址：

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 如果您未在部署期間變更預設名稱，則在上一個命令中使用 `-n mssql-cluster`。 `mssql-cluster` 是巨量資料叢集的預設名稱。

1. 使用 [azdata login](../azdata/reference/reference-azdata.md) 來登入巨量資料叢集。 將 `--endpoint` 參數設定為控制器端點的外部 IP 位址。

   ```bash
   azdata login --endpoint https://<ip-address-of-controller-svc-external>:30080 --username <user-name>
   ```

   指定您在部署期間為巨量資料叢集管理員所設定的使用者名稱和密碼 (AZDATA_USERNAME 和 AZDATA_PASSWORD)。

   > [!TIP]
   > 如果您是 Kubernetes 叢集管理員並可存取叢集設定檔 (Kube 設定檔)，您可以將目前的內容設定為指向目標 Kubernetes 叢集。 在此情況下，您可以使用 `azdata login -n <namespaceName>` 登入，其中 `namespace` 是巨量資料叢集名稱。 如果未在登入命令中指定，系統會提示您提供認證。
   
1. 執行 [azdata bdc endpoint list](../azdata/reference/reference-azdata-bdc-endpoint.md) 來取得一份清單，其中包含每個端點的描述及其對應 IP 位址和連接埠值。 

   ```bash
   azdata bdc endpoint list -o table
   ```

   下列清單顯示此命令的範例輸出：

   ```output
   Description                                             Endpoint                                                   Ip              Name               Port    Protocol
   ------------------------------------------------------  ---------------------------------------------------------  --------------  -----------------  ------  ----------
   Gateway to access HDFS files, Spark                     https://11.111.111.111:30443                               11.111.111.111  gateway            30443   https
   Spark Jobs Management and Monitoring Dashboard          https://11.111.111.111:30443/gateway/default/sparkhistory  11.111.111.111  spark-history      30443   https
   Spark Diagnostics and Monitoring Dashboard              https://11.111.111.111:30443/gateway/default/yarn          11.111.111.111  yarn-ui            30443   https
   Application Proxy                                       https://11.111.111.111:30778                               11.111.111.111  app-proxy          30778   https
   Management Proxy                                        https://11.111.111.111:30777                               11.111.111.111  mgmtproxy          30777   https
   Log Search Dashboard                                    https://11.111.111.111:30777/kibana                        11.111.111.111  logsui             30777   https
   Metrics Dashboard                                       https://11.111.111.111:30777/grafana                       11.111.111.111  metricsui          30777   https
   Cluster Management Service                              https://11.111.111.111:30080                               11.111.111.111  controller         30080   https
   SQL Server Master Instance Front-End                    11.111.111.111,31433                                       11.111.111.111  sql-server-master  31433   tcp
   HDFS File System Proxy                                  https://11.111.111.111:30443/gateway/default/webhdfs/v1    11.111.111.111  webhdfs            30443   https
   Proxy for running Spark statements, jobs, applications  https://11.111.111.111:30443/gateway/default/livy/v1       11.111.111.111  livy               30443   https
   ```

您也可以執行下列 `kubectl` 命令來取得針對叢集部署的所有服務端點：

```bash
kubectl get svc -n <your-big-data-cluster-name>
```

## <a name="verify-the-cluster-status"></a><a id="status"></a> 確認叢集狀態

部署之後，您可以使用 [azdata bdc status show](../azdata/reference/reference-azdata-bdc-status.md) 命令來檢查叢集的狀態。

```bash
azdata bdc status show
```

> [!TIP]
> 若要執行狀態命令，您必須先使用 `azdata login` 命令登入，此動作已於先前的端點一節中示範過。

下列顯示此命令的範例輸出：

```output
Bdc: ready                                                                                                                                                                                                          Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Services: ready                                                                                                                                                                                                     Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Servicename    State    Healthstatus    Details

 sql            ready    healthy         -
 hdfs           ready    healthy         -
 spark          ready    healthy         -
 control        ready    healthy         -
 gateway        ready    healthy         -
 app            ready    healthy         -


 Sql Services: ready                                                                                                                                                                                                 Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 master          ready    healthy         StatefulSet master is healthy
 compute-0       ready    healthy         StatefulSet compute-0 is healthy
 data-0          ready    healthy         StatefulSet data-0 is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Hdfs Services: ready                                                                                                                                                                                                Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 nmnode-0        ready    healthy         StatefulSet nmnode-0 is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy
 sparkhead       ready    healthy         StatefulSet sparkhead is healthy


 Spark Services: ready                                                                                                                                                                                               Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 sparkhead       ready    healthy         StatefulSet sparkhead is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Control Services: ready                                                                                                                                                                                             Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 controldb       ready    healthy         -
 control         ready    healthy         -
 metricsdc       ready    healthy         DaemonSet metricsdc is healthy
 metricsui       ready    healthy         ReplicaSet metricsui is healthy
 metricsdb       ready    healthy         StatefulSet metricsdb is healthy
 logsui          ready    healthy         ReplicaSet logsui is healthy
 logsdb          ready    healthy         StatefulSet logsdb is healthy
 mgmtproxy       ready    healthy         ReplicaSet mgmtproxy is healthy


 Gateway Services: ready                                                                                                                                                                                             Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 gateway         ready    healthy         StatefulSet gateway is healthy


 App Services: ready                                                                                                                                                                                                 Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 appproxy        ready    healthy         ReplicaSet appproxy is healthy
```

您也可以使用下列命令來取得更詳細的狀態：

- [azdata bdc control status show](../azdata/reference/reference-azdata-bdc-control-status.md) 會傳回與控制管理服務建立關聯的所有元件健全狀態
```
azdata bdc control status show
```
範例輸出：
```output
Control: ready                                                                                                                                                                                                      Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Resources: ready                                                                                                                                                                                                    Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 controldb       ready    healthy         -
 control         ready    healthy         -
 metricsdc       ready    healthy         DaemonSet metricsdc is healthy
 metricsui       ready    healthy         ReplicaSet metricsui is healthy
 metricsdb       ready    healthy         StatefulSet metricsdb is healthy
 logsui          ready    healthy         ReplicaSet logsui is healthy
 logsdb          ready    healthy         StatefulSet logsdb is healthy
 mgmtproxy       ready    healthy         ReplicaSet mgmtproxy is healthy
```

- `azdata bdc sql status show` 會傳回具有 SQL Server 服務的所有資源健全狀態
```
azdata bdc sql status show
```
範例輸出：
```output
Sql: ready                                                                                                                                                                                                          Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Resources: ready                                                                                                                                                                                                    Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 master          ready    healthy         StatefulSet master is healthy
 compute-0       ready    healthy         StatefulSet compute-0 is healthy
 data-0          ready    healthy         StatefulSet data-0 is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy
```

> [!IMPORTANT]
> 使用 `--all` 參數時，這些命令之輸出會包含 Kibana 和 Grafana 儀表板的 URL，以取得更詳細分析。

除了使用 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]，您也可以使用 Azure Data Studio 來尋找端點和狀態資訊。 如需使用 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] 和 Azure Data Studio 來檢視叢集狀態的詳細資訊，請參閱[如何檢視巨量資料叢集的狀態](view-cluster-status.md)。

## <a name="connect-to-the-cluster"></a><a id="connect"></a> 連線到叢集

如需如何連線到巨量資料叢集的詳細資訊，請參閱[使用 Azure Data Studio 連線到 SQL Server 巨量資料叢集](connect-to-big-data-cluster.md)。

## <a name="next-steps"></a>後續步驟

若要深入了解巨量資料叢集部署，請參閱下列資源：

- [針對巨量資料叢集設定部署設定](deployment-custom-configuration.md)
- [執行 SQL Server 巨量資料叢集的離線部署](deploy-offline.md)
- [工作坊：Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters) \(英文\)