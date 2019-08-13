---
title: 使用 Python 指令碼進行部署
titleSuffix: SQL Server big data clusters
description: 了解如何使用部署指令碼在 Azure Kubernetes Service (AKS) 上部署 SQL Server 2019 巨量資料叢集 (預覽)。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: dee1c8669e6496553c367b4d1078d1e6a7f26497
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "68470712"
---
# <a name="use-a-python-script-to-deploy-a-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>使用 Python 指令碼在 Azure Kubernetes Service (AKS) 上部署 SQL Server 巨量資料叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

在本教學課程中，您會使用範例 Python 部署指令碼將 SQL Server 2019 巨量資料叢集 (預覽) 部署至 Azure Kubernetes Service (AKS)。

> [!TIP]
> AKS 只是針對巨量資料叢集而裝載 Kubernetes 的選項之一。 若要深入了解其他部署選項以及如何自訂部署選項，請參閱[如何在 Kubernetes 上部署 SQL Server 巨量資料叢集](deployment-guidance.md)。

此處使用的預設巨量資料叢集部署，包含 SQL 主要執行個體、一個計算集區執行個體、兩個資料集區執行個體以及兩個存放集區執行個體。 資料會使用 Kubernetes 持續性磁碟區來保存，該磁碟區使用 AKS 預設儲存類別。 本教學課程中使用的預設設定適用於開發/測試環境。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="prerequisites"></a>Prerequisites

- Azure 訂用帳戶。
- [巨量資料工具](deploy-big-data-tools.md)：
   - **azdata**
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
   - **Azure CLI**

## <a name="log-in-to-your-azure-account"></a>登入您的 Azure 帳戶

此指令碼會使用 Azure CLI 來自動建立 AKS 叢集。 執行指令碼之前，您必須至少使用 Azure CLI 登入您的 Azure 帳戶一次。 從命令提示字元執行下列命令。

```
az login
```

## <a name="download-the-deployment-script"></a>下載部署指令碼

本教學課程會使用 Python 指令碼 **deploy-sql-big-data-aks.py** 在 AKS 上自動建立巨量資料叢集。 如果您已安裝適用於 **azdata** 的 Python，您應該能在本教學課程中成功執行指令碼。 

在 Windows PowerShell 或 Linux Bash 提示字元中執行下列命令，從 GitHub 下載部署指令碼。

```
curl -o deploy-sql-big-data-aks.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/aks/deploy-sql-big-data-aks.py"
```

## <a name="run-the-deployment-script"></a>執行部署指令碼

