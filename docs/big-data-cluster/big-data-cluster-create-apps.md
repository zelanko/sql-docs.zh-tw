---
title: 如何部署應用程式
titleSuffix: SQL Server 2019 big data clusters
description: 將 Python 或 R 指令碼部署為 SQL Server 2019 巨量資料叢集 （預覽） 上的應用程式。
author: TheBharath
ms.author: bharaths
manager: craigg
ms.date: 12/11/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: cca0ac5e7b81318d95fbb133758fca83e1a0742e
ms.sourcegitcommit: edf7372cb674179f03a330de5e674824a8b4118f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53246402"
---
# <a name="how-to-deploy-an-app-on-sql-server-2019-big-data-cluster-preview"></a>如何部署 SQL Server 2019 巨量資料叢集 （預覽） 上的應用程式

本文說明如何部署和管理 R 和 Python 指令碼中的 SQL Server 2019 巨量資料叢集 （預覽） 的應用程式。

部署與管理使用 R 和 Python 應用程式**mssqlctl-pre** CTP 2.2 中所含的命令列公用程式。 這篇文章提供如何將這些 R 和 Python 指令碼部署為應用程式，從命令列的範例。

## <a name="prerequisites"></a>先決條件

您必須設定的 SQL Server 2019 巨量資料叢集。 如需詳細資訊，請參閱 <<c0> [ 如何部署巨量資料叢集的 Kubernetes 的 SQL Server](deployment-guidance.md)。 

## <a name="installation"></a>安裝

**Mssqlctl-pre**命令列公用程式可用來預覽的 Python 和 R 應用程式部署功能。 您可以使用下列命令來安裝公用程式：

```cmd
pip install -r https://private-repo.microsoft.com/python/ctp-2.2/mssqlctlpre/mssqlctlpre.txt --trusted-host https://private-repo.microsoft.com
```

## <a name="capabilities"></a>Capabilities

CTP 2.2 中您可以建立、 刪除、 列出及執行 R 或 Python 應用程式。 下表描述您可以搭配使用的應用程式部署命令**mssqlctl-pre**。

| 命令 | 描述 |
|---|---|
| `mssqlctl-pre login` | 登入 SQL Server 的巨量資料叢集 |
| `mssqlctl-pre app create` | 建立應用程式 |
| `mssqlctl-pre app list` | 列出已部署的應用程式 |
| `mssqlctl-pre app delete` | 刪除應用程式 |
| `mssqlctl-pre app run` | 執行應用程式的清單 |

您可以取得說明`--help`參數，如下列範例所示：

```bash
mssqlctl-pre app create --help
```

下列各節說明這些命令的更多詳細資料。

## <a name="log-in"></a>登入

設定 R 和 Python 應用程式時，第一次登入您使用叢集的巨量資料的 SQL Server`mssqlctl-pre login`命令。 指定的外部 IP 位址`service-proxy-lb`或是`service-proxy-nodeport`服務 (例如： `https://ip-address:30777`) 以及使用者名稱和密碼，在叢集中。

您可以取得的 IP 位址**服務-proxy-lb**或**服務-proxy-nodeport**服務中的 bash 或 cmd 視窗執行下列命令：

```bash 
kubectl get svc service-proxy-lb -n <name of your cluster>
```

```bash
mssqlctl-pre login -e https://<ip-address-of-service-proxy-lb>:30777 -u <user-name> -p <password>
```

## <a name="create-an-app"></a>建立應用程式

若要建立應用程式，您會傳遞到 Python 或 R 程式碼檔案**mssqlctl-pre**與`app create`命令。 這些檔案位在本機建立的應用程式的電腦上。

在您的巨量資料叢集中建立新的應用程式中使用下列語法：

```bash
mssqlctl-pre app create -n <app_name> -v <version_number> -r <runtime> -i <path_to_code_init> -c <path_to_code> --inputs <input_params> --outputs <output_params> 
```

下列命令會顯示此命令可能如下所示的範例：

```py
#add.py
def add(x,y):
        result = x+y
        return result;
result=add(x,y)
```
若要嘗試這麼做，將以上幾行程式碼儲存到本機目錄為`add.py`並執行下列命令

```bash
mssqlctl-pre app create --name add-app --version v1 --runtime Python --code ./add.py  --inputs x=int,y=int --outputs result=int 
```

您可以檢查應用程式會使用 list 命令來部署：

```bash
mssqlctl-pre app list
```

如果部署未完成您應該會看到 「 狀態 」 顯示 「 建立 」: 

```
[
  {
    "name": "add-app",
    "state": "Creating",
    "version": "v1"
  }
]
```

部署成功之後您應該會看到 [狀態] 變更為 「 就緒 」 狀態：

```
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
mssqlctl-pre app list
```

如果您指定的名稱和版本，它會列出該特定的應用程式和它的狀態 （「 建立 」 或 「 就緒 」）：

```bash
mssqlctl-pre app list --name <app_name> --version <app_version>
```

下列範例示範此命令：

```bash
mssqlctl-pre app list --name add-app --version v1
```

您應該會看到類似下列範例輸出：

```
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="run-an-app"></a>執行應用程式

如果應用程式處於 「 就緒 」 狀態，您可以使用它，藉由執行與您指定的輸入參數。 若要執行的應用程式中使用下列語法：

```bash
mssqlctl-pre app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

下列範例命令示範如何執行的命令：

```bash
mssqlctl-pre app run --name add-app --version v1 --inputs x=1,y=2
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

## <a name="delete-an-app"></a>刪除應用程式

若要從您的巨量資料叢集刪除應用程式，請使用下列語法：

```bash
mssqlctl-pre app delete --name add-app --version v1
```

## <a name="next-steps"></a>後續步驟

您也可以查看其他樣本[ https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster)。 

如需有關 SQL Server 的巨量資料叢集的詳細資訊，請參閱 <<c0> [ 什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)。
