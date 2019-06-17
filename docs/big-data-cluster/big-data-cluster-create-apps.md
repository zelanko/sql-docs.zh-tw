---
title: 使用 mssqlctl 部署應用程式
titleSuffix: SQL Server big data clusters
description: 將 Python 或 R 指令碼部署為 SQL Server 2019 巨量資料叢集 （預覽） 上的應用程式。
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: aa95621178b26becd5985fd60b7b2d3588607d17
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66801865"
---
# <a name="how-to-deploy-an-app-on-sql-server-big-data-cluster-preview"></a>如何部署 SQL Server 的巨量資料叢集 （預覽） 上的應用程式

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何部署和管理 R 和 Python 指令碼中的 SQL Server 2019 巨量資料叢集 （預覽） 的應用程式。

## <a name="whats-new-and-improved"></a>全新和改進的功能

- 單一命令列公用程式來管理叢集和應用程式。
- 簡化應用程式部署，同時提供更精確地控制透過規格的檔案。
- 支援裝載其他應用程式類型-SSIS 和 MLeap （新功能 CTP 2.3)
- [VS Code 延伸模組](app-deployment-extension.md)來管理應用程式部署

應用程式部署及管理使用`mssqlctl`命令列公用程式。 本文章提供有關如何從命令列部署應用程式的範例。 若要了解如何使用這個 Visual Studio Code 中參考[VS Code 延伸模組](app-deployment-extension.md)。

支援下列類型的應用程式：
- R 和 Python 應用程式 （函數、 模型和應用程式）
- MLeap 服務
- SQL Server Integration Services (SSIS)

## <a name="prerequisites"></a>先決條件

- [SQL Server 2019 巨量資料叢集](deployment-guidance.md)
- [mssqlctl 命令列公用程式](deploy-install-mssqlctl.md)

## <a name="capabilities"></a>Capabilities

在 SQL Server 2019 （預覽） CTP 3.0 您可以建立、 刪除、 描述、 初始化，清單會執行，並更新您的應用程式。 下表描述您可以搭配使用的應用程式部署命令**mssqlctl**。

|命令 |描述 |
|:---|:---|
|`mssqlctl login` | 登入 SQL Server 的巨量資料叢集 |
|`mssqlctl app create` | 建立應用程式。 |
|`mssqlctl app delete` | 刪除應用程式。 |
|`mssqlctl app describe` | 說明應用程式。 |
|`mssqlctl app init` | 新應用程式基本架構著手進行。 |
|`mssqlctl app list` | 列出應用程式。 |
|`mssqlctl app run` | 執行應用程式。 |
|`mssqlctl app update`| 更新應用程式。 |

您可以取得說明`--help`參數，如下列範例所示：

```bash
mssqlctl app create --help
```

下列各節說明這些命令的更多詳細資料。

## <a name="sign-in"></a>登入

您部署或應用程式互動之前，先登入您的 SQL Server 使用巨量資料叢集`mssqlctl login`命令。 指定的外部 IP 位址`controller-svc-external`服務 (例如： `https://ip-address:30080`) 以及使用者名稱和密碼，在叢集中。

```bash
mssqlctl login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
```

## <a name="aks"></a>AKS

如果您使用 AKS，您需要執行下列命令來取得的 IP 位址`mgmtproxy-svc-external`服務中的 bash 或 cmd 視窗執行下列命令：


```bash
kubectl get svc mgmtproxy-svc-external -n <name of your big data cluster>
```

## <a name="kubeadm-or-minikube"></a>Kubeadm 或 Minikube

如果您使用 Kubeadm 或 Minikube 執行下列命令來取得登入到叢集的 IP 位址

```bash
kubectl get node --selector='node-role.kubernetes.io/master'
```

## <a name="create-an-app"></a>建立應用程式

若要建立應用程式，您使用`mssqlctl`與`app create`命令。 這些檔案位在本機建立的應用程式的電腦上。

在巨量資料叢集中建立新的應用程式中使用下列語法：

```bash
mssqlctl app create --spec <directory containing spec file>
```

下列命令會顯示此命令可能如下所示的範例：

```bash
mssqlctl app create --spec ./addpy
```

這是假設您有儲存在您的應用程式`addpy`資料夾。 此資料夾也應包含的應用程式中，然後再呼叫被呼叫的規格檔`spec.yaml`。 請參閱[應用程式部署頁面](concept-application-deployment.md)如需有關`spec.yaml`檔案。

