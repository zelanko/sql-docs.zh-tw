---
title: 部署指導
titleSuffix: SQL Server big data clusters
description: 了解如何部署在 Kubernetes 上的 SQL Server 2019 巨量資料叢集 （預覽）。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: a2ace569180006f54461631848ecbf5342b2c1e3
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "63472037"
---
# <a name="how-to-deploy-sql-server-big-data-clusters-on-kubernetes"></a>如何部署 SQL Server 在 Kubernetes 上的巨量資料叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

SQL Server 的巨量資料叢集會部署為 docker 容器的 Kubernetes 叢集。 這是安裝和設定步驟的概觀：

- 設定在單一 VM 的 Vm，或在 Azure Kubernetes Service (AKS) 叢集上的 Kubernetes 叢集。
- 安裝叢集的設定工具**mssqlctl**用戶端電腦上。
- 部署 SQL Server 的巨量資料叢集在 Kubernetes 叢集中。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="install-sql-server-2019-big-data-tools"></a>安裝 SQL Server 2019 巨量資料工具

在部署 SQL Server 2019 巨量資料叢集之前，先[安裝的巨量資料 」 工具](deploy-big-data-tools.md):

- **mssqlctl**
- **kubectl**
- **Azure Data Studio**
- **SQL Server 2019 延伸模組**

## <a id="prereqs"></a> Kubernetes 的必要條件

SQL Server 的巨量資料叢集至少需要的最小的 Kubernetes 版本 v1.10 伺服器和用戶端 (kubectl)。

> [!NOTE]
> 請注意，用戶端和伺服器的 Kubernetes 版本應該介於 + 1，則為-1 的次要版本。 如需詳細資訊，請參閱 < [Kubernetes 支援的版本和元件扭曲](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew)。

### <a id="kubernetes"></a> Kubernetes 叢集設定

