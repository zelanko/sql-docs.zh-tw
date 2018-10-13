---
title: 部署 SQL Server 的巨量資料叢集 |Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: quickstart
ms.prod: sql
ms.openlocfilehash: 5781b3acfd2262b3a3be540abb331839dfcc56c6
ms.sourcegitcommit: 08b3de02475314c07a82a88c77926d226098e23f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/12/2018
ms.locfileid: "49120455"
---
# <a name="quickstart-deploy-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>快速入門： 部署 Azure Kubernetes Service (AKS) 上的 SQL Server 巨量資料叢集

在本快速入門中，您會安裝在 AKS 上巨量資料的 SQL Server 叢集的預設組態適用於開發/測試環境中。 除了 SQL Master 執行個體，叢集會包含一個計算集區執行個體、 一個資料集區執行個體和兩個儲存體集區執行個體。 將會使用佈建在 AKS 的預設儲存體類別上的 Kubernetes 永續性磁碟區來保存資料。 在 [部署指引](deployment-guidance.md)主題，您可以找到一組環境變數可供您進一步自訂您的設定。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="prerequisites"></a>先決條件

本快速入門需要您具有 v1.10 的最低版本設定 AKS 叢集。 如需詳細資訊，請參閱 <<c0> [ 部署在 AKS 上](deploy-on-aks.md)指南。

在電腦上用來執行命令來安裝 SQL Server 的巨量資料叢集，您必須安裝[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)。 SQL Server 的巨量資料叢集需要 1.10 版本，如 Kubernetes、 伺服器和用戶端 (kubectl)。 若要安裝 kubectl，請參閱[安裝 kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl)。 