若要部署此應用程式範例應用程式，請在呼叫的目錄中建立下列檔案`addpy`:

- `add.py`. 將下列 Python 程式碼複製到這個檔案：
   ```py
   #add.py
   def add(x,y):
        result = x+y
        return result
    result=add(x,y)
   ```
- `spec.yaml`. 將下列程式碼複製到這個檔案：
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

然後，執行下列命令：

```bash
mssqlctl app create --spec ./addpy
```

您可以檢查應用程式會使用 list 命令來部署：

```bash
mssqlctl app list
```

如果部署未完成您應該會看到`state`顯示`WaitingforCreate`在下列範例所示：

```json
[
  {
    "name": "add-app",
    "state": "WaitingforCreate",
    "version": "v1"
  }
]
```

部署成功之後，您應該會看到`state`變更為`Ready`狀態：

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

您可以列出任何應用程式已成功建立與`app list`命令。

下列命令會列出所有可用的應用程式，在您的巨量資料叢集：

```bash
mssqlctl app list
```

如果您指定的名稱和版本，它會列出該特定的應用程式和其狀態 （「 建立 」 或 「 就緒 」）：

```bash
mssqlctl app list --name <app_name> --version <app_version>
```

下列範例示範此命令：

```bash
mssqlctl app list --name add-app --version v1
```

您應該會看到類似下列範例輸出：

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="run-an-app"></a>執行應用程式

如果應用程式處於`Ready`狀態時，您可以執行與您指定的輸入參數來使用。 若要執行的應用程式中使用下列語法：

```bash
mssqlctl app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

下列範例命令示範如何執行的命令：

```bash
mssqlctl app run --name add-app --version v1 --inputs x=1,y=2
```

如果執行成功，您應該會看到您的輸出，因為您在建立應用程式時指定。 以下是一個範例。

```json
{
  "changedFiles": [],
  "consoleOutput": "",
  "errorMessage": "",
  "outputFiles": {},
  "outputParameters": {
    "result": 3
  },
  "success": true
}
```

## <a name="create-an-app-skeleton"></a>建立應用程式基本架構

Init 命令提供的 scaffold 才能部署應用程式與相關的成品。 下列範例會建立 hello，您可以藉由執行下列命令。

```bash
mssqlctl app init --name hello --version v1 --template python
```

這會建立名為 hello 的資料夾。  您可以`cd`到目錄，並檢查資料夾中產生的檔案。 spec.yaml 定義應用程式，例如名稱、 版本和原始檔的程式碼。 您可以編輯以變更名稱、 版本、 輸入和輸出的規格。

以下是範例的輸出資料夾中，您會看到 init 指令

```
hello.py
README.md
run-spec.yaml
spec.yaml

```

## <a name="describe-an-app"></a>描述應用程式

描述命令提供應用程式，包括您的叢集中的結束點的詳細的資訊。 這通常是由應用程式開發人員建置應用程式使用 swagger 的用戶端，並使用 web 服務的應用程式互動以 RESTful 方式。 請參閱[巨量資料叢集上的應用程式會耗用](big-data-cluster-consume-apps.md)如需詳細資訊。

```json
{
  "input_param_defs": [
    {
      "name": "x",
      "type": "int"
    },
    {
      "name": "y",
      "type": "int"
    }
  ],
  "links": {
    "app": "https://10.1.1.3:30777/api/app/add-app/v1",
    "swagger": "https://10.1.1.3:30777/api/app/add-app/v1/swagger.json"
  },
  "name": "add-app",
  "output_param_defs": [
    {
      "name": "result",
      "type": "int"
    }
  ],
  "state": "Ready",
  "version": "v1"
}
```

## <a name="delete-an-app"></a>刪除應用程式

若要從您的巨量資料叢集刪除應用程式，請使用下列語法：

```bash
mssqlctl app delete --name add-app --version v1
```

## <a name="next-steps"></a>後續步驟

探索如何整合在您的應用程式中的巨量資料叢集的 SQL Server 上部署的應用程式[巨量資料叢集上的應用程式會耗用](big-data-cluster-consume-apps.md)如需詳細資訊。 您也可以查看其他樣本[應用程式部署範例](https://aka.ms/sql-app-deploy)。

如需有關 SQL Server 的巨量資料叢集的詳細資訊，請參閱 <<c0> [ 什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)。
