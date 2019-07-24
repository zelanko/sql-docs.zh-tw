---
title: 部署指導
titleSuffix: SQL Server big data clusters
description: 瞭解如何在 Kubernetes 上部署 SQL Server 2019 big data 叢集 (預覽)。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e6f2eefd37c45753e3051722448b80d88712df26
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419415"
---
# <a name="how-to-deploy-sql-server-big-data-clusters-on-kubernetes"></a>如何在 Kubernetes 上部署 SQL Server big data 叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

SQL Server big data 叢集會部署為 Kubernetes 叢集上的 docker 容器。 這是安裝程式和設定步驟的總覽:

- 在單一 VM、Vm 叢集或 Azure Kubernetes Service (AKS) 中設定 Kubernetes 叢集。
- 在您的用戶端電腦上安裝叢集設定工具**azdata** 。
- 在 Kubernetes 叢集中部署 SQL Server big data 叢集。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="install-sql-server-2019-big-data-tools"></a>安裝 SQL Server 2019 big data 工具

在部署 SQL Server 2019 big data 叢集之前, 請先[安裝 big data tools](deploy-big-data-tools.md):

- **azdata**
- **kubectl**
- **Azure Data Studio**
- **SQL Server 2019 延伸模組**

## <a id="prereqs"></a>Kubernetes 必要條件

SQL Server big data 叢集, 伺服器和用戶端 (kubectl) 至少需要 v 1.10 的最低 Kubernetes 版本。

> [!NOTE]
> 請注意, 用戶端和伺服器 Kubernetes 版本應該在 + 1 或-1 次要版本內。 如需詳細資訊, 請參閱[Kubernetes 版本資訊和版本誤差 SKU 原則)](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew)。

### <a id="kubernetes"></a>Kubernetes 叢集設定

