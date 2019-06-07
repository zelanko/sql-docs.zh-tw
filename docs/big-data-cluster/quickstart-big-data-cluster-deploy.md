---
title: 部署快速入門
titleSuffix: SQL Server big data clusters
description: 逐步解說部署的 SQL Server 2019 巨量資料叢集 （預覽） 在 Azure Kubernetes Service (AKS)。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: quickstart
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: a385a2691d37bf31186a3530e91bdf937ac4dc05
ms.sourcegitcommit: 32dce314bb66c03043a93ccf6e972af455349377
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2019
ms.locfileid: "66744203"
---
# <a name="quickstart-deploy-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>快速入門：部署 Azure Kubernetes Service (AKS) 上的 SQL Server 巨量資料叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

在本快速入門中，您可以使用範例部署指令碼部署 SQL Server 2019 巨量資料叢集 （預覽） Azure Kubernetes Service (AKS)。 

> [!TIP]
> AKS 會為您的巨量資料叢集裝載 Kubernetes 的只有一個選項。 若要瞭解其他部署選項，如何以自訂部署選項，請參閱[如何部署 SQL Server 的巨量資料叢集的 Kubernetes 上](deployment-guidance.md)。

這裡使用預設的巨量資料叢集部署是由 SQL Master 執行個體、 一個計算集區執行個體、 兩個資料集區執行個體和兩個儲存體集區執行個體所組成。 資料會保存使用使用 AKS 預設儲存體類別的 Kubernetes 永續性磁碟區。 在本快速入門使用的預設組態是適用於開發/測試環境。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="prerequisites"></a>先決條件

- Azure 訂用帳戶。
- [巨量資料工具](deploy-big-data-tools.md):
   - **mssqlctl**
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
   - **Azure CLI**

## <a name="log-in-to-your-azure-account"></a>登入您的 Azure 帳戶

指令碼會使用 Azure CLI 來自動化建立 AKS 叢集。 再執行指令碼，您必須登入您使用 Azure CLI 的 Azure 帳戶至少一次。 從命令提示字元中執行下列命令。

```
az login
```

## <a name="download-the-deployment-script"></a>下載部署指令碼

本快速入門中會自動建立巨量資料叢集上使用 python 指令碼的 AKS**部署-sql-巨量的資料-aks.py**。 如果您已安裝適用於 python **mssqlctl**，您應該能夠成功地執行指令碼，在本快速入門。 

在 Windows PowerShell 或 Linux bash 提示字元中，執行下列命令，以從 GitHub 下載的部署指令碼。

```
curl -o deploy-sql-big-data-aks.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/aks/deploy-sql-big-data-aks.py"
```

## <a name="run-the-deployment-script"></a>執行部署指令碼

