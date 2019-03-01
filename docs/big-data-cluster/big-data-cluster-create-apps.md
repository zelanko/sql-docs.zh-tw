---
title: 使用 mssqlctl 部署應用程式
titleSuffix: SQL Server 2019 big data clusters
description: 將 Python 或 R 指令碼部署為 SQL Server 2019 巨量資料叢集 （預覽） 上的應用程式。
author: TheBharath
ms.author: bharaths
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 6d0f5fba93b74aa5751635c9a10f320c85036bbb
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57017824"
---
# <a name="how-to-deploy-an-app-on-sql-server-2019-big-data-cluster-preview"></a>如何部署 SQL Server 2019 巨量資料叢集 （預覽） 上的應用程式

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

在 SQL Server 2019 （預覽） CTP 2.3 您可以建立、 刪除、 描述、 初始化，清單會執行，並更新您的應用程式。 下表描述您可以搭配使用的應用程式部署命令**mssqlctl**。

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

## <a name="log-in"></a>登入

在您部署或應用程式互動之前，先到巨量資料叢集與 SQL Server 登入`mssqlctl login`命令。 指定的外部 IP 位址`endpoint-service-proxy`服務 (例如： `https://ip-address:30777`) 以及使用者名稱和密碼，在叢集中。

```bash
mssqlctl login -e https://<ip-address-of-endpoint-service-proxy>:30777 -u <user-name> -p <password>
```

## <a name="aks"></a>AKS

如果您使用 AKS，您需要執行下列命令來取得的 IP 位址`endpoint-service-proxy`服務中的 bash 或 cmd 視窗執行下列命令：


```bash
kubectl get svc endpoint-service-proxy -n <name of your cluster>
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
mssqlctl app create -n <app_name> -v <version_number> --spec <directory containing spec file>
```

下列命令會顯示此命令可能如下所示的範例：

這是假設您有稱為檔案`spec.yaml`內`addpy`資料夾。 `addpy`資料夾包含`add.py`並`spec.yaml``spec.yaml`規格檔案`add.py`應用程式。


`add.py` 會建立下列的 python 應用程式： 

```py
#add.py
def add(x,y):
        result = x+y
        return result;
result=add(x,y)
```

下列指令碼是範例的目錄`spec.yaml`:

```yaml
#spec.yaml
name: add-app #name of your python script
version: v1  #version of the app 
runtime: Python #the languge this app uses (R or Python)
src: ./add.py #full path to the loction of the app
entrypoint: add #the function that will be called upon execution
replicas: 1  #number of replicas needed
poolsize: 1  #the pool size that you need your app to scale
inputs:  #input parameters that the app expects and the type
  x: int
  y: int
output: #output parameter the app expects and the type
  result: int
```

若要這麼做，將以上幾行程式碼複製到目錄中的兩個檔案`addpy`作為`add.py`和`spec.yaml`並執行下列命令：

```bash
mssqlctl app create --spec ./addpy
```

您可以檢查應用程式會使用 list 命令來部署：

```bash
mssqlctl app list
```

如果部署未完成您應該會看到`state`顯示`WaitingforCreate`在下列範例所示： 

```
[
  {
    "name": "add-app",
    `state`: "WaitingforCreate",
    "version": "v1"
  }
]
```

部署成功之後，您應該會看到`state`變更為`Ready`狀態：

```
[
  {
    "name": "add-app",
    `state`: `Ready`,
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

```
[
  {
    "name": "add-app",
    `state`: `Ready`,
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

```
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

Init 命令會提供與部署應用程式需要相關成品的 scaffold。 下列範例會建立 hello，您可以藉由執行下列命令。

```
mssqlctl app init --name hello --version v1 --template python
```

這會建立名為 hello 的資料夾。  您可以移至目錄，並檢查資料夾中產生的檔案。 spec.yaml 定義應用程式，例如名稱、 版本和原始檔的程式碼。 您可以編輯以變更名稱、 版本、 輸入和輸出的規格。

以下是範例的輸出資料夾中，您會看到 init 指令

```
hello.py
README.md
run-spec.yaml
spec.yaml

```

## <a name="describe-an-app"></a>描述應用程式

描述命令提供應用程式，包括您的叢集中的結束點的詳細的資訊。 這通常是由應用程式開發人員建置應用程式使用 swagger 的用戶端，並使用 web 服務的應用程式互動以 RESTful 方式。

```
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
  `state`: `Ready`,
  "version": "v1"
}

```

## <a name="delete-an-app"></a>刪除應用程式

若要從您的巨量資料叢集刪除應用程式，請使用下列語法：

```bash
mssqlctl app delete --name add-app --version v1
```

## <a name="next-steps"></a>後續步驟

您也可以查看其他樣本[應用程式部署範例](https://aka.ms/sql-app-deploy)。

如需有關 SQL Server 的巨量資料叢集的詳細資訊，請參閱 <<c0> [ 什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)。
