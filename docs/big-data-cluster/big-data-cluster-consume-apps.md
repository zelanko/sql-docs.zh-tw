---
title: 在大型資料叢集上使用應用程式
titleSuffix: SQL Server big data clusters
description: 使用 RESTful web 服務 (預覽), 取用部署在 SQL Server 2019 big data 叢集上的應用程式。
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a2135ef64fb17eba62eab75b81739eda047167ab
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419504"
---
# <a name="consume-an-app-deployed-on-sql-server-big-data-cluster-using-a-restful-web-service"></a>使用 RESTful web 服務, 取用部署在 SQL Server big data 叢集上的應用程式

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何使用 RESTful web 服務 (預覽), 來使用部署在 SQL Server 2019 big data 叢集上的應用程式。

## <a name="prerequisites"></a>必要條件

- [SQL Server 2019 big data cluster](deployment-guidance.md)
- [mssqlctl 命令列公用程式](deploy-install-azdata.md)
- 使用[azdata](big-data-cluster-create-apps.md)或[應用程式部署擴充](app-deployment-extension.md)功能部署的應用程式

## <a name="capabilities"></a>Capabilities

將應用程式部署到您的 SQL Server 2019 big data 叢集 (預覽) 之後, 您就可以使用 RESTful web 服務來存取和使用該應用程式。 這會啟用該應用程式與其他應用程式或服務 (例如行動應用程式或網站) 的整合。 下表描述您可以搭配**azdata**使用的應用程式部署命令, 以取得應用程式的 RESTful web 服務的相關資訊。

|命令 |描述 |
|:---|:---|
|`azdata app describe` | 描述應用程式。 |

如下列範例所示, `--help`您可以使用參數取得協助:

```bash
azdata app describe --help
```

下列各節說明如何取得應用程式的端點, 以及如何使用 RESTful web 服務進行應用程式整合。

## <a name="retrieve-the-endpoint"></a>取出端點

**Azdata 應用程式描述**命令會提供有關應用程式的詳細資訊, 包括叢集中的結束點。 應用程式開發人員通常會使用此方法來建立使用 swagger 用戶端的應用程式, 並使用 webservice 以 RESTful 的方式與應用程式互動。

執行類似下列的命令來描述您的應用程式:

```bash
azdata app describe --name addpy --version v1
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

請記下輸出中`10.1.1.3`的 IP 位址 (在此範例中為`30777`) 和埠號碼 ()。

## <a name="generate-a-jwt-access-token"></a>產生 JWT 存取權杖

為了存取您已部署之應用程式的 RESTful web 服務, 您必須先產生 JWT 存取權杖。 在您的瀏覽器中開啟下列`https://[IP]:[PORT]/api/docs/swagger.json` URL: 使用您所`describe`抓取的 IP 位址和埠, 以執行上述命令。 您必須使用您用於`azdata login`的相同認證來登入。

將的內容`swagger.json`貼入[Swagger 編輯器](https://editor.swagger.io), 以瞭解有哪些方法可供使用:

![API Swagger](media/big-data-cluster-consume-apps/api_swagger.png)

請注意`token` GET 方法以及 POST 方法。 `app` 由於應用程式的驗證會使用 JWT 權杖, 因此您必須使用您最愛的工具來取得權杖, 以對`token`方法進行 POST 呼叫。 以下是如何在[Postman](https://www.getpostman.com/)中執行這項操作的範例:

![Postman Token](media/big-data-cluster-consume-apps/postman_token.png)

此要求的結果會提供您 JWT `access_token`, 您必須呼叫 URL 來執行應用程式。

## <a name="execute-the-app-using-the-restful-web-service"></a>使用 RESTful web 服務執行應用程式

> [!NOTE]
> 如有需要, 您可以開啟`swagger` `azdata app describe --name [appname] --version [version]`在瀏覽器中執行時所傳回之的 URL, 這應該類似于`https://[IP]:[PORT]/api/app/[appname]/[version]/swagger.json`。 您必須使用您用於`azdata login`的相同認證來登入。 `swagger.json`您可以貼到[Swagger 編輯器](https://editor.swagger.io)中的內容。 您會看到 web 服務公開`run`方法。 另請注意顯示在頂端的基底 URL。

您可以使用您最愛的`run`工具來呼叫方法 (`https://[IP]:30778/api/app/[appname]/[version]/run`), 以 json 形式傳入 POST 要求主體中的參數。 在此範例中, 我們將使用[Postman](https://www.getpostman.com/)。 進行呼叫之前, 您必須先將設定`Authorization`為`Bearer Token` , 並貼上您先前抓取的權杖。 這會在您的要求上設定標頭。 請參閱下列螢幕擷取畫面。

![Postman 執行標頭](media/big-data-cluster-consume-apps/postman_run_1.png)

接下來, 在要求本文中, 將參數傳入您要呼叫的應用程式, 並將`content-type`設定`application/json`為:

![Postman 執行主體](media/big-data-cluster-consume-apps/postman_run_2.png)

當您傳送要求時, 會得到與您執行應用程式`azdata app run`時所使用的相同輸出:

![Postman 執行結果](media/big-data-cluster-consume-apps/postman_result.png)

您現在已成功透過 web 服務呼叫應用程式。 您可以遵循類似的步驟, 在您的應用程式中整合此 web 服務。

## <a name="next-steps"></a>後續步驟

您也可以參閱[應用程式部署範例](https://aka.ms/sql-app-deploy)中的其他範例。

如需有關 SQL Server big data 叢集的詳細資訊, 請參閱[什麼是 SQL Server 2019 big data 叢集？](big-data-cluster-overview.md)。
