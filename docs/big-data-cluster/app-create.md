---
title: 使用 azdata 部署應用程式
titleSuffix: SQL Server Big Data Clusters
description: 在 SQL Server 2019 巨量資料叢集上將 Python 或 R 指令碼部署為應用程式。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 890b029833e7d34da7663b9f0e6ccfa63195c6d5
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725079"
---
# <a name="how-to-deploy-an-app-on-sql-server-big-data-clusters"></a>如何在 SQL Server 巨量資料叢集上部署應用程式

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

在 SQL Server 巨量資料叢集 (BDC) 上部署的應用程式不僅可以受益於許多優點 (例如叢集的計算能力)，還能夠存取叢集上可用的大量資料。 其會大幅提升效能，因為您的應用程式會位於資料所在的同一個叢集中。

此文章描述如何將 R 與 Python 指令碼，當作 SQL Server 巨量資料叢集內的應用程式來部署及管理。

## <a name="whats-new-and-improved"></a>新功能和改善的項目

- 用來管理叢集和應用程式的單一命令列公用程式。
- 簡化的應用程式部署，同時透過規格檔案提供更細微的控制。
- 支援裝載其他應用程式類型：SQL Server Integration Services (SSIS) 和 MLeap。
- 管理應用程式部署的 [Visual Studio Code 延伸模組](app-deployment-extension.md)。

使用 `azdata` 命令列公用程式來部署和管理應用程式。 本文提供從命令列部署應用程式的範例。 若要了解如何在 Visual Studio Code 中使用此功能，請參閱 [Visual Studio Code 延伸模組](app-deployment-extension.md)。

支援下列類型的應用程式：

- **Python** - 適用於各種角色 (例如資料工程師、資料科學家或 DevOps 工程師) 的其中一種最受歡迎的一般程式設計語言，可支援許多案例 (例如資料整頓、自動化、原型設計)。在某種程度上，其也逐漸普遍用於企業級應用程式的設計上，並搭配 Web 開發架構 (例如 Flask 和 Django) 來解決不同的商務需求。  
- **R** - 適用於資料工程和資料科學家的另一種熱門程式設計語言。 相較於 Python，R 是一種更加著重在統計計算和圖形上的程式設計語言。  
- **SQL Server Integration Services (SSIS)** - 適用於建置 ETL 套件及加以偵錯的高效能資料整合解決方案，其使用的資料轉換服務套件檔案格式 (DTSX) 是一種 XML 型的檔案格式，可儲存處理資料庫之間的資料移轉，以及整合外部資料來源的指示。   
- **MLeap** - 一種常見的序列化格式，能提供執行和序列化 SparkML 管線以及其他所需的一切，並接著在執行階段載入，以近即時且接近資料的方式處理 ML 評分工作。  

## <a name="prerequisites"></a>Prerequisites

- [SQL Server 2019 巨量資料叢集](deployment-guidance.md)
- [azdata 命令列公用程式](../azdata/install/deploy-install-azdata.md)

## <a name="capabilities"></a>功能

在 SQL Server 2019 中，您可以建立、刪除、描述、初始化、列出執行及更新您的應用程式。 下表描述您可以搭配 **azdata** 使用的應用程式部署命令。

|Command |描述 |
|:---|:---|
|`azdata login` | 登入 SQL Server 巨量資料叢集 |
|`azdata app create` | 建立應用程式。 |
|`azdata app delete` | 刪除應用程式。 |
|`azdata app describe` | 描述應用程式。 |
|`azdata app init` | 快速啟動新的應用程式基本架構。 |
|`azdata app list` | 列出應用程式。 |
|`azdata app run` | 執行應用程式。 |
|`azdata app update`| 更新應用程式。 |

您可以使用 `--help` 參數取得協助，如下列範例所示：

```bash
azdata app create --help
```

下列各節會詳細描述這些命令。

## <a name="sign-in"></a>登入

在您部署應用程式或與其互動之前，請先使用 `azdata login` 命令登入您的 SQL Server 巨量資料叢集。 指定 `controller-svc-external` 服務的外部 IP 位址 (例如：`https://ip-address:30080`)，以及叢集的使用者名稱和密碼。

```bash
azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
```

## <a name="azure-kubernetes-service-aks"></a>Azure Kubernetes Service (AKS)

