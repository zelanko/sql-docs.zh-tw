---
title: 在 Web 應用程式中使用 URL 存取
description: Reporting Services 中的 URL 存取可供透過網路來存取報表，且將報表的檢視和瀏覽整合到自訂 Web 應用程式中。
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.custom: seo-lt-2019
ms.topic: reference
helpviewer_keywords:
- links [Reporting Services], URL access
- URL access [Reporting Services], Web applications
- POST requests
- direct addressing [Reporting Services]
- Web applications [Reporting Services]
- hyperlinks [Reporting Services]
ms.assetid: 39e7918c-ad2d-4ca6-b099-2dd4dbdb83dc
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 731ed382c029fb2115c4351d306bf5b33d294a48
ms.sourcegitcommit: d1f6da6f0f5e9630261cf733c64958938a3eb859
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/12/2020
ms.locfileid: "79198515"
---
# <a name="integrating-reporting-services-using-url-access---web-application"></a>使用 URL 存取整合 Reporting Services - Web 應用程式
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的 URL 存取是特別針對可透過網路存取個別報表所設計。 這種類型的存取最適於將報表檢視與導覽整合到自訂 Web 應用程式。 若要在 Web 應用程式中使用 URL 存取，您可以：  
  
-   從網站或是入口網站將 URL 定址到特定的報表伺服器。  
  
-   使用表單 POST 方法，並使用表單欄位將查詢字串參數傳遞到報表伺服器 URL。  
  
## <a name="url-access-through-direct-addressing"></a>透過直接定址的 URL 存取  
 若要使用 URL 來存取報表伺服器或是報表伺服器資料庫項目，請直接在網頁瀏覽器或應用程式中提供 URL 位址。 您也可以提供參數給 URL，這將可影響正在存取的報表或資源的外觀。 URL 可以透過網頁瀏覽器的位址列來鎖定報表伺服器，或者 URL 可以是較大的 Web 應用程式或是入口網站一部分之 **IFrame** 的來源。 您可以將超連結包括到入口網站之各個網頁上的報表中，以及鎖定報表的特定框架，或是在處理序中開啟一個新的瀏覽器視窗。  
  
 在下列範例中，超連結會鎖定名為 "main" 的框架，這可能與包含超連結的框架不同。 超連結可能是 Web 入口網站的一部分。  
  
```  
<a href="https://server/reportserver?/SampleReports/Territory Sales   
Drilldown&rs:Command=Render&rc:LinkTarget=main" target="main" >  
   Click here for the Territory Sales Drilldown sample report  
</a>  
```  
  
 在上述範例中，會使用 URL 的查詢字串中 "main" 的值來傳遞 **LinkTarget** 裝置資訊設定。 這可確保在報表中的任何鑽研超連結也鎖定名為 "main" 的框架。  
  
 如需裝置資訊設定的詳細資訊，請參閱[將裝置資訊設定傳遞至轉譯延伸模組](../../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)。  
  
 請注意，許多伺服器與瀏覽器會限制在 URL 中允許的字元數目。 在某些情況下，會加諸 256 個字元的限制。 若要解決此限制，您可以使用表單提交來使用 POST 要求。  
  
> [!NOTE]  
>  Internet Explorer 最大的 URL 長度為 2,083 個字元。 這個限制適用於 POST 與 GET 要求 URL。 不過，在提交名稱/值組做為表單一部分時，POST 並未受到 URL 大小的限制，因為會在標頭中而不是 URL 中傳輸它們。  
  
## <a name="url-access-through-a-form-post-method"></a>透過表單 POST 方法的 URL 存取  
 當使用者使用 URL 存取從報表伺服器要求資料時，HTTP 要求會使用 GET 方法。 這等於 METHOD="GET" 的表單提交。 使用 METHOD="GET" 的 URL 要求或是表單提交受限於伺服器或網頁瀏覽器可以處理的最大字元數目。  
  
 透過 POST 要求 (METHOD="POST" 與輸入欄位)，會在標頭中而不是 URL 中傳輸名稱/值組。 因此，查詢字串的名稱/值組不是 URL 的一部分，因此可讓您提供更長且更複雜的參數清單。  
  
 透過直接存取，使用者可以查看報表伺服器的 URL，而且可以修改查詢字串或是注意特定的 URL 要求與報表伺服器參數以供稍後使用。  
  
 下列範例 HTML 示範表單的使用，您可以透過特定的 URL 來使用目標報表伺服器，並將查詢字串參數以表單的輸入欄位之一部分來傳遞。  
  
```  
<FORM id="frmRender" action="https://server/reportserver?/SampleReports/  
   Territory Sales Drilldown" method="post" target="_self">  
   <INPUT type="hidden" name="rs:Command" value="Render">   
   <INPUT type="hidden" name="rc:LinkTarget" value="main">  
   <INPUT type="hidden" name="rs:Format" value="HTML4.0">  
   <INPUT type="submit" value="Button">  
</FORM>  
```  
  
 在上述範例中，如果使用者按一下表單上的按鈕，報表伺服器會傳回在目前框架鎖定的 HTML 轉譯報表。 可比較的 URL 存取字串可能如下所示：  
  
```  
https://server/reportserver?/SampleReports/Territory Sales   
Drilldown&rs:Command=Render&rc:LinkTarget=main&rs:Format=HTML4.0  
```  
  
## <a name="see-also"></a>另請參閱  
 [將 Reporting Services 整合到應用程式](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [使用 URL 存取整合 Reporting Services](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)   
 [在 Windows 應用程式中使用 URL 存取](../../reporting-services/application-integration/integrating-reporting-services-using-url-access-windows-application.md)   
 [URL 存取 &#40;SSRS&#41;](../../reporting-services/url-access-ssrs.md)  
  
  
