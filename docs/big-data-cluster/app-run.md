---
title: 使用 azdata 執行應用程式
titleSuffix: SQL Server Big Data Clusters
description: 在 SQL Server 2019 巨量資料叢集上使用 azdata 執行應用程式。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 08/16/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e8c603040c0b5df9440e3aaabadac0d947315310
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2020
ms.locfileid: "88681037"
---
# <a name="run-apps-with-azdata---sql-server-big-data-clusters"></a>使用 azdata 執行應用程式 - SQL Server 巨量資料叢集

此文章描述如何執行 SQL Server 巨量資料叢集內的應用程式。

## <a name="prerequisites"></a>Prerequisites

- [SQL Server 2019 巨量資料叢集](deployment-guidance.md)
- [azdata 命令列公用程式](deploy-install-azdata.md)

## <a name="capabilities"></a>功能

在 SQL Server 2019 中，您可以建立、刪除、描述、初始化、列出執行及更新您的應用程式。 下表描述您可以搭配 **azdata** 使用的應用程式部署命令。

|Command |說明 |
|:---|:---|
|`azdata app describe` | 描述應用程式。 |
|`azdata app run` | 執行應用程式。 |


下列各節會詳細描述這些命令。


## <a name="run-an-app"></a>執行應用程式

如果應用程式處於 `Ready` 狀態，您可以使用指定的輸入參數來執行。 使用下列語法來執行應用程式：

```bash
azdata app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

下列範例命令示範執行命令：

```bash
azdata app run --name add-app --version v1 --inputs x=1,y=2
```

如果執行成功，您應該會看到您在建立應用程式時所指定的輸出。 以下輸出是範例。

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


## <a name="describe-an-app"></a>描述應用程式

describe 命令提供有關應用程式的詳細資訊，包括您叢集中的端點。 應用程式開發人員通常會使用此方法來建立使用 Swagger 用戶端的應用程式，並使用 Webservice 以 RESTful 方式與應用程式互動。 如需詳細資訊，請參閱[取用巨量資料叢集上的應用程式](app-consume.md)。

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
    "app": "https://10.1.1.3:30080/api/app/add-app/v1",
    "swagger": "https://10.1.1.3:30080/api/app/add-app/v1/swagger.json"
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

若要探索如何在自己的應用程式中整合部署在 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]上的應用程式，請參閱[取用巨量資料叢集上的應用程式](app-consume.md)以取得詳細資訊。 您也可以在[應用程式部署範例](https://aka.ms/sql-app-deploy)中查看其他範例。

如需 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。