如果您已經有符合上述必要條件，Kubernetes 叢集，則您可以直接跳到[部署步驟](#deploy)。 本節假設 Kubernetes 概念的基本知識。  如需 Kubernetes 的詳細資訊，請參閱[Kubernetes 文件](https://kubernetes.io/docs/home)。

您可以選擇部署 Kubernetes 中任何一種方式：

| 部署 Kubernetes 上： | 描述 | 連結 |
|---|---|---|
| **Azure Kubernetes 服務 (AKS)** | 在 Azure 中受控的 Kubernetes 容器服務。 | [指示](deploy-on-aks.md) |
| **多部電腦 (kubeadm)** | 部署實體或虛擬機器上的 Kubernetes 叢集**kubeadm** | [指示](deploy-with-kubeadm.md) |
| **Minikube** | 在 VM 中單一節點 Kubernetes 叢集。 | [指示](deploy-on-minikube.md) |

> [!TIP]
> 部署 AKS 和巨量資料叢集在一個步驟中的 SQL Server 的範例 python 指令碼，請參閱[快速入門：將巨量資料叢集的 Azure Kubernetes Service (AKS) 上的 SQL Server 部署](quickstart-big-data-cluster-deploy.md)。

### <a name="verify-kubernetes-configuration"></a>確認 Kubernetes 組態

執行**kubectl**命令來檢視叢集組態。 請確定該 kubectl 指向正確的叢集內容。

```bash
kubectl config view
```

您已設定您的 Kubernetes 叢集之後，您可以繼續與新的 SQL Server 巨量資料叢集的部署。 如果您要從舊版升級，請參閱[如何升級 SQL Server 的巨量資料叢集](deployment-upgrade.md)。

## <a id="deploy"></a> 部署概觀

從 CTP 2.5，大部分的巨量資料叢集設定為 JSON 部署組態檔中定義。 您可以使用 AKS，kubeadm，預設的部署設定檔或 minikube 或您可以自訂安裝期間要使用您自己部署設定檔。 基於安全性理由，會透過環境變數來傳遞驗證設定。

下列各節提供更多有關如何設定您的巨量資料叢集部署，以及常見的自訂的範例。 此外，您一律可以編輯自訂的部署組態檔案，例如使用 VSCode 之類的編輯器。

## <a id="configfile"></a> 預設組態

巨量資料叢集的部署選項在 JSON 組態檔中定義。 有三個標準的部署設定檔，以預設設定為開發/測試環境：

| 部署設定檔 | Kubernetes 的環境 |
|---|---|
| **aks-dev-test.json** | Azure Kubernetes Service (AKS) |
| **kubeadm-dev-test.json** | 多部電腦 (kubeadm) |
| **minikube-dev-test.json** | Minikube |

您可以藉由執行部署巨量資料叢集**mssqlctl 叢集建立**。 這會提示您選擇其中一個預設設定，然後引導您完成部署。

```bash
mssqlctl cluster create
```

> [!TIP]
> 在此範例中，系統會提示您提供不是預設設定，例如密碼的一部分的任何設定。 請注意，Docker 資訊 Microsoft 提供給您的 SQL Server 2019 一部分[Early Adoption Program](https://aka.ms/eapsignup)。

## <a id="customconfig"></a> 自訂設定

它也可自訂您自己的部署設定檔。 您可以使用下列步驟來這麼做：

1. 開始使用其中一個符合您的 Kubernetes 環境的標準部署設定檔。 您可以使用**mssqlctl 叢集組態清單**命令來列出它們：

   ```bash
   mssqlctl cluster config list
   ```

1. 若要自訂您的部署，建立與部署設定檔的複本**mssqlctl 叢集組態 init**命令。 例如，下列命令會建立一份**aks-dev-test.json**目前目錄中的部署設定檔：

   ```bash
   mssqlctl cluster config init --src aks-dev-test.json --target custom.json
   ```

1. 若要自訂您的部署組態檔中設定，您可以在一種工具，適合編輯 json 文件，例如 VS 程式碼中加以編輯。 指令碼式自動化，您可以編輯自訂組態檔中使用**mssqlctl 叢集組態區段組**命令。 例如，下列命令會改變要變更預設的已部署的叢集名稱的自訂組態檔 (**mssql 叢集**) 來**測試叢集**:  

   ```bash
   mssqlctl cluster config section set --config-file custom.json --json-values "metadata.name=test-cluster"
   ```

   > [!TIP]
   > 有用的工具，尋找 JSON 路徑是[JSONPath 線上評估工具](https://jsonpath.com/)。

   除了傳遞索引鍵 / 值組，您也可以內嵌方式提供的 JSON 值，或傳遞 JSON 修補程式檔案。 如需詳細資訊，請參閱 <<c0> [ 巨量資料叢集的部署設定](deployment-custom-configuration.md)。

1. 然後將傳遞至自訂的組態檔**mssqlctl 叢集建立**。 請注意，您必須設定必要[環境變數](#env)，否則系統會提示的值：

   ```bash
   mssqlctl cluster create --config-file custom.json --accept-eula yes
   ```

> [!TIP]
> 如需有關部署組態檔案的結構的詳細資訊，請參閱[部署組態檔參考](reference-deployment-config.md)。 如需組態範例，請參閱[巨量資料叢集的部署設定](deployment-custom-configuration.md)。

## <a id="env"></a> 環境變數

下列環境變數用於不會儲存在 部署設定檔的安全性設定。

| 環境變數 | 描述 |
|---|---|---|---|
| **DOCKER_REGISTRY** | 私用登錄中儲存用來部署叢集的映像。 |
| **DOCKER_REPOSITORY** | 上述的登錄，影像都會儲存在私人存放庫。 |
| **DOCKER_USERNAME** | 存取容器映像，如果它們儲存在私人存放庫的使用者名稱。 |
| **DOCKER_PASSWORD** | 存取上述的私人存放庫的密碼。 |
| **DOCKER_IMAGE_TAG** | 用來標記映像的標籤。 預設值為**最新**，但我們建議使用對應的發行版本的標記，以避免版本不相容的問題。 |
| **CONTROLLER_USERNAME** | 針對叢集系統管理員使用者名稱。 |
| **CONTROLLER_PASSWORD** | 針對叢集系統管理員密碼。 |
| **KNOX_PASSWORD** | Knox 使用者的密碼。 |
| **MSSQL_SA_PASSWORD** | SQL master 執行個體的 SA 使用者的密碼。 |

呼叫之前，必須設定這些環境變數**mssqlctl 叢集建立**。 如果未設定任何變數，它會提示您。

下列範例示範如何設定環境變數，適用於 Linux (bash) 和 Windows (PowerShell):

```bash
export CONTROLLER_USERNAME=<controller_user>
export CONTROLLER_PASSWORD=<password>
export DOCKER_REGISTRY=<docker-registry>
export DOCKER_REPOSITORY=<docker-repository>
export MSSQL_SA_PASSWORD=<password>
export KNOX_PASSWORD=<password>
export DOCKER_USERNAME=<docker-username>
export DOCKER_PASSWORD=<docker-password>
export DOCKER_IMAGE_TAG=ctp2.5
```

```PowerShell
SET CONTROLLER_USERNAME=admin
SET CONTROLLER_PASSWORD=<password>
SET DOCKER_REGISTRY=<docker-registry>
SET DOCKER_REPOSITORY=<docker-repository>
SET MSSQL_SA_PASSWORD=<password>
SET KNOX_PASSWORD=<password>
SET DOCKER_USERNAME=<docker-username>
SET DOCKER_PASSWORD=<docker-password>
SET DOCKER_IMAGE_TAG=ctp2.5
```

設定環境變數，您必須執行`mssqlctl cluster create`觸發部署。 此範例會使用先前建立的叢集組態檔：

```
mssqlctl cluster create --config-file custom.json --accept-eula yes
```

請注意下列指導方針：

- 在此階段中，私用 Docker 登錄的認證會提供給您時分級您[Early Adoption Program 註冊](https://aka.ms/eapsignup)。 早期的採用計劃註冊，才能測試 SQL Server 的巨量資料叢集。
- 請確定您將包裝密碼雙引號括住，如果它包含任何特殊字元。 您可以設定**MSSQL_SA_PASSWORD**至任何您喜歡，但請確定密碼夠複雜，且不用`!`，`&`或`'`字元。 請注意，雙引號括住分隔符號僅適用於 bash 命令。
- **SA**登入是在安裝期間建立的 SQL Server 主要執行個體上的系統管理員。 建立您的 SQL Server 容器之後, **MSSQL_SA_PASSWORD**執行您所指定的環境變數是可探索回應在容器中的 $MSSQL_SA_PASSWORD。 基於安全考量，變更您的 SA 密碼，根據所述的最佳作法[此處](../linux/quickstart-install-connect-docker.md#sapassword)。
- **DOCKER_IMAGE_TAG**發行您的控制項安裝在此範例中。 在此範例中，它是 CTP 2.5 版。

## <a id="unattended"></a> 自動的安裝

如需自動部署，您必須設定所有必要的環境變數、 使用組態檔，並呼叫`mssqlctl cluster create`命令搭配`--accept-eula yes`參數。 上一節中的範例將示範自動安裝的語法。

## <a id="monitor"></a> 監視部署

在叢集啟動程序，用戶端的 [命令] 視窗會將輸出的部署狀態。 在部署過程中，您應該會看到一系列的訊息，它正在等候控制器 pod:

```output
2019-04-12 14:40:10.0129 UTC | INFO | Waiting for controller pod to be up...
```

在 15 到 30 分鐘內，應該會通知您正在執行控制器 pod:

```output
2019-04-12 15:01:10.0809 UTC | INFO | Waiting for controller pod to be up. Checkthe mssqlctl.log file for more details.
2019-04-12 15:01:40.0861 UTC | INFO | Controller pod is running.
2019-04-12 15:01:40.0884 UTC | INFO | Controller Endpoint: https://<ip-address>:30080
```

> [!IMPORTANT]
> 整個部署可能需要很長的時間，因為下載的巨量資料叢集元件的容器映像所需的時間。 不過，它應該不需要數小時。 如果您遇到部署問題，請參閱[監視和疑難排解 SQL Server 的巨量資料叢集](cluster-troubleshooting-commands.md)。

部署完成時，輸出會通知您成功：

```output
2019-04-12 15:37:18.0271 UTC | INFO | Monitor and track your cluster at the Portal Endpoint: https://<ip-address>:30777/portal/
2019-04-12 15:37:18.0271 UTC | INFO | Cluster deployed successfully.
```

記下的 URL**入口網站端點**在上述的輸出，以用於下一節。

> [!TIP]
> 已部署的巨量資料叢集的預設名稱是`mssql-cluster`除非修改自訂的組態。

## <a id="endpoints"></a> 擷取端點

部署指令碼已順利完成之後，您可以取得使用下列步驟的巨量資料叢集的外部端點的 IP 位址。

1. 從部署的輸出，複製**入口網站端點**，並移除`/portal/`結尾。 這是管理 Proxy URL (例如`https://<ip-address>:30777`)。

   > [!TIP]
   > 如果您還沒有部署輸出，您可以藉由查看外部 IP 的輸出下列管理 proxy 取得 IP 位址**kubectl**命令：
   >
   > ```bash
   > kubectl get svc mgmtproxy-svc-external -n <your-cluster-name>
   > ```

1. 登入的巨量資料叢集**mssqlctl 登入**。 設定 **-端點**管理 Proxy 參數。

   ```bash
   mssqlctl login --endpoint https://<ip-address>:30777
   ```

   在部署期間指定的使用者名稱和您設定控制站 （CONTROLLER_USERNAME 和 CONTROLLER_PASSWORD） 的密碼。

1. 執行**mssqlctl 叢集端點清單**來取得每個端點和其對應的 IP 位址和連接埠值的描述與清單。 例如，以下顯示的管理入口網站端點的輸出：

   ```output
   {
     "description": "Management Portal",
     "endpoint": "https://<ip-address>:30777/portal",
     "ip": "<ip-address>",
     "name": "portal",
     "port": 30777,
     "protocol": "https"
   },
   ```

1. 所有的叢集端點也會概述於**服務端點**叢集管理入口網站中的索引標籤。 您可以存取入口網站上一個步驟中使用管理入口網站的端點 (例如`https://<ip-address>:30777/portal`)。 存取系統管理入口網站的認證是控制器名稱和密碼，您在部署期間指定的值。 您也可以使用叢集系統管理入口網站來監視部署。

### <a name="minikube"></a>Minikube

如果您使用 minikube，您需要執行下列命令來取得 IP 位址需要連線到。 除了 IP，指定您要連接到端點的連接埠。

```bash
minikube ip
```

無論平台 Kubernetes 叢集上執行，以取得部署的叢集，請執行下列命令的所有服務端點：

```bash
kubectl get svc -n <your-cluster-name>
```

## <a id="connect"></a> 連線到叢集

如需有關如何連線至巨量資料叢集的詳細資訊，請參閱 <<c0> [ 連接到 SQL Server 巨量資料叢集使用 Azure Data Studio](connect-to-big-data-cluster.md)。

## <a name="next-steps"></a>後續步驟

若要深入了解巨量資料叢集部署，請參閱下列資源：

- [設定部署巨量資料叢集](deployment-custom-configuration.md)
- [執行離線部署的 SQL Server 的巨量資料叢集](deploy-offline.md)
- [研討會：Microsoft SQL Server 的巨量資料叢集架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