使用下列步驟來執行部署指令碼。 此指令碼會在 Azure 中建立 AKS 服務，然後將 SQL Server 2019 巨量資料叢集部署至 AKS。 您也可以使用其他[環境變數](deployment-guidance.md#configfile)來修改指令碼以建立自訂部署。

1. 使用下列命令來執行指令碼：

   ```
   python deploy-sql-big-data-aks.py
   ```

   > [!NOTE]
   > 如果您的用戶端電腦和路徑中都有 python3 和 python2，則必須使用 python3 來執行命令：`python3 deploy-sql-big-data-aks.py`。

1. 出現提示時，輸入下列資訊：

   | ReplTest1 | Description |
   |---|---|
   | **Azure 訂用帳戶識別碼** | 用於 AKS 的 Azure 訂用帳戶識別碼。 您可以從另一個命令列執行 `az account list` 以列出您所有訂用帳戶及其識別碼。 |
   | **Azure 資源群組** | 要為 AKS 叢集建立的 Azure 資源群組名稱。 |
   | **Azure 區域** | 新 AKS 叢集的 Azure 區域 (預設為 **westus**)。 |
   | **機器大小** | 要在 AKS 叢集中用於節點的[機器大小](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) (預設為 **Standard_L8s**)。 |
   | **背景工作節點** | AKS 叢集中的背景工作角色節點數目 (預設為 **1**)。 |
   | **叢集名稱** | AKS 叢集和巨量資料叢集的名稱。 您巨量資料叢集的名稱只能由小寫英數字元組成，且不能有空格。 (預設為 **sqlbigdata**)。 |
   | **密碼** | 控制器、HDFS/Spark 閘道和主要執行個體的密碼 (預設為 **MySQLBigData2019**)。 |
   | **控制器使用者** | 控制器使用者的使用者名稱 (預設：**admin**)。 |

SQL Server 2019 巨量資料叢集早期採用者計畫中的參與者需要下列參數：**Docker 使用者名稱**和 **Docker 密碼**。 自 CTP 3.2 開始不再需要它們。

   > [!IMPORTANT]
   > 預設的 **Standard_L8s** 機器大小可能無法在每個 Azure 區域中使用。 如果您選擇不同的機器大小，請確定可在叢集中節點之間連結的磁碟總數大於或等於 24。 叢集中的每個持續性磁碟區宣告，都需要連結的磁碟。 目前，巨量資料叢集需要 24 個持續性磁碟區宣告。 例如，[Standard_L8s](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-storage#lsv2-series) 機器大小支援 32 個連結的磁碟，因此您可以使用此機器大小的單一節點來評估巨量資料叢集。

   > [!NOTE]
   > `sa` 帳戶是在安裝期間建立的 SQL Server 主要執行個體系統管理員。 建立部署之後，您可以在主要執行個體中執行 `echo $MSSQL_SA_PASSWORD` 來探索 `MSSQL_SA_PASSWORD` 環境變數。 基於安全考量，請在在部署後，變更您主要執行個體上的 `sa` 密碼。 如需詳細資訊，請參閱[變更您的 SA 密碼](../linux/quickstart-install-connect-docker.md#sapassword)。

1. 指令碼會使用您指定的參數來開始建立 AKS 叢集。 此步驟需要幾分鐘的時間。

   <img src="./media/quickstart-big-data-cluster-deploy/script-parameters.png" width="800px" alt="Script parameters and AKS cluster creation"/>

## <a name="monitor-the-status"></a>監視狀態

指令碼建立 AKS 叢集後，會繼續使用您稍早指定的設定來設定必要環境變數。 然後會呼叫 **azdata**，在 AKS 上部署巨量資料叢集。

用戶端命令視窗將輸出部署狀態。 在部署程序中，您應該會看到一系列訊息，表示其正在等候控制器 Pod：

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

在 10 到 20 分鐘內，您應該會收到控制器 Pod 正在執行的通知：

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.111.111.111:30080
```

> [!IMPORTANT]
> 由於下載巨量資料叢集元件的容器映像需要時間，因此整個部署可能會很費時。 不過，應該不會花費到數小時。 如果您在部署期間遇到問題，請參閱[監視和針對 SQL Server 巨量資料叢集進行疑難排解](cluster-troubleshooting-commands.md)。

## <a name="inspect-the-cluster"></a>檢查叢集

在部署期間，隨時可以使用 **kubectl** 或 **azdata** 來檢查執行中巨量資料叢集的狀態和詳細資料。

### <a name="use-kubectl"></a>使用 kubectl

開啟新的命令視窗以在部署程序中使用 **kubectl**。

1. 執行下列命令以取得整個叢集狀態的摘要：

   ```
   kubectl get all -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 如果您未變更巨集資料叢集名稱，則指令碼會預設為 **sqlbigdata**。

1. 使用下列 **kubectl** 命令檢查 kubernetes 服務及其內部和外部端點：

   ```
   kubectl get svc -n <your-big-data-cluster-name>
   ```

1. 您也可以使用下列命令來檢查 kubernetes Pod 的狀態：

   ```
   kubectl get pods -n <your-big-data-cluster-name>
   ```

1. 使用下列命令來找出特定 Pod 的詳細資訊：

   ```
   kubectl describe pod <pod name> -n <your-big-data-cluster-name>
   ```

> [!TIP]
> 如需如何監視並針對部署並進行疑難排解的詳細資料，請參閱[監視並針對 SQL Server 巨量資料叢集進行疑難排解](cluster-troubleshooting-commands.md)。

## <a name="connect-to-the-cluster"></a>連線至叢集

部署指令碼完成時，輸出會通知您成功：

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

SQL Server 巨量資料叢集現在已部署在 AKS 上。 您現在可以使用 Azure Data Studio 連線至叢集。 如需詳細資訊，請參閱[使用 Azure Data Studio 連線至 SQL Server 巨量資料叢集](connect-to-big-data-cluster.md)。

## <a name="clean-up"></a>清除

如果您要在 Azure 中測試 SQL Server 巨量資料叢集，您應在完成時刪除 AKS 叢集，以避免產生非預期的費用。 如果您希望繼續使用叢集，請勿移除叢集。

> [!WARNING]
> 下列步驟會卸除 AKS 叢集，也會移除 SQL Server 巨量資料叢集。 如果您有任何想要保留的資料庫或 HDFS 資料，請在刪除叢集之前先備份該資料。

執行下列 Azure CLI 命令以移除 azure 中的巨量資料叢集和 AKS 服務 (將 `<resource group name>` 取代為您在部署指令碼中指定的 **Azure 資源群組**)：

```azurecli
az group delete -n <resource group name>
```

## <a name="next-steps"></a>後續步驟

部署指令碼已設定 Azure Kubernetes Service，同時也部署了 SQL Server 2019 巨量資料叢集。 您也可以選擇透過手動安裝來自訂未來的部署。 若要深入了解如何部署巨量資料叢集以及如何自訂部署，請參閱[如何在 Kubernetes 上部署 SQL Server 巨量資料叢集](deployment-guidance.md)。

現在 SQL Server 巨量資料叢集已完成部署，您可以載入範例資料並探索教學課程：

> [!div class="nextstepaction"]
> [教學課程：將範例資料載入 SQL Server 2019 巨量資料叢集](tutorial-load-sample-data.md)