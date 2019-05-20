---
title: URL 存取 (SSRS) | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- URL access [Reporting Services]
- links [Reporting Services], URL access
- URL access [Reporting Services], about URL access
- parameters [Reporting Services], URL access
- report servers [Reporting Services], URL access
- hyperlinks [Reporting Services]
ms.assetid: 52c3f2a3-3d6d-4fee-9c46-83f366919398
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a18ad4fd1d79bc7eae5f45318cece55037c78010
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2019
ms.locfileid: "65574242"
---
# <a name="url-access-ssrs"></a>URL 存取 (SSRS)
  在 SQL Server Reporting Services (SSRS) 中，報表伺服器的 URL 存取權可讓您透過 URL 要求，傳送命令至報表伺服器。 例如，您可在原生模式報表伺服器或 SharePoint 文件庫中自訂報表的轉譯。 您可能已使用特定一組報表參數值來檢視過報表，或報表中您感興趣的特定頁面。 您可以使用預先定義的 URL 存取參數，封裝 URL 中的資訊。 您還可以內嵌轉譯格式或調整報表檢視器外觀的參數，以進一步自訂報表伺服器處理報表的方式。 然後，您可以直接將此 URL 貼入電子郵件或網頁，讓其他人在瀏覽器中用相同方式存取您的報表。  
  
 您還可利用 URL 存取執行下列其他動作：  
  
-   傳送命令至 HTML 檢視器，例如調整其外觀  
  
-   列出目錄資料夾的子系  
  
-   擷取目錄項目的 XML 定義  
  
-   轉譯特定的報表記錄快照集  
  
-   管理報表工作階段  
  
 如需透過 URL 存取可用之命令與設定的完整清單，請參閱 [URL 存取參數參考](../reporting-services/url-access-parameter-reference.md)。  
  
## <a name="url-access-concepts"></a>URL 存取概念  
 報表伺服器的 URL 要求包含由報表伺服器處理的參數。 報表伺服器處理 URL 要求的方法須視 URL 中包含的參數、參數前置詞以及項目類型而定。 報表伺服器 URL 會遵循聯合全球資訊網協會 W3C/IETF 草案標準所提議的 URL 格式指導方針。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] URL 功能與大部分的網際網路瀏覽器或是支援標準 URL 定址的應用程式相容。  
  
### <a name="url-access-syntax"></a>URL 存取語法  
 URL 要求可包含以任何順序所列的多個參數。 參數是用連字號 (&) 分隔，而名稱/值組則是由等號 (=) 所分隔。  
  
```  
  
rswebserviceurl  
?  
reportpath  
      [&prefix:param=value]...n]  
  
```  
  
### <a name="syntax-description"></a>語法描述  
 *rswebserviceurl*  
 報表伺服器 Web 服務 URL。 針對原生模式，其為 Reporting Services 設定管理員中設定之報表伺服器執行個體的 Web 服務 URL (請參閱[設定報表伺服器 URL &#40;SSRS 設定管理員&#41;](../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md))。 例如：  
  
```  
https://myrshost/reportserver  
https://machine.adventure-works.com/reportserver_MYNAMEDINSTANCE  
```  
  
 針對 SharePoint 整合模式，其為整合 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 之 SharePoint 網站的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]Proxy URL。 例如：  
  
```  
https://myspsite/subsite/_vti_bin/reportserver  
```  
  
> [!TIP]  
>  請務必讓 URL 包含 `_vti_bin` Proxy 語法，以便透過 SharePoint 和 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] HTTP Proxy 路由傳送要求。 此 Proxy 會將某些內容加入至 HTTP 要求，也就是確保針對 SharePoint 模式報表伺服器正確執行報表所需的內容。  
  
 *pathinfo*  
 原生模式報表伺服器資料庫中項目的相對路徑名稱，或 SharePoint 目錄中項目的完整 URL。  
  
 目錄項目的路徑。 針對原生模式，其為報表伺服器資料庫中項目的相對路徑，以斜線 (**/**) 開頭。 例如：  
  
```  
/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2  
```  
  
 若為 SharePoint 整合模式，其為 SharePoint 文件庫中項目的完整 URL，包括項目延伸模組。 例如：  
  
```  
https://myspsite/subsite/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2.rdl  
```  
  
 **&**  
 用以分隔 URL 存取參數的名稱與值組。  
  
 **prefix**  
 選擇性。 URL 存取參數前置詞 (例如 `rs:` 或 `rc:`)，用以存取在報表伺服器中執行的特定處理序。  
  
> [!NOTE]  
>  如果未包括 URL 存取參數的前置詞，報表伺服器會以報表參數來處理參數。 報表參數不使用參數前置詞，且有區分大小寫。  
  
 **參數**  
 參數名稱。  
  
 *value*  
 對應至要使用的參數值之 URL 文字。  
  
 **注意** ：如需可用的 URL 存取參數清單，請參閱 [URL 存取參數參考](../reporting-services/url-access-parameter-reference.md)。 如需透過 URL 傳遞報表參數的範例，請參閱 [在 URL 內傳遞報表參數](../reporting-services/pass-a-report-parameter-within-a-url.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|連結|  
|-----------------------|-----------|  
|存取報表伺服器項目，如報表、共用資料來源和資源。|[使用 URL 存取權存取報表伺服器項目](../reporting-services/access-report-server-items-using-url-access.md)|  
|將報表參數傳遞至報表。|[在 URL 內傳遞報表參數](../reporting-services/pass-a-report-parameter-within-a-url.md)|  
|在 URL 存取字串中設定報表參數的地區設定，以定義特定地區的日期、貨幣等轉換。|[設定 URL 中報表參數的語言](../reporting-services/set-the-language-for-report-parameters-in-a-url.md)|  
|傳送可自訂報表轉譯方式的轉譯延伸模組特定設定。|[在 URL 中指定裝置資訊設定](../reporting-services/specify-device-information-settings-in-a-url.md)|  
|不在瀏覽器中檢視，而直接將報表匯出至檔案格式。|[使用 URL 存取匯出報表](../reporting-services/export-a-report-using-url-access.md)|  
|開啟報表，並直接導覽至字串位置。|[使用 URL 存取搜尋報表](../reporting-services/search-a-report-using-url-access.md)|  
|轉譯特定的報表記錄快照集。|[使用 URL 存取轉譯報表記錄快照集](../reporting-services/render-a-report-history-snapshot-using-url-access.md)|  
  
## <a name="see-also"></a>另請參閱  
 [在 URL 內傳遞報表參數](../reporting-services/pass-a-report-parameter-within-a-url.md)   
 [URL 存取參數參考](../reporting-services/url-access-parameter-reference.md)   
 [使用 URL 存取整合 Reporting Services](../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)   
 [尋找、檢視和管理報表 &#40;報表產生器及 SSRS &#41;](../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
