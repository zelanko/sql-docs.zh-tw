---
title: 使用 azdata 部署應用程式
titleSuffix: SQL Server big data clusters
description: 在 SQL Server 2019 big data cluster (預覽) 上, 將 Python 或 R 腳本部署為應用程式。
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 06b76e7eb8eec8db1993ca558a1f57355457c4ad
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419490"
---
# <a name="how-to-deploy-an-app-on-sql-server-big-data-cluster-preview"></a>如何在 SQL Server big data cluster (預覽) 上部署應用程式

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何部署和管理 R 和 Python 腳本, 做為 SQL Server 2019 big data cluster (預覽) 內的應用程式。

## <a name="whats-new-and-improved"></a>新功能和改進

- 用來管理叢集和應用程式的單一命令列公用程式。
- 簡化應用程式部署, 同時透過規格檔案提供更細微的控制。
- 支援裝載其他應用程式類型-SSIS 和 MLeap (CTP 2.3 中的新功能)
- 管理應用程式部署[VS Code 擴充](app-deployment-extension.md)功能

應用程式是使用`azdata`命令列公用程式來部署和管理。 本文提供如何從命令列部署應用程式的範例。 若要瞭解如何在 Visual Studio Code 中使用此功能, 請參閱[VS Code 延伸](app-deployment-extension.md)模組。

支援下列類型的應用程式:
- R 和 Python 應用程式 (功能、模型和應用程式)
- MLeap 服務
- SQL Server Integration Services (SSIS)

## <a name="prerequisites"></a>先決條件

- [SQL Server 2019 big data cluster](deployment-guidance.md)
- [azdata 命令列公用程式](deploy-install-azdata.md)

## <a name="capabilities"></a>Capabilities

在 SQL Server 2019 (預覽) 中, 您可以建立、刪除、描述、初始化、列出執行及更新您的應用程式。 下表描述您可以搭配**azdata**使用的應用程式部署命令。

|命令 |描述 |
|:---|:---|
|`azdata login` | 登入 SQL Server big data 叢集 |
|`azdata app create` | 建立應用程式。 |
|`azdata app delete` | 刪除應用程式。 |
|`azdata app describe` | 描述應用程式。 |
|`azdata app init` | Kickstart 新的應用程式基本架構。 |
|`azdata app list` | 列出應用程式。 |
|`azdata app run` | 執行應用程式。 |
|`azdata app update`| 更新應用程式。 |

如下列範例所示, `--help`您可以使用參數取得協助:

```bash
azdata app create --help
```

下列各節會更詳細地說明這些命令。

## <a name="sign-in"></a>登入

在您部署或與應用程式互動之前, 請先使用`azdata login`命令登入您的 SQL Server big data cluster。 指定`controller-svc-external`服務的外部 IP 位址 (例如: `https://ip-address:30080`), 以及叢集的使用者名稱和密碼。

```bash
azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
```

## <a name="aks"></a>AKS

如果您使用 AKS, 您需要執行下列命令來取得`mgmtproxy-svc-external`服務的 IP 位址, 方法是在 bash 或 cmd 視窗中執行此命令:


```bash
kubectl get svc mgmtproxy-svc-external -n <name of your big data cluster>
```

## <a name="kubeadm-or-minikube"></a>Kubeadm 或 Minikube

如果您使用 Kubeadm 或 Minikube, 請執行下列命令以取得要登入叢集的 IP 位址

```bash
kubectl get node --selector='node-role.kubernetes.io/master'
```

## <a name="create-an-app"></a>建立應用程式

若要建立應用程式, 您`azdata`可以使用`app create`搭配命令。 這些檔案位於您用來建立應用程式的本機電腦上。

使用下列語法在 big data 叢集中建立新的應用程式:

```bash
azdata app create --spec <directory containing spec file>
```

下列命令顯示此命令可能的樣子範例:

```bash
azdata app create --spec ./addpy
```

這會假設您已將應用程式儲存在`addpy`資料夾中。 此資料夾也應該包含應用程式的規格檔案, 稱為`spec.yaml`。 如需檔案的詳細資訊`spec.yaml` , 請參閱[應用程式部署頁面](concept-application-deployment.md)。

若要部署此應用程式範例應用程式, 請在名`addpy`為的目錄中建立下列檔案:

- `add.py`. 將下列 Python 程式碼複製到此檔案中:
   ```py
   #add.py
   def add(x,y):
        result = x+y
        return result
    result=add(x,y)
   ```
- `spec.yaml`. 將下列程式碼複製到此檔案中:
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

然後, 執行下列命令:

```bash
azdata app create --spec ./addpy
```

您可以使用 list 命令來檢查應用程式是否已部署:

```bash
azdata app list
```

如果部署未完成, 您應該會看到如`state`下列`WaitingforCreate`範例所示的顯示:

```json
[
  {
    "name": "add-app",
    "state": "WaitingforCreate",
    "version": "v1"
  }
]
```

部署成功之後, 您應該會看到`state` `Ready`狀態的變更:

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

您可以使用`app list`命令來列出已成功建立的任何應用程式。

下列命令會列出您的 big data 叢集中所有可用的應用程式:

```bash
azdata app list
```

如果您指定名稱和版本, 它會列出該特定應用程式及其狀態 (建立中或就緒):

```bash
azdata app list --name <app_name> --version <app_version>
```

下列範例示範此命令:

```bash
azdata app list --name add-app --version v1
```

您應該會看到類似下列範例的輸出:

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

如果應用程式`Ready`處於狀態, 您可以使用指定的輸入參數來加以執行。 使用下列語法來執行應用程式:

```bash
azdata app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

下列範例命令示範執行命令:

```bash
azdata app run --name add-app --version v1 --inputs x=1,y=2
```

如果執行成功, 您應該會看到您在建立應用程式時所指定的輸出。 以下是一個範例。

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

Init 命令會提供 scaffold, 其中包含部署應用程式所需的相關構件。 下列範例會藉由執行下列命令來建立您的 hello。

```bash
azdata app init --name hello --version v1 --template python
```

這會建立名為 hello 的資料夾。  您可以`cd`進入目錄, 並檢查資料夾中產生的檔案。 yaml 會定義應用程式, 例如 [名稱]、[版本] 和 [原始程式碼]。 您可以編輯規格來變更名稱、版本、輸入和輸出。

以下是 init 命令的範例輸出, 您會在資料夾中看到

```
hello.py
README.md
run-spec.yaml
spec.yaml

```

## <a name="describe-an-app"></a>描述應用程式

[描述] 命令會提供應用程式的詳細資訊, 包括叢集中的結束點。 應用程式開發人員通常會使用此方法來建立使用 swagger 用戶端的應用程式, 並使用 webservice 以 RESTful 的方式與應用程式互動。 如需詳細資訊, 請參閱[在大型資料叢集上使用應用程式](big-data-cluster-consume-apps.md)。

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

若要從您的 big data cluster 中刪除應用程式, 請使用下列語法:

```bash
azdata app delete --name add-app --version v1
```

## <a name="next-steps"></a>後續步驟

探索如何在您的應用程式中[使用大型資料叢集上的應用程式](big-data-cluster-consume-apps.md), 將部署在 SQL Server big data 叢集上的應用程式整合, 以取得詳細資訊。 您也可以參閱[應用程式部署範例](https://aka.ms/sql-app-deploy)中的其他範例。

如需有關 SQL Server big data 叢集的詳細資訊, 請參閱[什麼是 SQL Server 2019 big data 叢集？](big-data-cluster-overview.md)。
