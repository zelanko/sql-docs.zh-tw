---
title: 部署指導
titleSuffix: SQL Server big data clusters
description: 了解如何在 Kubernetes 上部署 SQL Server 2019 巨量資料叢集 (預覽)。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b7439fdc93f04ad137b0bb65269b9767d8281798
ms.sourcegitcommit: 58f1d5498c87bfe0f6ec4fd9d7bbe723be47896b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2019
ms.locfileid: "68995828"
---
# <a name="how-to-deploy-sql-server-big-data-clusters-on-kubernetes"></a>如何在 Kubernetes 上部署 SQL Server 巨量資料叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

SQL Server 巨量資料叢集會部署為 Kubernetes 叢集上的 Docker 容器。 這是安裝和設定步驟的概觀：

- 在單一 VM、VM 叢集或 Azure Kubernetes Service (AKS) 中設定 Kubernetes 叢集。
- 在您的用戶端電腦上，安裝叢集組態工具 **azdata**。
- 在 Kubernetes 叢集中部署 SQL Server 巨量資料叢集。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="install-sql-server-2019-big-data-tools"></a>安裝 SQL Server 2019 巨量資料工具

部署 SQL Server 2019 巨量資料叢集之前，請先[安裝巨量資料工具](deploy-big-data-tools.md)：

- **azdata**
- **kubectl**
- **Azure Data Studio**
- **SQL Server 2019 延伸模組**

## <a id="prereqs"></a> Kubernetes 先決條件

SQL Server 巨量資料叢集針對伺服器和用戶端 (kubectl) 至少需要 v 1.10 的 Kubernetes 版本。

> [!NOTE]
> 請注意，用戶端和伺服器 Kubernetes 版本應該在 +1 或 -1 次要版本內。 如需詳細資訊，請參閱 [Kubernetes 版本資訊和版本誤差 SKU 原則](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew) \(英文\)。

### <a id="kubernetes"></a> Kubernetes 叢集設定

