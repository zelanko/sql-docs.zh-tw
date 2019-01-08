---
title: 部署快速入門
titleSuffix: SQL Server 2019 big data clusters
description: 逐步解說部署的 SQL Server 2019 巨量資料叢集 （預覽） 在 Azure Kubernetes Service (AKS)。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/07/2018
ms.topic: quickstart
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: f5ddd80eaf29db657c42eec5c84c8485e8b0d8b6
ms.sourcegitcommit: 85fd3e1751de97a16399575397ab72ebd977c8e9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/17/2018
ms.locfileid: "53531153"
---
# <a name="quickstart-deploy-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>快速入門：部署 Azure Kubernetes Service (AKS) 上的 SQL Server 巨量資料叢集

在本快速入門中，您將部署在 AKS 上的 SQL Server 2019 巨量資料叢集 （預覽） 適用於開發/測試環境的預設組態中。

> [!NOTE]
> AKS 是主機 Kubernetes 只在一個位置。 巨量資料叢集可以部署到 Kubernetes，不論基礎結構。 如需詳細資訊，請參閱 <<c0> [ 如何部署 SQL Server 的巨量資料叢集的 Kubernetes 上](deployment-guidance.md)。

除了 SQL Master 執行個體中，叢集會包含一個計算集區執行個體、 一個資料集區執行個體和兩個儲存體集區執行個體。 資料會保存使用使用 AKS 預設儲存體類別的 Kubernetes 永續性磁碟區。 若要進一步自訂您的組態，請參閱中的環境變數[部署指引](deployment-guidance.md)。

如果您想要執行指令碼來建立 AKS 叢集並安裝在同一時間的巨量資料叢集，請參閱[部署巨量資料叢集的 Azure Kubernetes Service (AKS) 上的 SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/aks)。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="prerequisites"></a>先決條件

本快速入門需要您具有 v1.10 的最低版本設定 AKS 叢集。 如需詳細資訊，請參閱 <<c0> [ 部署在 AKS 上](deploy-on-aks.md)指南。

