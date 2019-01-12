---
title: 部署快速入門
titleSuffix: SQL Server 2019 big data clusters
description: 逐步解說部署的 SQL Server 2019 巨量資料叢集 （預覽） 在 Azure Kubernetes Service (AKS)。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/17/2018
ms.topic: quickstart
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 39c79c39c04d64656b83004425d476896cbc75db
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2019
ms.locfileid: "54241699"
---
# <a name="quickstart-deploy-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>快速入門：部署 Azure Kubernetes Service (AKS) 上的 SQL Server 巨量資料叢集

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

您可以使用下列步驟來執行部署指令碼。 此指令碼會在 Azure 中建立的 AKS 服務，並接著將 SQL Server 2019 巨量資料叢集部署至 AKS。 您也可以修改與其他指令碼[環境變數](deployment-guidance.md#env)來建立自訂的部署。

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
   | **機器大小** | [機器大小](https://docs.microsoft.com/azure/virtual-machines/windows/sizes)用於 AKS 叢集中的節點 (預設**Standard_L4s**)。 |
   | **背景工作角色節點** | 在 AKS 叢集中的背景工作節點數目 (預設值**3**)。 |
   | **叢集名稱** | AKS 叢集與巨量資料叢集的名稱。 只有大小寫英數字元，而且沒有空格，必須是叢集的名稱。 (預設值**sqlbigdata**)。 |
   | **密碼** | 控制器、 HDFS/Spark 閘道和主要執行個體的密碼 (預設值**MySQLBigData2019**)。 |
   | **控制器的使用者** | 控制器的使用者的使用者名稱 (預設值： **admin**)。 |

   > [!IMPORTANT]
   > 在叢集中的每個永續性磁碟區宣告需要連接的磁碟。 目前，巨量資料叢集需要 21 的永續性磁碟區宣告。 在選擇的 Azure 虛擬機器大小和節點數目時，請確定可附加的節點之間的磁碟總數大於或等於 21。 例如， [Standard_L4s](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-storage#ls-series)機器大小支援 16 個附加的磁碟，所以三個節點表示，可連結 48 的磁碟。

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
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.222.222.222:30080
```

> [!IMPORTANT]
> 整個部署可能需要很長的時間，因為下載的巨量資料叢集元件的容器映像所需的時間。 不過，它應該不需要數小時。 如果您遇到部署問題，請參閱[部署疑難排解](deployment-guidance.md#troubleshoot)的部署指引文件的區段。

## <a name="inspect-the-cluster"></a>檢查叢集

隨時都在部署期間，您可以使用 kubectl 或叢集的系統管理入口網站來檢查 狀態 和 執行巨量資料叢集的相關詳細資料。

### <a name="use-kubectl"></a>使用 kubectl

開啟新的命令視窗，以使用**kubectl**在部署程序。

1. 執行下列命令，以取得整個叢集的狀態摘要：

   ```
   kubectl get all -n <your-cluster-name>
   ```

1. 檢查 kubernetes 服務，以及其內部和外部端點，以下列**kubectl**命令：

   ```
   kubectl get svc -n <your-cluster-name>
   ```

1. 您也可以檢查狀態的 kubernetes pod，使用下列命令：

   ```
   kubectl get pods -n <your-cluster-name>
   ```

1. 找出特定的 pod，使用下列命令的詳細資訊：

   ```
   kubectl describe pod <pod name> -n <your-cluster-name>
   ```

> [!TIP]
> 如需有關如何監視和疑難排解部署的詳細資訊，請參閱 <<c0> [ 部署疑難排解](deployment-guidance.md#troubleshoot)的部署指引文件的區段。

### <a name="use-the-cluster-administration-portal"></a>使用叢集系統管理入口網站

當控制器 pod 執行時，您也可以使用叢集系統管理入口網站來監視部署。 您可以存取入口網站中使用的外部 IP 位址和連接埠號碼`service-proxy-lb`(例如： **https://\<ip 位址\>: 30777/入口網站**)。 用來登入入口網站的認證比對的值**Controller 使用者**並**密碼**您在部署指令碼中指定。

您可以取得的 IP 位址**lb-proxy 服務-** 服務中的 bash 或 cmd 視窗執行下列命令：

```bash
kubectl get svc service-proxy-lb -n <your-cluster-name>
```

> [!NOTE]
> 在 CTP 2.2，您會看到安全性警告時存取網頁，因為巨量資料叢集目前正在使用自動產生的 SSL 憑證。 此外，在 CTP 2.2，它不會顯示 SQL Server 的主要執行個體的狀態。

## <a name="connect-to-the-cluster"></a>連線到叢集

部署指令碼完成時，輸出會通知您成功：

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

巨量資料叢集現在已部署在 AKS SQL Server。 您現在可以使用 Azure Data Studio 連接到 SQL Server 的主要執行個體並使用 Azure Data Studio HDFS/Spark 端點。

### <a id="master"></a> 主要執行個體

SQL Server 的主要執行個體是傳統的 SQL Server 執行個體，包含 SQL Server 的關聯式資料庫。 下列步驟說明如何使用 Azure Data Studio 的主要執行個體的連接。

1. 從命令列中，找出 IP 主要執行個體使用下列命令：

   ```
   kubectl get svc endpoint-master-pool -n <your-cluster-name>
   ```

1. 在 Azure Data Studio，按下**F1** > **新連線**。

1. 在 **連線類型**，選取**Microsoft SQL Server**。

1. 輸入中的 SQL Server 主要執行個體的 IP 位址**伺服器名稱**(例如：**\<IP 位址\>31433、**)。

1. 輸入 SQL 登入**使用者名**(`SA`) 及**密碼**（您在部署指令碼中輸入的密碼）。

1. 變更目標**資料庫名稱**其中一項關聯式資料庫。

   ![連接到主要執行個體](./media/quickstart-big-data-cluster-deploy/connect-to-cluster.png)

1. 按下**Connect**，而**Server 儀表板**應該會出現。

### <a id="hdfs"></a> HDFS/Spark 閘道

**HDFS/Spark 閘道**可讓您連接才能使用 HDFS 儲存體集區，並執行 Spark 作業。 下列步驟說明如何使用 Azure Data Studio 來連線。

1. 從命令列中，尋找您的 HDFS/Spark 閘道，使用下列命令的 IP 位址：

   ```
   kubectl get svc service-security-lb -n <your-cluster-name>
   ```
 
1. 在 Azure Data Studio，按下**F1** > **新連線**。

1. 在 **連線類型**，選取**巨量資料的 SQL Server 叢集**。
   
   > [!TIP]
   > 如果您看不見**巨量資料的 SQL Server 叢集**連線類型，請確定您已安裝[SQL Server 2019 延伸模組](../azure-data-studio/sql-server-2019-extension.md)和您在完成的延伸模組後重新啟動 Azure Data Studio正在安裝。

1. 輸入中的巨量資料叢集的 IP 位址**伺服器名稱**（不指定連接埠）。

1. 請輸入`root`for**使用者**並指定**密碼**至您在部署指令碼中所輸入的巨量資料叢集。

   ![連線到 HDFS/Spark 閘道](./media/quickstart-big-data-cluster-deploy/connect-to-cluster-hdfs-spark.png)

1. 按下**Connect**，而**Server 儀表板**應該會出現。

## <a name="clean-up"></a>清除

如果您要測試 SQL Server 的巨量資料叢集在 Azure 中，您應該刪除 AKS 叢集，以避免產生非預期的費用所完成。 請勿移除叢集中，如果您想要繼續使用它。

> [!WARNING]
> 下列步驟會終止移除 SQL Server 巨量資料叢集 AKS 叢集。 如果您有任何資料庫或您想要保留的 HDFS 資料，該資料前先備份刪除叢集。

執行下列 Azure CLI 命令來移除 Azure 中的巨量資料叢集和 AKS 服務 (取代`<resource group name>`具有**Azure 資源群組**您在部署指令碼中指定):

```azurecli
az group delete -n <resource group name>
```

## <a name="next-steps"></a>後續步驟

既然已經部署的 SQL Server 的巨量資料叢集，您可以載入範例資料，並瀏覽教學課程：

> [!div class="nextstepaction"]
> [教學課程：將範例資料載入 SQL Server 2019 巨量資料叢集](tutorial-load-sample-data.md)