如果您已經有滿足上述先決條件的 Kubernetes 叢集，則可直接跳到[部署步驟](#deploy)。 本節假設您對 Kubernetes 概念有基本瞭解。  如需 Kubernetes 的詳細資訊，請參閱 [Kubernetes 文件](https://kubernetes.io/docs/home) \(英文\)。

您可以選擇以下列三種方式中的任一種來部署 Kubernetes：

| 在下列項目上部署 Kubernetes： | 描述 | 連結 |
|---|---|---|
| **Azure Kubernetes Service (AKS)** | Azure 中的受控 Kubernetes 容器服務。 | [指示](deploy-on-aks.md) |
| **多部電腦 (kubeadm)** | 使用 **kubeadm**，在實體或虛擬機器上部署 Kubernetes 叢集 | [指示](deploy-with-kubeadm.md) |
| **Minikube** | VM 中的單一節點 Kubernetes 叢集。 | [指示](deploy-on-minikube.md) |

> [!TIP]
> 您也可以在一個步驟中編寫部署 AKS 和巨量資料叢集的指令碼。 如需詳細資訊，請參閱如何在 [Python 指令碼](quickstart-big-data-cluster-deploy.md)或 Azure Data Studio [筆記本](deploy-notebooks.md)中執行此動作。

### <a name="verify-kubernetes-configuration"></a>確認 Kubernetes 組態

執行 **kubectl** 命令來檢視叢集組態。 確定 kubectl 指向正確的叢集內容。

```bash
kubectl config view
```

設定 Kubernetes 叢集之後，您可以繼續部署新的 SQL Server 巨量資料叢集。 如果您從前一個版本升級，請參閱[如何升級 SQL Server 巨量資料叢集](deployment-upgrade.md)。

## <a id="deploy"></a> 部署概觀

大部分的巨量資料叢集設定都定義於 JSON 部署組態檔中。 您可以針對 AKS、`kubeadm` 或 `minikube` 使用預設的部署設定檔，或者您可以自訂自己的部署組態檔以在設定期間使用。 基於安全因素，驗證設定會透過環境變數來傳遞。

下列各節會提供更多有關如何設定巨量資料叢集部署的詳細資訊，以及一般自訂的範例。 此外，您一律可以使用 VS Code 之類的編輯器來編輯自訂部署組態檔。

## <a id="configfile"></a> 預設組態

巨量資料叢集部署選項均定義於 JSON 組態檔中。 有三個具有適用於開發/測試環境之預設設定的標準部署設定檔：

| 部署設定檔 | Kubernetes 環境 |
|---|---|
| **aks-dev-test** | Azure Kubernetes Service (AKS) |
| **kubeadm-dev-test** | 多部電腦 (kubeadm) |
| **minikube-dev-test** | minikube |

您可以執行 **azdata bdc create** 來部署巨量資料叢集。 這會提示您選擇其中一個預設組態，然後引導您完成部署。

第一次執行 `azdata` 時，您必須包含 `--accept-eula=yes` 以接受使用者授權合約 (EULA)。

```bash
azdata bdc create --accept-eula=yes
```

在此案例中，系統會提示您輸入任何不屬於預設組態 (例如密碼) 一部分的設定。 

> [!IMPORTANT]
> 巨量資料叢集的預設名稱是 **mssql-cluster**。 若要執行任何 **kubectl** 命令，以使用 `-n` 參數來指定 Kubernetes 命名空間，請務必了解這一點。

## <a id="customconfig"></a> 自訂組態

您也可以自訂自己的部署組態設定檔。 您可以執行下列步驟來達成此目的：

1. 從符合您 Kubernetes 環境的其中一個標準部署設定檔開始。 您可以使用 **azdata bdc config list** 命令來列出它們：

   ```bash
   azdata bdc config list
   ```

1. 若要自訂部署，請使用 **azdata bdc config init** 命令來建立部署設定檔的複本。 例如，下列命令會在名為 `custom` 的目標目錄中建立 **aks-dev-test** 部署組態檔的複本：

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

   azdata
   > `--target` 會根據 `--source` 參數來指定包含組態檔 (**cluster.json** 和 **control.json**) 的目錄。

1. 若要在您的部署組態設定檔中自訂設定，您可以在適用於編輯 JSON 檔案的工具 (例如 VS Code) 中編輯部署組態檔。 針對已編寫指令碼的自動化，您也可以使用 **azdata bdc config** 命令來編輯自訂部署設定檔。 例如，下列命令會改變自訂部署設定檔，以將部署的叢集名稱從預設值 (**mssql-cluster**) 變更為 **test-cluster**：  

   ```bash
   azdata bdc config replace --config-file custom/cluster.json --json-values "metadata.name=test-cluster"
   ```
   
> [!TIP]
> 您也可以使用 *azdata create bdc* 命令的 *--name* 參數，在部署期間傳入叢集名稱。 命令中的參數優先於組態檔中的值。

   > 尋找 JSON 路徑的實用工具是 [JSONPath Online Evaluator](https://jsonpath.com/) \(英文\)。

   除了傳遞索引鍵/值組，您也可以提供內嵌的 JSON 值，或傳遞 JSON 修補檔案。 如需詳細資訊，請參閱[針對巨量資料叢集設定部署設定](deployment-custom-configuration.md)。

1. 接著，將自訂組態檔傳遞至 **azdata bdc create**。 請注意，您必須設定必要的[環境變數](#env)，否則系統將提示您輸入下列值：

   ```bash
   azdata bdc create --config-profile custom --accept-eula yes
   ```

> 如需部署組態檔結構的詳細資訊，請參閱[部署組態檔參考](reference-deployment-config.md)。 如需更多組態範例，請參閱[設定巨量資料叢集的部署設定](deployment-custom-configuration.md)。

## <a id="env"></a> 環境變數

下列環境變數用於不會儲存於部署組態檔中的安全性設定。 請注意，您可以在組態檔中設定認證以外的 Docker 設定。

| 環境變數 | 需求 |描述 |
|---|---|---|
| **CONTROLLER_USERNAME** | 必要項 |叢集管理員的使用者名稱。 |
| **CONTROLLER_PASSWORD** | 必要項 |叢集管理員的密碼。 |
| **MSSQL_SA_PASSWORD** | 必要項 |適用於 SQL 主要執行個體的 SA 使用者密碼。 |
| **KNOX_PASSWORD** | 必要項 |Knox 使用者的密碼。 |
| **ACCEPT_EULA**| 第一次使用 `azdata` 時的必要項| 不需要任何值。 設定為環境變數時，會將 EULA 套用至 SQL Server 和 `azdata`。 如果未設定為環境變數，您可以在第一次使用 `azdata` 命令時包含 `--accept-eula`。|
| **DOCKER_USERNAME** | 選擇性 | 用來存取容器映像的使用者名稱，以防它們儲存於私人存放庫中。 如需如何使用私人 Docker 存放庫來進行巨量資料叢集部署的詳細資訊，請參閱[離線部署](deploy-offline.md)主題。|
| **DOCKER_PASSWORD** | 選擇性 |用來存取上述私人存放庫的密碼。 |

呼叫 **azdata bdc create** 之前，必須先設定這些環境變數。 如果未設定任何變數，系統就會提示您輸入。

下列範例示範如何設定適用於 Linux (Bash) 和 Windows (PowerShell) 的環境變數：

```bash
export CONTROLLER_USERNAME=admin
export CONTROLLER_PASSWORD=<password>
export MSSQL_SA_PASSWORD=<password>
export KNOX_PASSWORD=<password>
```

```PowerShell
SET CONTROLLER_USERNAME=admin
SET CONTROLLER_PASSWORD=<password>
SET MSSQL_SA_PASSWORD=<password>
SET KNOX_PASSWORD=<password>
```

設定環境變數之後，您必須執行 `azdata bdc create` 來觸發部署。 此範例會使用上方所建立的叢集組態設定檔：

```bash
azdata bdc create --config-profile custom --accept-eula yes
```

請注意下列方針：

- 如果密碼包含任何特殊字元，請務必以雙引號括住密碼。 您可以將 **MSSQL_SA_PASSWORD** 設定為您喜歡的任何內容，但請確定密碼夠複雜，而且不要使用 `!`、`&` 或 `'` 字元。 請注意，雙引號分隔符號僅適用於 Bash 命令。
- **SA** 登入是在安裝期間所建立之 SQL Server 主要執行個體上的系統管理員。 建立您的 SQL Server 容器之後，在容器中執行 `echo $MSSQL_SA_PASSWORD`，即可探索您指定的 **MSSQL_SA_PASSWORD** 環境變數。 基於安全因素，請根據[此處](../linux/quickstart-install-connect-docker.md#sapassword)記載的最佳做法來變更您的 SA 密碼。

## <a id="unattended"></a> 自動安裝

針對自動部署，您必須設定所有必要的環境變數、使用組態檔，並使用 `--accept-eula yes` 參數來呼叫 `azdata bdc create` 命令。 上一節的範例會示範自動安裝的語法。

## <a id="monitor"></a> 監視部署

在叢集啟動程序期間，用戶端命令視窗將輸出部署狀態。 在部署過程中，您應該會看到一系列的訊息，表示其正在等候控制器 Pod：

```output
Waiting for cluster controller to start.
```

在 15 到 30 分鐘內，您應該會收到控制器 Pod 正在執行的通知：

```output
Cluster controller endpoint is available at 11.111.111.11:30080.
Cluster control plane is ready.
```

> [!IMPORTANT]
> 由於下載巨量資料叢集元件的容器映像所需的時間，整個部署可能需要很長的時間。 不過，應該不會花費到數小時。 如果您在部署期間遇到問題，請參閱[監視和疑難排解 SQL Server 巨量資料叢集](cluster-troubleshooting-commands.md)。

完成部署時，輸出會通知您成功：

```output
Cluster deployed successfully.
```

> [!TIP]
> 除非是透過自訂組態來修改，否則所部署巨量資料叢集的預設名稱會是 `mssql-cluster`。

## <a id="endpoints"></a> 取出端點

成功完成部署指令碼之後，您可以使用下列步驟來取得巨量資料叢集之外部端點的 IP 位址。

1. 部署之後，可從部署標準輸出來尋找控制器端點的 IP 位址，或查看下列 **kubectl** 命令的外部 IP 輸出來尋找該位址：

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 如果您未在部署期間變更預設名稱，則在上一個命令中使用 `-n mssql-cluster`。 **mssql-cluster** 是巨量資料叢集的預設名稱。

1. 使用 [azdata login](reference-azdata.md) 來登入巨量資料叢集。 將 **--controller-endpoint** 參數設定為控制器端點的外部 IP 位址。

   ```bash
   azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   指定您在部署期間為控制器所設定的使用者名稱和密碼 (CONTROLLER_USERNAME 和 CONTROLLER_PASSWORD)。

1. 執行 [azdata bdc endpoint list](reference-azdata-bdc-endpoint.md) 來取得一份清單，其中包含每個端點的描述及其對應 IP 位址和連接埠值。 

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

您也可以執行下列 **kubectl** 命令，來取得針對叢集部署的所有服務端點：

```bash
kubectl get svc -n <your-big-data-cluster-name>
```

### <a name="minikube"></a>Minikube

如果您使用 minikube，則需要執行下列命令，以取得您需要連線的 IP 位址。 除了該 IP，還要指定您需要連線之端點的連接埠。

```bash
minikube ip
```

## <a id="status"></a> 確認叢集狀態

部署之後，您可以使用 [azdata bdc status show](reference-azdata-bdc-status.md) 命令來檢查叢集的狀態。

```bash
azdata bdc status show -o table
```

> [!TIP]
> 若要執行狀態命令，您必須先使用 **azdata login** 命令登入，此動作已於先前的端點小節中示範過。

以下顯示此命令的範例輸出：

```output
Kind     Name           State
-------  -------------  -------
BDC      mssql-cluster  Ready
Control  default        Ready
Master   default        Ready
Compute  default        Ready
Data     default        Ready
Storage  default        Ready
```

在此摘要狀態中，您也可以使用下列命令來取得更詳細的狀態：

- [azdata bdc control status](reference-azdata-bdc-control-status.md)
- [azdata bdc pool status](reference-azdata-bdc-pool-status.md)

這些命令的輸出包含 Kibana 和 Grafana 儀表板的 URL，可用來進行更詳細的分析。

除了使用 **azdata**，您也可以使用 Azure Data Studio 來尋找端點和狀態資訊。 如需使用 **azdata** 和 Azure Data Studio 來檢視叢集狀態的詳細資訊，請參閱[如何檢視巨量資料叢集的狀態](view-cluster-status.md)。

## <a id="connect"></a> 連線到叢集

如需如何連線到巨量資料叢集的詳細資訊，請參閱[使用 Azure Data Studio 連線到 SQL Server 巨量資料叢集](connect-to-big-data-cluster.md)。

## <a name="next-steps"></a>後續步驟

若要深入了解巨量資料叢集部署，請參閱下列資源：

- [針對巨量資料叢集設定部署設定](deployment-custom-configuration.md)
- [執行 SQL Server 巨量資料叢集的離線部署](deploy-offline.md)
- [工作坊：Microsoft SQL Server 巨量資料叢集架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