- [SQL Server 2019 巨量資料工具](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
   - **kubectl**
   - **mssqlctl**

## <a name="verify-aks-configuration"></a>確認 AKS 組態

一旦您有部署 AKS 叢集時，您可以執行下列 kubectl 命令以檢視叢集組態。 請確定該 kubectl 指向正確的叢集內容。

```bash
kubectl config view
```

## <a name="define-environment-variables"></a>定義環境變數

稍微部署巨量資料叢集所需的環境變數設定，需視您是否使用 Windows 或 Linux/macOS 用戶端的方法而有所不同。  選擇執行下列步驟根據哪一個作業系統使用。

在繼續之前，請注意下列重要指導方針：

- 在 [命令視窗](https://docs.microsoft.com/visualstudio/ide/reference/command-window)，引號括住包含環境變數中。 如果您可以使用引號括住来包裝的密碼，密碼中包含引號。
- 在 bash 中，引號不包含在變數中。 我們的範例中使用雙引號括住`"`。
- 可以為任何您喜歡，設定密碼環境變數，但請確定它們已夠複雜，而且不使用`!`， `&`，或`'`字元。
- `sa`帳戶是在安裝期間建立的 SQL Server Master 執行個體上的系統管理員。 建立您的 SQL Server 容器之後，在容器中執行 `echo $MSSQL_SA_PASSWORD`，即可探索您指定的 `MSSQL_SA_PASSWORD` 環境變數。 基於安全考量，變更您`sa`根據所述的最佳作法的密碼[這裡](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker?view=sql-server-2017#change-the-sa-password)。

初始化下列環境變數。  所需要的部署巨量資料叢集：

### <a name="windows"></a>視窗

使用命令視窗 (非 PowerShell)，設定下列環境變數：

```cmd
SET ACCEPT_EULA=Y
SET CLUSTER_PLATFORM=aks

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

### <a name="linuxmacos"></a>Linux/macOS

初始化下列環境變數：

```bash
export ACCEPT_EULA="Y"
export CLUSTER_PLATFORM="aks"

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

> [!NOTE]
> 有限公開預覽期間，若要下載 SQL Server 的巨量資料叢集映像的 Docker 認證是 Microsoft 提供給每位客戶。 若要要求存取權，註冊[此處](https://aka.ms/eapsignup)，並指定您要試用 SQL Server 的巨量資料叢集的興趣。

## <a name="deploy-a-big-data-cluster"></a>部署巨量資料叢集

若要部署 Kubernetes 叢集上的 SQL Server 2019 CTP 2.2 巨量資料叢集，請執行下列命令：

```bash
mssqlctl create cluster <your-cluster-name>
```

> [!NOTE]
> 您的叢集名稱必須是只有大小寫英數字元，不含空格。 適用於巨量資料叢集的所有 Kubernetes 成品將會都建立與叢集名稱相同的命名空間中指定的名稱。

在命令視窗或殼層未傳回的部署狀態。 您也可以在不同的 cmd 視窗執行下列命令來檢查部署狀態：

```bash
kubectl get all -n <your-cluster-name>
kubectl get pods -n <your-cluster-name>
kubectl get svc -n <your-cluster-name>
```

您可以執行，以查看更細微的 「 狀態 」 和 「 每個 pod 的組態：
```bash
kubectl describe pod <pod name> -n <your-cluster-name>
```

> [!TIP]
> 如需如何監視和疑難排解部署的詳細資訊，請參閱 <<c0> [ 部署疑難排解](deployment-guidance.md#troubleshoot)的部署指引文件的區段。

## <a name="open-the-cluster-administration-portal"></a>開啟叢集管理入口網站

當控制器 pod 執行時，您可以使用叢集系統管理入口網站來監視部署。 您可以存取入口網站中使用的外部 IP 位址和連接埠號碼`service-proxy-lb`(例如： **https://\<ip 位址\>: 30777/入口網站**)。 認證為存取管理員入口網站的值`CONTROLLER_USERNAME`和`CONTROLLER_PASSWORD`上面提供的環境變數。

您可以在 bash 或 cmd 視窗執行下列命令來取得服務-proxy-l b 服務的 IP 位址：

```bash
kubectl get svc service-proxy-lb -n <your-cluster-name>
```

> [!NOTE]
> 存取網頁，因為我們使用自動產生的 SSL 憑證時，您會看到安全性警告。 在未來版本中，我們將提供的功能，可提供您自己的簽署的憑證。

## <a name="connect-to-the-big-data-cluster"></a>連線至巨量資料叢集

部署指令碼已順利完成之後，您可以取得 IP 位址的 SQL Server 的主要執行個體和 Spark/HDFS 結束點，使用下面所述的步驟。 所有的叢集端點會顯示在 叢集系統管理入口網站，以及以方便參考的服務端點一節。

Azure 提供 AKS Azure 負載平衡器服務。 執行下列命令，在 cmd 或 bash 視窗：

```bash
kubectl get svc endpoint-master-pool -n <your-cluster-name>
kubectl get svc service-security-lb -n <your-cluster-name>
```

尋求**EXTERNAL-IP**值，指派給服務。 連接到 SQL Server 主要執行個體使用的 IP 位址`endpoint-master-pool`在連接埠 31433 (例如：  **\<ip 位址\>31433、**) 以及 SQL Server 巨量資料叢集端點使用的外部 IP`service-security-lb`服務。   巨量資料叢集端點是您可以在其中與 HDFS 互動並提交 Spark 作業，透過 Knox。

## <a name="next-steps"></a>後續步驟

既然已經部署的 SQL Server 的巨量資料叢集，請試試看一些新功能：

> [!div class="nextstepaction"]
> [如何在 SQL Server 2019 預覽中使用 notebook](notebooks-guidance.md)
