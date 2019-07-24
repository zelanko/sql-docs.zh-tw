---
title: 部署腳本
titleSuffix: SQL Server big data clusters
description: 逐步解說 Azure Kubernetes Service (AKS) 上的 SQL Server 2019 big data 叢集 (預覽) 部署。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7ff1ec3672fbcf101d98ad30913742186dea574d
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419397"
---
# <a name="deploy-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>Azure Kubernetes Service 上部署 SQL Server big data 叢集 (AKS)

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

在本教學課程中, 您會使用範例部署腳本, 將 SQL Server 2019 big data cluster (預覽) 部署至 Azure Kubernetes Service (AKS)。 

> [!TIP]
> AKS 只有一個選項可裝載您 big data 叢集的 Kubernetes。 若要深入瞭解其他部署選項, 以及如何自訂部署選項, 請參閱[如何在 Kubernetes 上部署 SQL Server big data](deployment-guidance.md)叢集。

此處使用的預設 big data cluster 部署包含 SQL 主要實例、一個計算集區實例、兩個資料集區實例, 以及兩個儲存集區實例。 資料會使用使用 AKS 預設儲存類別的 Kubernetes 持續性磁片區來保存。 本教學課程中使用的預設設定適用于開發/測試環境。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="prerequisites"></a>先決條件

- Azure 訂用帳戶。
- [海量資料工具](deploy-big-data-tools.md):
   - **azdata**
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
   - **Azure CLI**

## <a name="log-in-to-your-azure-account"></a>登入您的 Azure 帳戶

此腳本會使用 Azure CLI 來自動建立 AKS 叢集。 執行腳本之前, 您必須使用 Azure CLI 至少一次登入您的 Azure 帳戶。 從命令提示字元執行下列命令。

```
az login
```

## <a name="download-the-deployment-script"></a>下載部署腳本

本教學課程會使用 python 腳本**deploy-sql-big-data-aks.py**, 在 AKS 上自動建立 big data 叢集。 如果您已安裝適用于**azdata**的 python, 您應該能夠在本教學課程中成功地執行腳本。 

在 Windows PowerShell 或 Linux bash 提示字元中, 執行下列命令以從 GitHub 下載部署腳本。

```
curl -o deploy-sql-big-data-aks.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/aks/deploy-sql-big-data-aks.py"
```

## <a name="run-the-deployment-script"></a>執行部署腳本