您可以使用下列步驟來執行部署指令碼。 此指令碼會在 Azure 中建立的 AKS 服務，並接著將 SQL Server 2019 巨量資料叢集部署至 AKS。 您也可以修改與其他指令碼[環境變數](deployment-guidance.md#configfile)來建立自訂的部署。

1. 執行指令碼使用下列命令：

   ```
   python deploy-sql-big-data-aks.py
   ```

   > [!NOTE]
   > 如果您有 python3 和 python2 在用戶端電腦和路徑中，您必須使用 python3 執行命令： `python3 deploy-sql-big-data-aks.py`。

1. 出現提示時，輸入下列資訊：

   | 值 | 描述 |
   |---|---|
   | **Azure 訂用帳戶識別碼** | 要用於 AKS 的 Azure 訂用帳戶識別碼。 您可以執行來列出所有訂用帳戶和其識別碼`az account list`從另一個命令列。 |
   | **Azure 資源群組** | 若要建立 AKS 叢集的 Azure 資源群組名稱。 |
   | **Docker 使用者名稱** | Docker 使用者名稱提供給有限的公開預覽的一部分。 |
   | **Docker 的密碼** | Docker 密碼提供給有限的公開預覽的一部分。 |
   | **Azure 區域** | 新的 AKS 叢集的 Azure 區域 (預設值**westus**)。 |
   | **機器大小** | [機器大小](https://docs.microsoft.com/azure/virtual-machines/windows/sizes)用於 AKS 叢集中的節點 (預設**Standard_L8s**)。 |
   | **背景工作角色節點** | 在 AKS 叢集中的背景工作節點數目 (預設值**1**)。 |
   | **叢集名稱** | AKS 叢集與巨量資料叢集的名稱。 只有大小寫英數字元，而且沒有空格，必須是您的巨量資料叢集的名稱。 (預設值**sqlbigdata**)。 |
   | **密碼** | 控制器、 HDFS/Spark 閘道和主要執行個體的密碼 (預設值**MySQLBigData2019**)。 |
   | **控制器的使用者** | 控制器的使用者的使用者名稱 (預設值： **admin**)。 |

   > [!IMPORTANT]
   > 預設值**Standard_L8s**機器大小可能無法使用每個 Azure 區域中。 如果您選取不同的機器大小，請確定磁碟可連接到叢集中的節點總數大於或等於 24。 在叢集中的每個永續性磁碟區宣告需要連接的磁碟。 目前，巨量資料叢集需要 24 的永續性磁碟區宣告。 例如， [Standard_L8s](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-storage#lsv2-series)機器大小支援 32 個附加的磁碟，因此您能夠評估此機器大小的單一節點的巨量資料叢集。

   > [!NOTE]
   > `sa`帳戶是在安裝期間建立的 SQL Server 主要執行個體上的系統管理員。 建立部署之後,`MSSQL_SA_PASSWORD`環境變數是可探索執行`echo $MSSQL_SA_PASSWORD`主要執行個體的容器中。 基於安全考量，變更您`sa`在部署後的主要執行個體上的密碼。 如需詳細資訊，請參閱 <<c0> [ 變更 SA 密碼](../linux/quickstart-install-connect-docker.md#sapassword)。

1. 指令碼首先會建立 AKS 叢集，使用您指定的參數。 這個步驟需要幾分鐘的時間。

   <img src="./media/quickstart-big-data-cluster-deploy/script-parameters.png" width="800px" alt="Script parameters and AKS cluster creation"/>

## <a name="monitor-the-status"></a>監視狀態

指令碼會建立 AKS 叢集之後，它會設定必要的環境變數，使用您稍早指定的設定。 然後它會呼叫**mssqlctl**部署在 AKS 上的巨量資料叢集。

用戶端的 [命令] 視窗會將輸出的部署狀態。 在部署過程中，您應該會看到一系列的訊息，它正在等候控制器 pod:

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

在 10 到 20 分鐘後應該會通知您正在執行控制器 pod:

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.111.111.111:30080
```

> [!IMPORTANT]
> 整個部署可能需要很長的時間，因為下載的巨量資料叢集元件的容器映像所需的時間。 不過，它應該不需要數小時。 如果您遇到部署問題，請參閱[監視和疑難排解 SQL Server 的巨量資料叢集](cluster-troubleshooting-commands.md)。

## <a name="inspect-the-cluster"></a>檢查叢集

隨時都在部署期間，您可以使用**kubectl**或是**mssqlctl**檢查 狀態 和 執行巨量資料叢集的相關詳細資料。

### <a name="use-kubectl"></a>使用 kubectl

開啟新的命令視窗，以使用**kubectl**在部署程序。

1. 執行下列命令，以取得整個叢集的狀態摘要：

   ```
   kubectl get all -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 如果您未變更的巨量資料叢集名稱，指令碼會預設為**sqlbigdata**。

1. 檢查 kubernetes 服務，以及其內部和外部端點，以下列**kubectl**命令：

   ```
   kubectl get svc -n <your-big-data-cluster-name>
   ```

1. 您也可以檢查狀態的 kubernetes pod，使用下列命令：

   ```
   kubectl get pods -n <your-big-data-cluster-name>
   ```

1. 找出特定的 pod，使用下列命令的詳細資訊：

   ```
   kubectl describe pod <pod name> -n <your-big-data-cluster-name>
   ```

> [!TIP]
> 如需有關如何監視和疑難排解部署的詳細資訊，請參閱 <<c0> [ 監視和疑難排解 SQL Server 的巨量資料叢集](cluster-troubleshooting-commands.md)。

## <a name="connect-to-the-cluster"></a>連線到叢集

部署指令碼完成時，輸出會通知您成功：

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

巨量資料叢集現在已部署在 AKS SQL Server。 您現在可以使用 Azure Data Studio 來連線到叢集。 如需詳細資訊，請參閱 <<c0> [ 連接到 SQL Server 巨量資料叢集使用 Azure Data Studio](connect-to-big-data-cluster.md)。

## <a name="clean-up"></a>清除

如果您要測試 SQL Server 的巨量資料叢集在 Azure 中，您應該刪除 AKS 叢集，以避免產生非預期的費用所完成。 請勿移除叢集中，如果您想要繼續使用它。

> [!WARNING]
> 下列步驟會終止移除 SQL Server 巨量資料叢集 AKS 叢集。 如果您有任何資料庫或您想要保留的 HDFS 資料，該資料前先備份刪除叢集。

執行下列 Azure CLI 命令來移除 Azure 中的巨量資料叢集和 AKS 服務 (取代`<resource group name>`具有**Azure 資源群組**您在部署指令碼中指定):

```azurecli
az group delete -n <resource group name>
```

## <a name="next-steps"></a>後續步驟

部署指令碼會設定 Azure Kubernetes 服務，而且也部署 SQL Server 2019 巨量資料叢集。 您也可以選擇自訂進行手動安裝的未來部署。 若要深入了解更多有關如何在巨量資料叢集可藉由部署以及如何自訂部署，請參閱[如何部署 SQL Server 的巨量資料叢集的 Kubernetes 上](deployment-guidance.md)。

既然已經部署的 SQL Server 的巨量資料叢集，您可以載入範例資料，並瀏覽教學課程：

> [!div class="nextstepaction"]
> [教學課程：將範例資料載入 SQL Server 2019 巨量資料叢集](tutorial-load-sample-data.md)