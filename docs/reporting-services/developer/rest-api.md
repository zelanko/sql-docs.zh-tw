---
title: 使用 Reporting Services 的 REST API 進行開發 | Microsoft Docs
ms.description: The REST API provides programmatic access to the objects in a SQL Server 2017 Reporting Services report server catalog.
ms.date: 05/25/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: developer
ms.topic: conceptual
author: markingmyname
ms.author: maghan
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: d4872ffea819c23ca27ec0d01e4709a231f95cf5
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52514405"
---
# <a name="develop-with-the-rest-apis-for-reporting-services"></a>使用 Reporting Services 的 REST API 進行開發

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

Microsoft SQL Server 2017 Reporting Services 支援具象狀態傳輸 (REST) API。 REST API 是支援一組 HTTP 作業 (方法) 的服務端點，提供報表伺服器中資源的建立、擷取、更新或刪除權限。

REST API 可透過程式設計方式存取 SQL Server 2017 Reporting Services 報表伺服器目錄中的物件。 物件的範例包括資料夾、報表、KPI、資料來源、資料集、重新整理計劃、訂閱等等。 例如，您可以使用 REST API 巡覽資料夾階層、探索資料夾內容或下載報表定義。 您也可以建立、更新及刪除物件。 使用物件的範例包括上傳報表、執行重新整理計劃、刪除資料夾等等。

[!INCLUDE [GDPR-related guidance](../../includes/gdpr-hybrid-note.md)]

## <a name="components-of-a-rest-api-requestresponse"></a>REST API 要求/回應的元件

REST API 要求/回應配對可分成五個元件：

* 由 `{URI-scheme} :// {URI-host} / {resource-path} ? {query-string}` 所組成的**要求 URI**。 雖然要求 URI 包含在要求訊息標頭中，但由於大多數語言或架構要求您將它與要求訊息分開傳遞，因此我們會另外呼叫它。

    * URI 配置：表示用來傳輸要求的通訊協定。 例如，`http` 或 `https`。
    * URI 主機：指定裝載 REST 服務端點之伺服器的網域名稱或 IP 位址，例如 `myserver.contoso.com`。
    * 資源路徑：指定資源或資源集合，其中可能包含服務用來判斷這些資源選取的多個區段。 例如：`CatalogItems(01234567-89ab-cdef-0123-456789abcdef)/Properties` 可用來取得 CatalogItem 的指定屬性。
    * 查詢字串 (選用)：提供其他簡單參數，例如 API 版本或資源選取準則。

* HTTP 要求訊息標頭欄位：

    * 必要的 [HTTP 方法](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) (也稱為作業或動詞)，這會告知服務所要求的作業類型。 Reporting Services REST API 支援 DELETE、GET、HEAD、PUT、POST 和 PATCH 方法。
    * 指定的 URI 和 HTTP 方法所需的其他選擇性標頭欄位。

* 選擇性的 HTTP **要求訊息主體**欄位，以支援 URI 和 HTTP 作業。 例如，POST 作業包含當作複雜參數傳遞的 MIME 編碼物件。 針對 POST 或 PUT 作業，也必須在 `Content-type` 要求標頭中指定主體的 MIME 編碼類型。 某些服務要求您使用特定 MIME 類型，例如 `application/json`。

* HTTP **回應訊息標頭**欄位：

    * [HTTP 狀態碼](https://www.w3.org/Protocols/HTTP/HTRESP.html)，範圍可介於 2xx 成功碼到 4xx 或 5xx 錯誤碼之間。 或者，可能會傳回服務定義的狀態碼，如 API 文件中所示。
    * 支援要求回應所需的其他選擇性標頭欄位，例如 `Content-type` 回應標頭。

* 選擇性的 HTTP **回應訊息主體**欄位：

    * MIME 編碼回應物件會在 HTTP 回應主體中傳回，例如來自傳回資料之 GET 方法的回應。 一般而言，這些物件會以 JSON 或 XML 等結構化格式傳回，如 `Content-type` 回應標頭所示。

## <a name="api-documentation"></a>API 文件

新式 REST API 需要新式 API 文件。 REST API 是以 OpenAPI 規格 (也稱為 swagger 規格) 為建置基礎，相關文件可從 [SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0) 上取得。 除了記載 API 之外，SwaggerHub 還有助於以 JavaScript、TypeScript、C#、Java、Python、Ruby 等所選擇的語言來產生用戶端程式庫。

## <a name="testing-api-calls"></a>測試 API 呼叫

用於測試 HTTP 要求/回應訊息的工具之一是 [Fiddler](https://www.telerik.com/fiddler)。 Fiddler 是可攔截 REST 要求的免費 Web 偵錯 Proxy，讓您輕鬆就能診斷 HTTP 要求/回應訊息。

## <a name="next-steps"></a>後續步驟

在 [SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0) 上檢閱可用的 API。

這類的範例可從 [GitHub](https://github.com/Microsoft/Reporting-Services) 上取得。 此範例包含以 TypeScript、React 和 webpack 為建置基礎的 HTML5 應用程式，以及 PowerShell 範例。

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