如果您使用 AKS，則需要執行下列命令來取得 `controller-svc-external` 服務的 IP 位址，方法是在 bash 或 cmd 視窗中執行此命令：


```bash
kubectl get svc controller-svc-external -n <name of your big data cluster>
```

## <a name="kubernetes-clusters-created-with-kubeadm"></a>使用 kubeadm 建立的 Kubernetes 叢集

執行下列命令以取得要登入叢集的 IP 位址

```bash
kubectl get node --selector='node-role.kubernetes.io/master'
```

## <a name="create-an-app-skeleton"></a>建立應用程式基本架構

**azdata app init** 命令會提供 Scaffold，其中包含部署應用程式所需的相關成品。 下列範例會建立 add-app，您可以透過執行下列命令來完成。

```bash
azdata app init --name add-app --version v1 --template python
```

這會建立稱為 hello 的資料夾。  您可以使用 `cd` 命令進入目錄，並檢查資料夾中產生的檔案。 spec.yaml 會定義應用程式 (例如名稱、版本和原始程式碼)。 您可以編輯規格來變更名稱、版本、輸入和輸出。

以下是您將會在資料夾中看到的 init 命令範例輸出

```
add-app.py
run-spec.yaml
spec.yaml
```

## <a name="create-an-app"></a>建立應用程式

若要建立應用程式，您可以使用 `azdata` 搭配 `app create` 命令。 這些檔案位於您用來建立應用程式的本機電腦上。

使用下列語法，在巨量資料叢集中建立新的應用程式：

```bash
azdata app create --spec <directory containing spec file>
```

下列命令顯示此命令可能的外觀範例：

```bash
azdata app create --spec ./addpy
```

這會假設您已將應用程式儲存在 `addpy` 資料夾中。 此資料夾也應該包含應用程式的規格檔案，稱為 `spec.yaml`。 如需詳細資訊，請參閱關於 `spec.yaml` 檔案的[應用程式部署頁面](concept-application-deployment.md)。

若要部署此應用程式範例應用程式請在稱為 `addpy` 的目錄中建立下列檔案：

- `add.py`. 將下列 Python 程式碼複製到此檔案中：
   ```py
   #add.py
  def add(x, y):
    result = x+y
    return result
  result=add(x,y)
   ```
- `spec.yaml`. 將下列程式碼複製到此檔案中：
   ```yaml
   #spec.yaml
   name: add-app #name of your python script
   version: v1  #version of the app
   runtime: Python #the language this app uses (R or Python)
   src: ./add.py #full path to the location of the app
   entrypoint: add #the function that will be called upon execution
   replicas: 1  #number of replicas needed
   poolsize: 1  #the pool size that you need your app to scale
   inputs:  #input parameters that the app expects and the type
     x: int
     y: int
   output: #output parameter the app expects and the type
     result: int
   ```

然後執行下列命令：

```bash
azdata app create --spec ./addpy
```

您可以使用 list 命令來檢查是否已部署應用程式：

```bash
azdata app list
```

如果部署未完成，您應該會看到 `state` 顯示 `WaitingforCreate`，如下列範例所示：

```json
[
  {
    "name": "add-app",
    "state": "WaitingforCreate",
    "version": "v1"
  }
]
```

部署成功之後，您應該會看到 `state` 變更為 `Ready` 狀態：

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="list-an-app"></a>列出應用程式

您可以使用 `app list` 命令來列出任何已成功建立的應用程式。

下列命令會列出您巨量資料叢集中所有可用的應用程式：

```bash
azdata app list
```

如果您指定名稱和版本，則會列出該特定應用程式及其狀態 (正在建立或已就緒)：

```bash
azdata app list --name <app_name> --version <app_version>
```

下列範例示範此命令：

```bash
azdata app list --name add-app --version v1
```

您應該會看到類似下列範例的結果：

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="delete-an-app"></a>刪除應用程式

若要從您的巨量資料叢集中刪除應用程式，請使用下列語法：

```bash
azdata app delete --name add-app --version v1
```

## <a name="next-steps"></a>後續步驟

若要探索如何在自己的應用程式中整合於 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 上部署的應用程式，請參閱[在巨量資料叢集上執行應用程式](app-run.md)和[取用巨量資料叢集上的應用程式](app-consume.md)以取得詳細資訊。 您也可以在[應用程式部署範例](https://aka.ms/sql-app-deploy)中查看其他範例。

如需 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。