如果您已經有符合上述必要條件的 Kubernetes 叢集, 則可以直接跳到[部署步驟](#deploy)。 本節假設您對 Kubernetes 概念有基本瞭解。  如需 Kubernetes 的詳細資訊, 請參閱[Kubernetes 檔](https://kubernetes.io/docs/home)。

您可以選擇以三種方式部署 Kubernetes:

| 部署 Kubernetes: | 描述 | 連結 |
|---|---|---|
| **Azure Kubernetes Services (AKS)** | Azure 中的受控 Kubernetes 容器服務。 | [螢幕](deploy-on-aks.md) |
| **多部電腦 (kubeadm)** | 使用**kubeadm**部署在實體或虛擬機器上的 Kubernetes 叢集 | [螢幕](deploy-with-kubeadm.md) |
| **Minikube** | VM 中的單一節點 Kubernetes 叢集。 | [螢幕](deploy-on-minikube.md) |

> [!TIP]
> 如需在一個步驟中部署 AKS 和 SQL Server big data 叢集的範例 python 腳本, 請參閱[快速入門:在 Azure Kubernetes Service 上部署 SQL Server big data 叢集 (AKS](quickstart-big-data-cluster-deploy.md))。

### <a name="verify-kubernetes-configuration"></a>確認 Kubernetes 設定

執行**kubectl**命令來查看叢集設定。 請確定 kubectl 指向正確的叢集內容。

```bash
kubectl config view
```

設定 Kubernetes 叢集之後, 您可以繼續部署新的 SQL Server big data cluster。 如果您是從上一版升級, 請參閱[如何升級 SQL Server big data](deployment-upgrade.md)叢集。

## <a id="deploy"></a>部署總覽

最大的資料叢集設定會定義在 JSON 部署設定檔中。 您可以使用 AKS、或`kubeadm` `minikube`的預設部署設定檔, 也可以自訂您自己的部署設定檔, 以在安裝期間使用。 基於安全考慮, 驗證設定會透過環境變數來傳遞。

下列各節提供更多有關如何設定 big data cluster 部署的詳細資訊, 以及一般自訂的範例。 此外, 您一律可以使用 VS Code 之類的編輯器來編輯自訂部署設定檔, 例如。

## <a id="configfile"></a>預設設定

Big data cluster 部署選項定義于 JSON 設定檔中。 有三個標準部署設定檔具有開發/測試環境的預設設定:

| 部署設定檔 | Kubernetes 環境 |
|---|---|
| **aks-dev-test** | Azure Kubernetes Service (AKS) |
| **kubeadm-dev-test** | 多部電腦 (kubeadm) |
| **minikube-dev-test** | Minikube |

您可以藉由執行**azdata bdc create**來部署 big data cluster。 這會提示您選擇其中一個預設設定, 然後引導您完成部署。

第一次執行`azdata`時, 您必須包含`--accept-eula`以接受使用者授權合約 (EULA)。

```bash
azdata bdc create --accept-eula
```

在此案例中, 系統會提示您輸入不屬於預設設定 (例如密碼) 的任何設定。 

> [!NOTE]
> 從 SQL Server 2019 CTP 3.2 開始, 您不再屬於 SQL Server 2019[早期採用計畫](https://aka.ms/eapsignup)的成員, 以體驗 big data cluster 的預覽版本。

> [!IMPORTANT]
> Big data 叢集的預設名稱是**mssql-cluster**。 請務必知道, 才能執行任何以`-n`參數指定 Kubernetes 命名空間的**kubectl**命令。

## <a id="customconfig"></a>自訂設定

也可以自訂您自己的部署設定設定檔。 您可以使用下列步驟來執行這項操作:

1. 從符合您 Kubernetes 環境的其中一個標準部署設定檔開始。 您可以使用**azdata bdc config list**命令來列出它們:

   ```bash
   azdata bdc config list
   ```

1. 若要自訂您的部署, 請使用**azdata bdc config init**命令建立部署設定檔的複本。 例如, 下列命令會在名為`custom`的目標目錄中建立**aks-開發/測試**部署設定檔的複本:

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

   azdata
   > 會根據`--source`參數,  指定包含設定檔(cluster.json和control.json)的`--target`目錄。

1. 若要在您的部署設定檔中自訂設定, 您可以在適用于編輯 JSON 檔案的工具中編輯部署設定檔, 例如 VS Code。 針對已編寫腳本的自動化, 您也可以使用**azdata bdc config**命令來編輯自訂部署設定檔。 例如, 下列命令會變更自訂部署設定檔, 以將部署的叢集名稱從預設 (**mssql-** 叢集) 變更為**測試**叢集:  

   ```bash
   azdata bdc config replace --config-file custom/cluster.json --json-values "metadata.name=test-cluster"
   ```

   > 尋找 JSON 路徑的公用程式是[JSONPath Online 評估](https://jsonpath.com/)工具。

   除了傳遞索引鍵/值組以外, 您也可以提供內嵌 JSON 值, 或傳遞 JSON 修補程式檔案。 如需詳細資訊, 請參閱[設定 big data 叢集的部署設定](deployment-custom-configuration.md)。

1. 然後將自訂設定檔傳遞至**azdata bdc create**。 請注意, 您必須設定必要的[環境變數](#env), 否則系統會提示您輸入下列值:

   ```bash
   azdata bdc create --config-profile custom --accept-eula yes
   ```

> 如需部署設定檔結構的詳細資訊, 請參閱[部署設定檔參考](reference-deployment-config.md)。 如需更多設定範例, 請參閱[設定大型資料叢集的部署設定](deployment-custom-configuration.md)。

## <a id="env"></a>環境變數

下列環境變數會用於不會儲存在部署設定檔中的安全性設定。 請注意, 您可以在設定檔中設定認證以外的 Docker 設定。

| 環境變數 | 需求 |描述 |
|---|---|---|
| **CONTROLLER_USERNAME** | 必要項 |叢集系統管理員的使用者名稱。 |
| **CONTROLLER_PASSWORD** | 必要項 |叢集系統管理員的密碼。 |
| **MSSQL_SA_PASSWORD** | 必要項 |SQL 主要實例的 SA 使用者密碼。 |
| **KNOX_PASSWORD** | 必要項 |Knox 使用者的密碼。 |
| **ACCEPT_EULA**| 第一次使用時所需`azdata`| 不需要任何值。 當設定為環境變數時, 會將 EULA 套用至 SQL Server 和`azdata`。 如果未設定為環境變數, 您可以在`--accept-eula`第一次`azdata`使用命令時包含。|
| **DOCKER_USERNAME** | 選擇性 | 用來存取容器映射的使用者名稱, 以防它們儲存在私人存放庫中。 如需如何使用私用 Docker 存放庫來進行 big data cluster 部署的詳細資訊, 請參閱[離線部署](deploy-offline.md)主題。|
| **DOCKER_PASSWORD** | 選擇性 |用來存取上述私人存放庫的密碼。 |

呼叫**azdata bdc create**之前, 必須先設定這些環境變數。 如果未設定任何變數, 系統會提示您輸入。

下列範例顯示如何設定 Linux (bash) 和 Windows (PowerShell) 的環境變數:

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

設定環境變數之後, 您必須執行`azdata bdc create`來觸發部署。 這個範例會使用上面建立的叢集設定檔:

```bash
azdata bdc create --config-profile custom --accept-eula yes
```

請注意下列指導方針:

- 若包含任何特殊字元, 請務必以雙引號括住密碼。 您可以將**MSSQL_SA_PASSWORD**設定為您喜歡的任何內容, 但請確定密碼夠複雜, 而且不使用`!` `&`或`'`字元。 請注意, 雙引號分隔符號僅適用于 bash 命令。
- **SA**登入是在安裝期間建立之 SQL Server 主要實例的系統管理員。 建立 SQL Server 容器之後, 在容器 `echo $MSSQL_SA_PASSWORD`中執行可探索您指定的 MSSQL_SA_PASSWORD 環境變數。 基於安全考慮, 請根據[這裡](../linux/quickstart-install-connect-docker.md#sapassword)記載的最佳做法變更您的 SA 密碼。

## <a id="unattended"></a>自動安裝

若是自動部署, 您必須設定所有必要`azdata bdc create` `--accept-eula yes`的環境變數、使用設定檔, 並使用參數呼叫命令。 上一節中的範例會示範自動安裝的語法。

## <a id="monitor"></a>監視部署

在叢集啟動程式期間, 用戶端命令視窗會輸出部署狀態。 在部署過程中, 您應該會看到一系列的訊息正在等候控制器 pod:

```output
Waiting for cluster controller to start.
```

在15到30分鐘內, 您應該會收到控制器 pod 正在執行的通知:

```output
Cluster controller endpoint is available at 11.111.111.11:30080.
Cluster control plane is ready.
```

> [!IMPORTANT]
> 整個部署可能需要很長的時間, 因為下載大型資料叢集元件的容器映射所需的時間。 不過, 這應該不需要花費數小時的時間。 如果您的部署遇到問題, 請參閱[監視和疑難排解 SQL Server big data](cluster-troubleshooting-commands.md)叢集。

當部署完成時, 輸出會通知您成功:

```output
Cluster deployed successfully.
```

> [!TIP]
> 已部署之 big data 叢集的預設名稱, `mssql-cluster`除非是由自訂設定修改。

## <a id="endpoints"></a>取出端點

成功完成部署腳本之後, 您可以使用下列步驟, 取得 big data 叢集外部端點的 IP 位址。

1. 部署之後, 請從部署標準輸出或查看下列**kubectl**命令的外部 IP 輸出, 尋找控制器端點的 IP 位址:

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 如果您未在部署期間變更預設名稱, 請在`-n mssql-cluster`上一個命令中使用。 **mssql-** 叢集是 big data cluster 的預設名稱。

1. 使用[azdata 登](reference-azdata.md)入來登入 big data 叢集。 將 **--controller-endpoint**參數設定為控制器端點的外部 IP 位址。

   ```bash
   azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   指定在部署期間為控制器設定的使用者名稱和密碼 (CONTROLLER_USERNAME 和 CONTROLLER_PASSWORD)。

1. 執行[azdata bdc 端點清單](reference-azdata-bdc-endpoint.md)來取得清單, 其中包含每個端點的描述及其對應的 IP 位址和埠值。 

   ```bash
   azdata bdc endpoint list -o table
   ```

   下列清單顯示此命令的範例輸出:

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

您也可以藉由執行下列**kubectl**命令, 取得為叢集部署的所有服務端點:

```bash
kubectl get svc -n <your-big-data-cluster-name>
```

### <a name="minikube"></a>Minikube

如果您使用 minikube, 您需要執行下列命令, 以取得您需要連接的 IP 位址。 除了 IP 以外, 請指定您需要連接的端點埠。

```bash
minikube ip
```

## <a id="status"></a>確認叢集狀態

部署之後, 您可以使用[azdata bdc status show](reference-azdata-bdc-status.md)命令來檢查叢集的狀態。

```bash
azdata bdc status show -o table
```

> [!TIP]
> 若要執行狀態命令, 您必須先使用**azdata login**命令進行登入, 這會顯示在先前的端點一節中。

以下顯示此命令的範例輸出:

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

在此摘要狀態中, 您也可以使用下列命令取得更詳細的狀態:

- [azdata bdc 控制項狀態](reference-azdata-bdc-control-status.md)
- [azdata bdc 集區狀態](reference-azdata-bdc-pool-status.md)

這些命令的輸出包含 Kibana 和 Grafana 儀表板的 Url, 以進行更詳細的分析。

除了使用**azdata**, 您也可以使用 Azure Data Studio 來尋找端點和狀態資訊。 如需使用**azdata**和 Azure Data Studio 來查看叢集狀態的詳細資訊, 請參閱[如何查看 big Data 叢集的狀態](view-cluster-status.md)。

## <a id="connect"></a>連接到叢集

如需有關如何連接到 big data 叢集的詳細資訊, 請參閱[使用 Azure Data Studio 連接到 SQL Server big data](connect-to-big-data-cluster.md)叢集。

## <a name="next-steps"></a>後續步驟

若要深入瞭解 big data cluster 部署, 請參閱下列資源:

- [設定 big data 叢集的部署設定](deployment-custom-configuration.md)
- [執行 SQL Server big data 叢集的離線部署](deploy-offline.md)
- [發現Microsoft SQL Server big data 叢集架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