若要安裝`mssqlctl`CLI 工具來管理 SQL Server 的巨量資料叢集化您的用戶端電腦上，您必須先安裝[Python](https://www.python.org/downloads/)最低版本 v3.0 並[pip3](https://pip.pypa.io/en/stable/installing/)。 請注意是否您使用最少 3.4 從下載的 Python 版本，已安裝 pip [python.org](https://www.python.org/)。

如果您的 Python 安裝遺漏`requests`套件，您必須安裝`requests`使用`python -m pip install requests`。 如果您已經有`requests`封裝升級至最新版本使用`python -m pip install requests --upgrade`。

## <a name="verify-aks-configuration"></a>確認 AKS 組態

一旦您有部署 AKS 叢集時，您可以執行下列 kubectl 命令以檢視叢集組態。 請確定該 kubectl 指向正確的叢集內容。

```bash
kubectl config view
```

## <a name="install-mssqlctl-cli-management-tool"></a>安裝 mssqlctl CLI 管理工具

執行下列命令來安裝`mssqlctl`用戶端電腦上的工具。 相同的命令適用於 Windows 和 Linux 用戶端，但請確定您從 Windows 以系統管理權限執行的 cmd 視窗中執行它，或您在它前面加`sudo`Linux 上：

```
pip3 install --index-url https://private-repo.microsoft.com/python/ctp-2.0 mssqlctl  
```

## <a name="define-environment-variables"></a>定義環境變數

稍微部署巨量資料叢集所需的環境變數設定，需視您是否使用 Windows 或 Linux/macOS 用戶端的方法而有所不同。  選擇執行下列步驟根據哪一個作業系統使用。

在繼續之前，請注意下列重要指導方針：

- 請確定您將包裝密碼雙引號括住，如果它包含任何特殊字元。 請注意，雙引號括住分隔符號僅適用於 bash 命令。
- 可以為任何您喜歡，設定密碼環境變數，但請確定它們已夠複雜，而且不使用`!`， `&`，或`‘`字元。
- CTP 2.0 版本中，不會變更預設連接埠。
- **SA**帳戶是在安裝期間建立的 SQL Server Master 執行個體上的系統管理員。 建立您的 SQL Server 容器，您所指定的 MSSQL_SA_PASSWORD 環境變數設定為可探索執行後回應在容器中的 $MSSQL_SA_PASSWORD。 基於安全考量，變更您的 SA 密碼，根據所述的最佳作法[此處](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker?view=sql-server-2017#change-the-sa-password)。

初始化下列環境變數。  所需要的部署巨量資料叢集：

### <a name="windows"></a>Windows

使用命令提示字元 視窗 (非 PowerShell)，設定下列環境變數：

```cmd
SET ACCEPT_EULA=Y
SET CLUSTER_PLATFORM=aks

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

### <a name="linuxmacos"></a>Linux/macOS

初始化下列環境變數：

```bash
export ACCEPT_EULA=Y
export CLUSTER_PLATFORM=aks

export CONTROLLER_USERNAME=<controller_admin_name – can be anything>
export CONTROLLER_PASSWORD=<controller_admin_password – can be anything, password complexity compliant>
export KNOX_PASSWORD=<knox_password – can be anything, password complexity compliant>
export MSSQL_SA_PASSWORD=<sa_password_of_master_sql_instance, password complexity compliant>

export DOCKER_REGISTRY=private-repo.microsoft.com
export DOCKER_REPOSITORY=mssql-private-preview
export DOCKER_USERNAME=<your username, credentials provided by Microsoft>
export DOCKER_PASSWORD=<your password, credentials provided by Microsoft>
export DOCKER_EMAIL=<your Docker email, use the username provided by Microsoft>
export DOCKER_PRIVATE_REGISTRY="1"
```

> [!NOTE]
> 有限公開預覽期間，若要下載 SQL Server 的巨量資料叢集映像的 Docker 認證是 Microsoft 提供給每位客戶。 若要要求存取權，註冊[此處](https://aka.ms/eapsignup)，並指定您要試用 SQL Server 的巨量資料叢集的興趣。

## <a name="deploy-a-big-data-cluster"></a>部署巨量資料叢集

若要部署 Kubernetes 叢集上的 SQL Server 2019 CTP 2.0 巨量資料叢集，請執行下列命令：

```bash
mssqlctl create cluster <name of your cluster>
```

> [!NOTE]
> 您的叢集名稱必須是只有大小寫英數字元，不含空格。 適用於巨量資料叢集的所有 Kubernetes 成品將會都建立與叢集名稱相同的命名空間中指定的名稱。


[命令] 視窗會將輸出的部署狀態。 您也可以在不同的 cmd 視窗執行下列命令來檢查部署狀態：

```bash
kubectl get all -n <name of your cluster>
kubectl get pods -n <name of your cluster>
kubectl get svc -n <name of your cluster>
```

您可以執行，以查看更細微的 「 狀態 」 和 「 每個 pod 的組態：
```bash
kubectl describe pod <pod name> -n <name of your cluster>
```

當控制器 pod 執行時，您可以使用叢集系統管理入口網站來監視部署。 您可以存取入口網站中使用的外部 IP 位址和連接埠號碼`service-proxy-lb`(例如： **https://\<ip 位址\>: 30777**)。 認證為存取管理員入口網站的值`CONTROLLER_USERNAME`和`CONTROLLER_PASSWORD`上面提供的環境變數。

您可以在 bash 或 cmd 視窗執行下列命令來取得服務-proxy-l b 服務的 IP 位址：

```bash
kubectl get svc service-proxy-lb -n <name of your cluster>
```

> [!NOTE]
> 存取網頁，因為我們使用自動產生的 SSL 憑證時，您會看到安全性警告。 在未來版本中，我們將提供的功能，可提供您自己的簽署的憑證。
 

## <a name="connect-to-the-big-data-cluster"></a>連線至巨量資料叢集

部署指令碼已順利完成之後，您可以取得 IP 位址的 SQL Server 的主要執行個體和 Spark/HDFS 結束點，使用下面所述的步驟。 所有的叢集端點會顯示在 叢集系統管理入口網站，以及以方便參考的服務端點一節。

Azure 提供 AKS Azure 負載平衡器服務。 執行下列命令，在 cmd 或 bash 視窗：

```bash
kubectl get svc service-master-pool-lb -n <name of your cluster>
kubectl get svc service-security-lb -n <name of your cluster>
```

尋求**EXTERNAL-IP**值，指派給服務。 連接到 SQL Server 主要執行個體使用的 IP 位址`service-master-pool-lb`在連接埠 31433 (例如：  **\<ip 位址\>31433、**) 以及 SQL Server 巨量資料叢集端點使用的外部 IP`service-security-lb`服務。   巨量資料叢集端點是您可以在其中與 HDFS 互動並提交 Spark 作業，透過 Knox。

## <a name="next-steps"></a>後續步驟

既然已經部署的 SQL Server 的巨量資料叢集，請試試看一些新功能：

> [!div class="nextstepaction"]
> [如何在 SQL Server 2019 預覽中使用 notebook](notebooks-guidance.md)
