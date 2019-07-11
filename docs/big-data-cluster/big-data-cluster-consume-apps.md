---
title: 使用巨量資料叢集上的應用程式
titleSuffix: SQL Server big data clusters
description: 使用 SQL Server 2019 巨量資料叢集使用 RESTful web 服務 （預覽） 上部署應用程式。
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
manager: jroth
ms.date: 03/18/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 308bbe40ba49566bf6cbccad13f8edab0db3d363
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67729292"
---
# <a name="consume-an-app-deployed-on-sql-server-big-data-cluster-using-a-restful-web-service"></a>使用 SQL Server 使用 RESTful web 服務的巨量資料叢集上部署的應用程式

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何使用 SQL Server 2019 巨量資料叢集使用 RESTful web 服務 （預覽） 上部署的應用程式。

## <a name="prerequisites"></a>必要條件

- [SQL Server 2019 巨量資料叢集](deployment-guidance.md)
- [mssqlctl 命令列公用程式](deploy-install-mssqlctl.md)
- 部署使用的應用程式[ `mssqlctl` ](big-data-cluster-create-apps.md)或[應用程式部署的延伸模組](app-deployment-extension.md)

## <a name="capabilities"></a>Capabilities

您已部署至您的 SQL Server 2019 巨量資料叢集 （預覽） 的應用程式之後，您可以存取，並使用該應用程式使用 RESTful web 服務。 這可讓該應用程式，從其他應用程式或服務 （例如，行動裝置應用程式或網站） 的整合。 下表描述您可以搭配使用的應用程式部署命令**mssqlctl**來取得您的應用程式的 RESTful web 服務的相關資訊。

|命令 |描述 |
|:---|:---|
|`mssqlctl app describe` | 說明應用程式。 |

您可以取得說明`--help`參數，如下列範例所示：

```bash
mssqlctl app describe --help
```

下列各節說明如何擷取應用程式的端點，以及如何使用 RESTful web 服務應用程式整合。

## <a name="retrieve-the-endpoint"></a>擷取端點

**Mssqlctl 應用程式描述**命令提供應用程式，包括您的叢集中的結束點的詳細的資訊。 這通常是由應用程式開發人員建置應用程式使用 swagger 的用戶端，並使用 web 服務的應用程式互動以 RESTful 方式。

描述您的應用程式執行的命令如下所示：

```bash
mssqlctl app describe --name addpy --version v1
```

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
    "app": "https://10.1.1.3:30777/api/app/addpy/v1",
    "swagger": "https://10.1.1.3:30777/api/app/addpy/v1/swagger.json"
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

請記下 IP 位址 (`10.1.1.3`在此範例中) 和連接埠號碼 (`30777`) 在輸出中。

## <a name="generate-a-jwt-access-token"></a>產生的 JWT 存取權杖

若要存取已部署應用程式的 RESTful web 服務，您有產生的 JWT 存取權杖。 在您的瀏覽器中開啟下列 URL:`https://[IP]:[PORT]/api/docs/swagger.json`使用的 IP 位址和連接埠執行擷取`describe`上述命令。 您必須登入您所使用的相同認證`mssqlctl login`。

貼上的內容`swagger.json`成[Swagger 編輯器](https://editor.swagger.io)來了解哪些方法會提供：

![API Swagger](media/big-data-cluster-consume-apps/api_swagger.png)

請注意`app`GET 方法，以及`token`POST 方法。 因為應用程式的驗證會使用 JWT 權杖，所以您必須取得權杖，我使用您最愛的工具將 POST 呼叫`token`方法。 以下是如何執行這項作業的範例[Postman](https://www.getpostman.com/):

![Postman 的語彙基元](media/big-data-cluster-consume-apps/postman_token.png)

此要求的結果會提供您 JWT `access_token`，您將需要以呼叫執行應用程式的 URL。

## <a name="execute-the-app-using-the-restful-web-service"></a>執行使用 RESTful web 服務的應用程式

> [!NOTE]
> 如果您想，您可以開啟的 URL`swagger`當您執行時所傳回`mssqlctl app describe --name [appname] --version [version]`在瀏覽器中，其應該類似於`https://[IP]:[PORT]/api/app/[appname]/[version]/swagger.json`。 您必須登入您所使用的相同認證`mssqlctl login`。 內容`swagger.json`您可以將它貼入[Swagger 編輯器](https://editor.swagger.io)。 您會看到 web 服務會公開`run`方法。 也請注意顯示在頂端的基底 URL。

您可以使用您最愛的工具來呼叫`run`方法 (`https://[IP]:30778/api/app/[appname]/[version]/run`)，並傳入您為 json 的 POST 要求主體中的參數。 在此範例中我們將使用[Postman](https://www.getpostman.com/)。 再進行呼叫，您必須設定`Authorization`至`Bearer Token`並貼上您先前擷取的權杖。 這會將設定您的要求標頭。 請參閱以下螢幕擷取畫面。

![Postman 執行標頭](media/big-data-cluster-consume-apps/postman_run_1.png)

接下來，在要求主體中，將參數傳入的應用程式，您將會呼叫，並設定`content-type`至`application/json`:

![Postman 執行主體](media/big-data-cluster-consume-apps/postman_run_2.png)

當您傳送要求時，您會取得相同的輸出時您執行應用程式`mssqlctl app run`:

![Postman 執行結果](media/big-data-cluster-consume-apps/postman_result.png)

已成功現在呼叫透過 web 服務應用程式。 您可以依照類似的步驟，將此應用程式中的 web 服務。

## <a name="next-steps"></a>後續步驟

您也可以查看其他樣本[應用程式部署範例](https://aka.ms/sql-app-deploy)。

如需有關 SQL Server 的巨量資料叢集的詳細資訊，請參閱 <<c0> [ 什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)。