使用下列步驟來執行部署腳本。 此腳本會在 Azure 中建立 AKS 服務, 然後將 SQL Server 2019 big data 叢集部署至 AKS。 您也可以使用其他[環境變數](deployment-guidance.md#configfile)來修改腳本, 以建立自訂部署。

1. 使用下列命令執行腳本:

   ```
   python deploy-sql-big-data-aks.py
   ```

   > [!NOTE]
   > 如果您的用戶端電腦和路徑中都有 python3 和 python2, 則必須使用 python3: `python3 deploy-sql-big-data-aks.py`來執行命令。

1. 出現提示時, 輸入下列資訊:

   | 值 | 描述 |
   |---|---|
   | **Azure 訂用帳戶識別碼** | 要用於 AKS 的 Azure 訂用帳戶識別碼。 您可以`az account list`從另一個命令列執行, 以列出您所有的訂用帳戶及其識別碼。 |
   | **Azure 資源群組** | 要為 AKS 叢集建立的 Azure 資源組名。 |
   | **Azure 區域** | 新 AKS 叢集的 Azure 區域 (預設**westus**)。 |
   | **機器大小** | 要在 AKS 叢集中用於節點的[機器大小](https://docs.microsoft.com/azure/virtual-machines/windows/sizes)(預設**Standard_L8s**)。 |
   | **背景工作節點** | AKS 叢集中的背景工作節點數目 (預設值為**1**)。 |
   | **叢集名稱** | AKS 叢集和 big data 叢集的名稱。 您的 big data 叢集名稱必須是小寫的英數位元, 而且不能有空格。 (預設值**sqlbigdata**)。 |
   | **密碼** | 控制器、HDFS/Spark 閘道和主要實例的密碼 (預設**MySQLBigData2019**)。 |
   | **控制器使用者** | 控制器使用者的使用者名稱 (預設值: **admin**)。 |

SQL Server 2019 big data cluster 早期採用者計畫中的參與者需要下列參數:**Docker 使用者名稱**和**docker 密碼**。 從 CTP 3.2, 不再需要它們。

   > [!IMPORTANT]
   > 預設的**Standard_L8s**機器大小可能無法在每個 Azure 區域中使用。 如果您選擇不同的機器大小, 請確定可在叢集中的節點之間附加的磁片總數大於或等於24。 叢集中的每個持續性磁片區宣告都需要連接的磁片。 目前, big data cluster 需要24個持續性磁片區宣告。 例如, [Standard_L8s](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-storage#lsv2-series)機器大小支援32連接的磁片, 因此您可以使用此機器大小的單一節點來評估大型資料叢集。

   > [!NOTE]
   > 此`sa`帳戶是在安裝期間建立之 SQL Server 主要實例上的系統管理員。 建立部署之後, 您`MSSQL_SA_PASSWORD`可以`echo $MSSQL_SA_PASSWORD`在主要實例容器中執行, 以探索環境變數。 基於安全考慮, 請在`sa`部署後變更主要實例上的密碼。 如需詳細資訊, 請參閱[變更 SA 密碼](../linux/quickstart-install-connect-docker.md#sapassword)。

1. 腳本一開始會使用您指定的參數來建立 AKS 叢集。 此步驟需要幾分鐘的時間。

   <img src="./media/quickstart-big-data-cluster-deploy/script-parameters.png" width="800px" alt="Script parameters and AKS cluster creation"/>

## <a name="monitor-the-status"></a>監視狀態

在腳本建立 AKS 叢集之後, 它會繼續使用您稍早指定的設定來設定必要的環境變數。 然後它會呼叫**azdata** , 以在 AKS 上部署 big data 叢集。

[用戶端命令] 視窗將會輸出部署狀態。 在部署過程中, 您應該會看到一系列的訊息正在等候控制器 pod:

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

10到20分鐘後, 您應該會收到控制器 pod 正在執行的通知:

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.111.111.111:30080
```

> [!IMPORTANT]
> 整個部署可能需要很長的時間, 因為下載大型資料叢集元件的容器映射所需的時間。 不過, 這應該不需要花費數小時的時間。 如果您的部署遇到問題, 請參閱[監視和疑難排解 SQL Server big data](cluster-troubleshooting-commands.md)叢集。

## <a name="inspect-the-cluster"></a>檢查叢集

在部署期間, 您可以隨時使用**kubectl**或**azdata**來檢查有關執行中 big data 叢集的狀態和詳細資料。

### <a name="use-kubectl"></a>使用 kubectl

開啟新的命令視窗, 在部署過程中使用**kubectl** 。

1. 執行下列命令以取得整個叢集狀態的摘要:

   ```
   kubectl get all -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 如果您沒有變更 big data 叢集名稱, 腳本會預設為**sqlbigdata**。

1. 使用下列**kubectl**命令檢查 kubernetes 服務及其內部和外部端點:

   ```
   kubectl get svc -n <your-big-data-cluster-name>
   ```

1. 您也可以使用下列命令來檢查 kubernetes pod 的狀態:

   ```
   kubectl get pods -n <your-big-data-cluster-name>
   ```

1. 使用下列命令, 找出特定 pod 的詳細資訊:

   ```
   kubectl describe pod <pod name> -n <your-big-data-cluster-name>
   ```

> [!TIP]
> 如需有關如何監視和疑難排解部署的詳細資訊, 請參閱[監視和疑難排解 SQL Server big data](cluster-troubleshooting-commands.md)叢集。

## <a name="connect-to-the-cluster"></a>連接到叢集

當部署腳本完成時, 輸出會通知您成功:

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

SQL Server big data 叢集現在已部署在 AKS 上。 您現在可以使用 Azure Data Studio 連接到叢集。 如需詳細資訊, 請參閱[使用 Azure Data Studio 連接到 SQL Server big data](connect-to-big-data-cluster.md)叢集。

## <a name="clean-up"></a>清除

如果您要在 Azure 中測試 SQL Server big data 叢集, 您應該在完成時刪除 AKS 叢集, 以避免產生非預期的費用。 如果您想要繼續使用叢集, 請勿移除叢集。

> [!WARNING]
> 下列步驟會向下眼淚 AKS 叢集, 此叢集也會移除 SQL Server big data 叢集。 如果您有想要保留的任何資料庫或 HDFS 資料, 請在刪除叢集之前先備份該資料。

執行下列 Azure CLI 命令, 以移除 azure 中的 big data 叢集和 AKS 服務 (將取代`<resource group name>`為您在部署腳本中指定的**Azure 資源群組**):

```azurecli
az group delete -n <resource group name>
```

## <a name="next-steps"></a>後續步驟

部署腳本已設定 Azure Kubernetes Service, 同時也部署了 SQL Server 2019 big data 叢集。 您也可以選擇透過手動安裝來自訂未來的部署。 若要深入瞭解如何部署海量資料叢集, 以及如何自訂部署, 請參閱[如何在 Kubernetes 上部署 SQL Server big data](deployment-guidance.md)叢集。

現在, SQL Server big data 叢集已部署, 您可以載入範例資料並探索教學課程:

> [!div class="nextstepaction"]
> [教學課程：將範例資料載入 SQL Server 2019 big data 叢集中](tutorial-load-sample-data.md)