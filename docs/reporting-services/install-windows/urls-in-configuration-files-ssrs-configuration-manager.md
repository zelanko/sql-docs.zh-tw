---
title: 設定檔中的 URL (SSRS 設定管理員) | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- URL configuration [Reporting Services]
ms.assetid: 4f5e7fe0-b5b1-4665-93d4-80dce12d6b14
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 75da68330bcce06a4ffdaf152bb19811cffe1f99
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593930"
---
# <a name="urls-in-configuration-files--ssrs-configuration-manager"></a>組態檔中的 URL (SSRS 組態管理員)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會將應用程式設定儲存在 RSReportServer.config 檔案中。 在這個檔案中，URL 和 URL 保留項目都有組態設定。 這些組態設定的用途與修改規則大不相同。 如果您習慣修改組態檔來微調部署，本主題將可幫助您了解每一個 URL 設定的使用方式。  
  
## <a name="url-settings-in-rsreportserverconfig-file"></a>RSReportServer.config 檔案中的 URL 設定  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會儲存 URL 以供應用程式和報表存取，並可將 Web 前端元件連接到後端報表伺服器。  
  
#### <a name="urls-for-application-access"></a>供應用程式存取的 URL  
 URL 是用來存取報表伺服器 Web 服務和 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]。 若要設定 URL，您必須使用 Reporting Services 組態工具。 此工具會在 HTTP.SYS 中建立每一個應用程式的 URL 保留項目，並將 URL 的項目加入 RSReportServer.config 的 **URLReservations** 區段。  
  
-   若要檢視 **URLReservations** 區段中每個元素的描述，請參閱 [RsReportServer.config Configuration File](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) (RsReportServer.config 組態檔)。  
  
