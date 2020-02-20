---
title: 取用應用程式
titleSuffix: SQL Server Big Data Clusters
description: 使用 RESTful Web 服務取用部署在 SQL Server 巨量資料叢集上的應用程式。
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 01/07/2020
ms.metadata: seo-lt-2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 305080d5c3b0a1c517d757c1f6f2bd07fefb216c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75721403"
---
# <a name="consume-an-app-deployed-on-big-data-clusters-2019-using-a-restful-web-service"></a>使用 RESTful Web 服務取用部署在 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]上的應用程式

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何使用 RESTful Web 服務取用部署在 SQL Server 巨量資料叢集上的應用程式。

## <a name="prerequisites"></a>Prerequisites

- [SQL Server 巨量資料叢集](deployment-guidance.md)
- [azdata 命令列公用程式](deploy-install-azdata.md)
- 使用 [azdata](big-data-cluster-create-apps.md) 或[應用程式部署擴充功能](app-deployment-extension.md)部署的應用程式

## <a name="capabilities"></a>功能

將應用程式部署到您的 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]之後，您就可以使用 RESTful Web 服務來存取和取用該應用程式。 這樣能夠從其他應用程式或服務 (例如，行動應用程式或網站) 整合該應用程式。 下表描述您可以搭配 **azdata** 使用的應用程式部署命令，以取得應用程式的 RESTful Web 服務相關資訊。

|Command |描述 |
|:---|:---|
|`azdata app describe` | 描述應用程式。 |

您可以使用 `--help` 參數取得協助，如下列範例所示：

```bash
azdata app describe --help
```

下列小節說明如何擷取應用程式端點，以及如何使用 RESTful Web 服務進行應用程式整合。

## <a name="retrieve-the-endpoint"></a>擷取端點

**azdata app describe** 命令提供有關應用程式的詳細資訊，包括您叢集中的端點。 應用程式開發人員通常會使用此方法來建立使用 Swagger 用戶端的應用程式，並使用 Webservice 以 RESTful 方式與應用程式互動。

執行類似下列範例的命令來描述您的應用程式：

```bash
azdata app describe --name add-app --version v1
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
    "app": "https://10.1.1.3:30080/app/addpy/v1",
    "swagger": "https://10.1.1.3:30080/app/addpy/v1/swagger.json"
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

請記下輸出中的 IP 位址 (在此範例中為 `10.1.1.3`) 和連接埠號碼 (`30080`)。

取得此資訊的另一種方法是在 Azure Data Studio 中，於伺服器的 [管理] 上按一下滑鼠右鍵，您將在其中找到所列服務的端點。

![ADS 端點](media/big-data-cluster-consume-apps/ads_end_point.png)

## <a name="generate-a-jwt-access-token"></a>產生 JWT 存取權杖

為了存取您已部署之應用程式的 RESTful Web 服務，您必須先產生 JWT 存取權杖。 存取權杖的 URL 相依於巨量資料叢集的版本。 

|版本 |URL|
|------------|------|
|GDR1|  `https://[IP]:[PORT]/docs/swagger.json`|
|CU1 與更新版本| `https://[IP]:[PORT]/api/v1/swagger.json`|

> 如需版本資訊，請參閱[發行記錄](release-notes-big-data-cluster.md#release-history)。

使用您以上述 [`describe`](#retrieve-the-endpoint) 命令擷取的 IP 位址與連接埠，在瀏覽器中開啟適當的 URL。 使用您用於 `azdata login` 的相同認證來登入。

將 `swagger.json` 的內容貼入 [Swagger 編輯器](https://editor.swagger.io) \(英文\)，以了解可以使用哪些方法：

![API Swagger](media/big-data-cluster-consume-apps/api_swagger.png)

請注意 `app` GET 方法，以及 `token` POST 方法。 由於應用程式的驗證是使用 JWT 權杖，因此您將必須使用您最愛的工具對 `token` 方法進行 POST 呼叫來取得權杖。 以下是如何在 [Postman ](https://www.getpostman.com/) \(英文\) 中執行此操作的範例：

![Postman 權杖](media/big-data-cluster-consume-apps/postman_token.png)

此要求的結果會提供您 JWT `access_token`，您呼叫 URL 來執行應用程式時將會需要它。

## <a name="execute-the-app-using-the-restful-web-service"></a>使用 RESTful Web 服務執行應用程式

> [!NOTE]
> 如有需要，您可以在瀏覽器中開啟執行 `azdata app describe --name [appname] --version [version]` 時所傳回的 `swagger` URL，它應該類似於 `https://[IP]:[PORT]/app/[appname]/[version]/swagger.json`。 您必須使用您用於 `azdata login` 的相同認證來登入。 您可以貼入 [Swagger 編輯器](https://editor.swagger.io)的 `swagger.json` 內容。 您將會看到 Web 服務公開 `run` 方法。 另請注意顯示在頂端的基底 URL。

您可以使用您最愛的工具來呼叫 `run` 方法 (`https://[IP]:30778/api/app/[appname]/[version]/run`)，並在 POST 要求主體中，以 json 格式傳入參數。 在此範例中，我們將會使用 [Postman](https://www.getpostman.com/) \(英文\)。 進行呼叫之前，您必須先將 `Authorization` 設定為 `Bearer Token`，並貼入您先前擷取的權杖。 這會在您的要求上設定標頭。 請參閱下面的螢幕擷取畫面。

![Postman 執行標題](media/big-data-cluster-consume-apps/postman_run_1.png)

接下來，在要求本文中，將參數傳入您要呼叫的應用程式，並將 `content-type` 設定為 `application/json`：

![Postman 執行本文](media/big-data-cluster-consume-apps/postman_run_2.png)

當您傳送要求時，您得到的輸出會與透過 `azdata app run` 執行應用程式的相同：

![Postman 執行結果](media/big-data-cluster-consume-apps/postman_result.png)

您現在已成功透過 Web 服務呼叫應用程式。 您可以遵循類似的步驟，在您的應用程式中整合此 Web 服務。

## <a name="next-steps"></a>後續步驟

您也可以在[應用程式部署範例](https://aka.ms/sql-app-deploy)中查看其他範例。

如需 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。
