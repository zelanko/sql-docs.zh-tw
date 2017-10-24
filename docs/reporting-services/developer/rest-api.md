---
title: "使用 Reporting Services 的 REST Api 進行開發 |Microsoft 文件"
ms.description: The REST API provides programmatic access to the objects in a SQL Server 2017 Reporting Services report server catalog.
ms.date: 10/19/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 7c2c34047ac316045387b036cf10ee149175580a
ms.contentlocale: zh-tw
ms.lasthandoff: 10/20/2017

---
# <a name="develop-with-the-rest-apis-for-reporting-services"></a>Reporting services 使用 REST Api 進行開發

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

Microsoft SQL Server 2017 報告的服務支援 Representational State Transfer (REST) Api。 REST Api 會的支援一組 HTTP 作業 （方法），提供建立、 擷取、 更新或刪除報表伺服器中資源的存取權的服務端點。

REST API 提供以程式設計方式存取 SQL Server 2017 Reporting Services 報表伺服器目錄中的物件。 物件範例包括資料夾、 報表、 Kpi、 資料來源、 資料集、 重新整理計劃、 訂用帳戶，等等。 使用 REST API，您可以比方說，瀏覽資料夾階層、 探索資料夾的內容，或下載報表定義。 您也可以建立、 更新和刪除的物件。 使用物件的範例會將報表上傳、 執行重新整理計劃、 刪除資料夾，並以此類推。

## <a name="components-of-a-rest-api-requestresponse"></a>REST API 的要求/回應的元件

REST API 的要求/回應配對可以分成五個元件：

* **要求 URI**，其所組成： `{URI-scheme} :// {URI-host} / {resource-path} ? {query-string}`。 雖然在要求 URI 包含要求訊息標頭中，我們稱之為 「 個別這裡因為大部分的語言或架構需要您分別從要求訊息傳遞。

    * URI 配置： 指出用來傳送要求的通訊協定。 例如，`http`或`https`。
    * URI 主機： 指定的網域名稱或 IP 位址的 REST 服務端點裝載，例如伺服器`myserver.contoso.com`。
    * 資源路徑： 指定資源集合，其中可能包含多個區段中判斷這些資源的選取的服務所使用的資源。 例如：`CatalogItems(01234567-89ab-cdef-0123-456789abcdef)/Properties`可用來取得 CatalogItem 中指定的屬性。
    * 查詢字串 （選用）： 提供其他簡單參數的詳細資訊，例如應用程式開發介面版本或資源選擇準則。

* HTTP 要求訊息標頭欄位：

    * 必要[HTTP 方法](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)（也稱為作業或動詞命令），這會告知服務作業所要求的類型。 Reporting Services REST Api 支援刪除、 HEAD、 PUT、 POST、 GET 和修補程式的方法。
    * 選擇性的額外標頭欄位，如同所指定的 URI 和 HTTP 方法。

* 選擇性的 HTTP**要求訊息本文**欄位，以支援 URI 和 HTTP 作業。 例如，POST 作業包含 MIME 編碼的物件做為複雜參數傳遞。 應該在中指定主體的 MIME 編碼類型為 POST 或 PUT 作業，`Content-type`要求標頭。 有些服務需要您使用特定的 MIME 類型，例如`application/json`。

* HTTP**回應訊息標頭**欄位：

    * [HTTP 狀態碼](http://www.w3.org/Protocols/HTTP/HTRESP.html)，範圍可從 2xx 成功碼 4xx 或 5xx 錯誤代碼。 或者，定義服務的狀態碼可能會傳回，應用程式開發介面文件中所示。
    * 選擇性的額外標頭欄位，為必要項目支援要求的回應，例如`Content-type`回應標頭。

* 選擇性的 HTTP**回應訊息內文**欄位：

    * 在 HTTP 回應主體中，例如 GET 方法的傳回資料的回應會傳回 MIME 編碼的回應物件。 一般而言，這些物件會傳回 JSON 或 XML，例如結構化的格式所示`Content-type`回應標頭。

## <a name="api-documentation"></a>應用程式開發介面文件

現代的 REST API 呼叫的新型應用程式開發介面文件。 REST API 是根據 OpenAPI 規格 （也稱為 swagger 規格） 和文件位於[SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0)。 超出記錄 API，SwaggerHub 會有助於產生用戶端程式庫中選擇 – JavaScript、 TypeScript、 C#、 Java、 Python、 Ruby、 等等的語言。

## <a name="testing-api-calls"></a>測試應用程式開發介面呼叫

進行測試的 HTTP 要求/回應訊息的工具之一是[Fiddler](http://www.telerik.com/fiddler)。 Fiddler 是免費的 web 偵錯 proxy 可以攔截 REST 要求，以便輕鬆地診斷 HTTP 要求 / 回應訊息。

## <a name="next-steps"></a>後續的步驟

檢閱可用的應用程式開發介面上[SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0)。

範例位於[GitHub](https://github.com/Microsoft/Reporting-Services)。 此範例包含 TypeScript、 React 和 webpack 以及 PowerShell 範例上建置的 HTML5 應用程式。

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