-   如果只需 **UrlString** 項目的語法詳細資訊，請參閱 [URL 保留項目語法 &#40;SSRS 設定管理員&#41;](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md)。  
  
-   如需有關如何設定 URL 以供應用程式存取的指示，請參閱 [設定 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)。  
  
#### <a name="urls-for-report-access"></a>供報表存取的 URL  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包含一個報表伺服器電子郵件傳遞延伸模組，可用來傳送報表連結或附加檔案。 當傳遞報表時，就會建構報表連結。 此報表伺服器電子郵件傳遞延伸模組會使用組態檔中的 **UrlRoot** 設定來建立此連結。 **UrlRoot** 也會用來解析透過自動報表處理產生之轉譯報表中的連結。  
  
 當您設定用於應用程式存取的 URL 時，**UrlRoot** 便會自動指定於 RSReportServer.config 檔案中。 如果您在組態檔中修改這個值，您必須指定報表伺服器 Web 服務的有效 URL 位址，該服務會連接到包含您要傳遞之報表的報表伺服器資料庫。 您只能為單一報表伺服器執行個體指定一個 **UrlRoot** ；任何給定之報表伺服器執行個體的 RSReportServer.config 檔案中只能有一個 **UrlRoot** 項目存在。 如果您為報表伺服器 Web 服務保留多個 URL，您必須為 **UrlRoot**選擇其中一個可用的值。  
  
 在大部分情況下，您不需要修改 **UrlRoot**。 但是，如果報表將會透過完整 URL 來存取報表伺服器，而您並未設定 URL 來使用完整網站名稱的主機標頭，就必須手動編輯 RSReportServer.config，以將 **UrlRoot** 設定為用來轉譯報表的完整報表伺服器 URL (例如 https://www.adventure-works.com/mywebapp/reportserver) 。  
  
#### <a name="urls-connecting-the-includessrswebportalincludesssrswebportalmd-and-web-parts-to-the-report-server-web-service"></a>將 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 和 Web 組件連接到報表伺服器 Web 服務的 URL  
 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 和 Reporting Services 的 SharePoint 2.0 Web 組件是用來連接報表伺服器的 Web 前端元件。 用來連接後端報表伺服器的 URL 包含以下項目：  
  
-   **ReportServerUrl** (由 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]使用)  
  
-   **ReportServerExternalUrl** (由 Web 組件使用)  
  
> [!NOTE]  
>  舊版 Reporting Services 包含 **ReportServerVirtualDirectory** 元素。 但是，在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本中，此值已經過時。 如果您已升級現有的安裝，而且正在使用包含此設定的組態檔，則報表伺服器就不會再讀取這個值。  
  
 下表提供可以在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態檔中指定之所有 URL 的摘要。  
  
|設定|使用方式|Description|  
|-------------|-----------|-----------------|  
|**ReportServerUrl**|選擇性。 除非您自行加入，否則這個元素不會包含在 RSReportServer.config 檔案中。<br /><br /> 只有當您要設定以下其中一個狀況時，才能設定這個元素：<br /><br /> [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 會提供報表伺服器 Web 服務的 Web 前端存取權，該服務可在不同電腦上執行或是在相同電腦的不同執行個體上執行。<br /><br /> 當您擁有報表伺服器的多個 URL，而且希望 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 使用特定的 URL 時。<br /><br /> 您擁有特定報表伺服器 URL，您希望所有 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 連接都使用此 URL。<br /><br /> 例如，您可能會啟用網路上所有電腦的 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 存取權，但是您需要 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 透過本機連接來連接報表伺服器。 在此情況下，您可能會將 **ReportServerUrl** 設定為 "`https://localhost/reportserver`"。|這個值會指定報表伺服器 Web 服務的 URL。 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 應用程式會在啟動時讀取這個值。 如果設定了這個值， [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 將會連接到此 URL 中指定的報表伺服器。<br /><br /> 依預設， [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 會提供報表伺服器 Web 服務的 Web 前端存取權，該服務會在相同報表伺服器執行個體內作為 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]來執行。 但是，如果您要將 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 搭配報表伺服器 Web 服務一起使用 (該服務屬於另一個執行個體的一部分，或是會在不同電腦的執行個體中執行)，您就可以設定此 URL 來引導 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 連接外部報表伺服器 Web 服務。<br /><br /> 如果您在要連接的報表伺服器上安裝了安全通訊端層 (SSL) 憑證， **ReportServerUrl** 值必須是為該憑證註冊的伺服器名稱。 如果您收到錯誤訊息「基礎連接已關閉: 無法為 SSL/TLS 安全通道建立信任關係」，請將 **ReportServerUrl** 設定為發出 SSL 憑證之伺服器的完整網域名稱。 例如，如果已將此憑證註冊到 **https:\//adventure-works.com.onlinesales**，報表伺服器 URL 即為 **https:\//adventure-works.com.onlinesales/reportserver**。|  
|**ReportServerExternalUrl**|選擇性。 除非您自行加入，否則這個元素不會包含在 RSReportServer.config 檔案中。<br /><br /> 只有當您要使用 SharePoint 2.0 Web 組件，而且希望使用者能夠擷取報表，並在新的瀏覽器視窗中開啟此報表時，才設定這個元素。<br /><br /> 在不同的瀏覽器視窗中存取時，將 \<**ReportServerExternalUrl**> 新增至 \<**ReportServerUrl**> 項目底下，然後將它設定為可解析為報表伺服器執行個體的完整報表伺服器名稱。 請勿刪除 \<**ReportServerUrl**>。<br /><br /> 下列範例說明語法：<br /><br /> `<ReportServerExternalUrl>https://myserver/reportserver</ReportServerExternalUrl>`|這個值是由 SharePoint 2.0 Web 組件使用。<br /><br /> 舊版中曾經建議您設定這個值，以便將「報表產生器」部署在供網際網路存取的報表伺服器上， 這是未經測試的部署狀況。 如果您過去使用這項設定來支援「報表產生器」的網際網路存取，現在應該考慮改用替代的策略。|  
  
## <a name="see-also"></a>另請參閱  
 [設定報表伺服器 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [設定 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)
