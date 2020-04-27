---
title: 關於 URL 保留項目和註冊 (SSRS 設定管理員) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- URL reservations
- URL registration
- Report Server service, URL reservations
ms.assetid: c2c460c3-e749-4efd-aa02-0f8a98ddbc76
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6b72d0a263010cc82abab38ea2d6149d3492ed7b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108936"
---
# <a name="about-url-reservations-and-registration--ssrs-configuration-manager"></a>關於 URL 保留項目和註冊 (SSRS 組態管理員)
  Reporting Services 應用程式的 URL 會當做 URL 保留項目定義在 HTTP.SYS 中。 URL 保留項目會定義 Web 應用程式之 URL 端點的語法。 當您在報表伺服器上設定應用程式時，會同時針對報表伺服器 Web 服務和報表管理員定義 URL 保留項目。 當您透過安裝程式或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具設定 URL 時，將會自動為您建立 URL 保留項目：  
  
-   安裝程式將會使用預設值建立 URL 保留項目。 如果安裝程式安裝預設組態，它將會保留兩個 URL；其中一個用於報表伺服器 Web 服務，另一個用於報表管理員。 您可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具來加入更多的 URL，或是修改安裝程式所建立的預設 URL。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具將會根據您在此工具的 **[Web 服務 URL]** 或 **[報表管理員 URL]** 頁面所指定的 URL 來建立 URL 保留項目。  
  
 安裝程式和此工具也都將指派報表伺服器服務之 URL 的權限、檢查是否有重複的執行個體，然後將此 URL 保留項目加入到 HTTP.SYS。 絕對不要直接使用 HttpCfg.exe 或其他工具來建立或修改 Reporting Services URL 保留項目。 如果您略過某個步驟或是設定無效的值，您將會遇到可能很難診斷或修復的問題。  
  
> [!NOTE]  
>  HTTP.SYS 是一個作業系統元件，它可接聽網路要求，並將這些要求路由傳送到要求佇列。 在這一版的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，HTTP.SYS 會建立及維護報表伺服器 Web 服務和報表管理員的要求佇列。 將不再使用 Internet Information Services (IIS) 來主控或存取 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 應用程式。 如需有關 HTTP.SYS 功能的詳細資訊，請參閱 MSDN 上的＜ [HTTP 伺服器 API](https://go.microsoft.com/fwlink/?LinkId=92652) ＞。  
  
##  <a name="urls-in-reporting-services"></a><a name="ReportingServicesURLs"></a>Reporting Services 中的 Url  
 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝中，您可以透過 URL 存取下列工具、應用程式和項目：  
  
-   報表伺服器 Web 服務  
  
-   報表管理員  
  
-   報表產生器  
  
-   已經發行至報表伺服器的報表  
  
 其他已發行之可由 URL 定址的項目 (例如模型和共用資料來源) 不應該透過當做獨立項目的 URL 來存取。 在瀏覽器視窗中檢視這些項目時，報表伺服器不會使用有意義的格式來顯示這些項目。  
  
> [!NOTE]  
>  本主題並未說明可存取報表產生器或報表伺服器上儲存之特定報表的 URL。 如需這些項目之 URL 存取的詳細資訊，請參閱《 [線上叢書》中的](../access-report-server-items-using-url-access.md) 使用 URL 存取權存取報表伺服器項目 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
##  <a name="url-reservation-and-registration"></a><a name="URLreservation"></a>URL 保留專案和註冊  
 URL 保留項目會定義可用於存取 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 應用程式的 URL。  將會保留一個或多個 URL 以供 HTTP.SYS 中的報表伺服器 Web 服務和報表管理員使用，然後在此服務啟動時加以註冊。 報表產生器和報表的 URL 是根據報表伺服器 Web 服務的 URL 保留項目。 您可以將參數附加到 URL，透過此 Web 服務開啟報表產生器或報表。 保留項目和註冊是由 HTTP.SYS 所提供。 如需詳細資訊，請參閱 MSDN 上的＜ [命名空間保留、註冊和路由](https://go.microsoft.com/fwlink/?LinkId=92653) ＞。  
  
 *「URL 保留」* 是建立 Web 應用程式的 URL 端點，並將其儲存在 HTTP.SYS 中的一項程序。 HTTP.SYS 是所有定義於電腦上之 URL 保留項目的通用儲存機制，而且會定義一組通用規則來保證唯一的 URL 保留項目。  
  
 當此服務啟動時，就會發生 *「URL 註冊」* 。 於是會建立要求佇列，而且 HTTP.SYS 會開始將要求路由傳送到該佇列。 必須先註冊 URL 端點之後，導向該端點的要求才會加入此佇列中。 當報表伺服器服務啟動時，它將會註冊保留給所有啟用之應用程式使用的所有 URL。 這表示必須啟用此 Web 服務，才會發生註冊。 如果您在原則式管理之 Reporting Services 的介面區組態 Facet 中，將 [WebServiceAndHTTPAccessEnabled]**** 屬性設定為 [False]****，當此服務啟動時，將不會註冊此 Web 服務的 URL。  
  
 如果您停止此服務或是回收此 Web 服務或報表管理員應用程式定義域，URL 會取消註冊。 如果您在此服務執行時修改 URL 保留項目，報表伺服器將會立即回收應用程式定義域，好讓舊的 URL 可以取消註冊，並使用新的 URL。  
  
 幾個簡單範例將可說明 URL 保留項目的概念，以及它如何與用於 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 應用程式的 URL 位址相關。 請注意一個要點，URL 保留項目的語法與用於存取此應用程式 URL 的語法不同：  
  
|HTTP.SYS 中的 URL 保留項目|URL|說明|  
|---------------------------------|---------|-----------------|  
|http://+:80/reportserver|HTTP://\<computername>/reportserver<br /><br /> HTTP://\<IPAddress>/reportserver<br /><br /> http://localhost/reportserver|此 URL 保留項目會在通訊埠 80 上指定萬用字元 (+)。 如此會將任何指定可在通訊埠 80 上解析為報表伺服器電腦之主機的內送要求放入報表伺服器佇列中。 請注意在處理這個 URL 保留項目時，可使用任意數目的 URL 來存取報表伺服器。<br /><br /> 對於大多數作業系統而言，這是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器的預設 URL 保留項目。|  
|http://123.45.67.0:80/reportserver|http://123.45.67.0/reportserver|此 URL 保留項目會指定 IP 位址，而且比起萬用字元 URL 保留項目更具限制性。 只有包含此 IP 位址的 URL 可用來連接報表伺服器。 假設此 URL 保留專案，在 HTTP://\<computername> 的報表伺服器要求會/reportserver 或http://localhost/reportserver失敗。|  
  
##  <a name="default-urls"></a><a name="DefaultURLs"></a>預設 Url  
 如果您使用預設組態安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，安裝程式將會保留 URL 供報表伺服器 Web 服務和報表管理員使用。 當您在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具內定義 URL 保留項目時，您也可以接受這些預設值。 如果您安裝 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 或是將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝為具名執行個體，預設 URL 將會包含執行個體名稱。  
  
> [!IMPORTANT]  
>  執行個體字元是一個底線字元 (`_`)。  
  
 URL 保留項目包含通訊埠編號。 下列作業系統將允許多個 Web 應用程式共用一個連接埠：  
  
1.  [!INCLUDE[win8srv](../../includes/win8srv-md.md)]  
  
2.  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]  
  
3.  [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]  
  
4.  [!INCLUDE[win7](../../includes/win7-md.md)]  
  
5.  [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)]  
  
|執行個體類型|Application|預設 URL|HTTP.SYS 中的實際 URL 保留項目|  
|-------------------|-----------------|-----------------|----------------------------------------|  
|預設執行個體|報表伺服器 Web 服務|HTTP://\<servername>/reportserver|HTTP://\<servername>： 80/reportserver|  
|預設執行個體|報表管理員|HTTP://\<servername>/reportserver|HTTP://\<servername>： 80/reportserver|  
|具名執行個體|報表伺服器 Web 服務|HTTP://\<servername>/reportserver_\<instancename>|HTTP://\<servername>： 80/reportserver_\<instancename>|  
|具名執行個體|報表管理員|HTTP://\<servername>/reports_\<instancename>|HTTP://\<servername>： 80/reports_\<instancename>|  
|SQL Server Express|報表伺服器 Web 服務|HTTP://\<servername>/reportserver_SQLExpress|HTTP://\<servername>： 80/reportserver_SQLExpress|  
|SQL Server Express|報表管理員|HTTP://\<servername>/reports_SQLExpress|HTTP://\<servername>： 80/reports_SQLExpress|  
  
##  <a name="authentication-and-service-identity-for-reporting-services-urls"></a><a name="URLPermissionsAccounts"></a>Reporting Services Url 的驗證和服務識別  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 保留項目會指定報表伺服器服務的服務帳戶。 執行此服務所用的帳戶會用於針對相同執行個體內執行之 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 應用程式所建立的所有 URL。 報表伺服器執行個體的服務識別會儲存在 RSReportServer.config 檔案中。  
  
 此服務帳戶沒有預設值。 但是，安裝期間需要指定服務帳戶，而且即使您在僅限檔案模式下安裝伺服器，仍然會在 RSReportServer.config 的 `URLReservation` 中指定服務帳戶。 此服務帳戶的有效值包括網域使用者帳戶、`LocalSystem` 或 `NetworkService`。  
  
 由於預設安全性為 `RSWindowsNegotiate`，所以會停用匿名存取。 如果是內部網路存取，報表伺服器 URL 會使用網路電腦名稱。 如果您想要設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 進行網際網路連接，就必須使用不同的設定。 如需驗證的詳細資訊，請參閱《 [線上叢書》中的](../security/authentication-with-the-report-server.md) 使用報表伺服器驗證 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
##  <a name="urls-for-local-administration"></a><a name="URLlocalAdmin"></a> 用於本機管理的 URL  
 如果您指定了強式或弱式萬用字元作為 URL 保留項目，則可以使用 http://localhost/reportserver 或 http://localhost/reports。  
  
 http://localhost URL 會解譯成 http://127.0.0.1。 如果您將 URL 保留項目限制為電腦名稱或單一 IP 位址，則除非您針對本機電腦上的 127.0.0.1 建立其他保留項目，否則將無法使用 localhost。 同樣地，如果電腦上已停用 localhost 或 127.0.0.1，您將無法使用該 URL。  
  
  和  包含新的安全性功能，可讓意外使用更高權限執行程式的風險降到最低。 您需要其他步驟，才能在這些作業系統上啟用管理。 如需詳細資訊，請參閱 [設定原生模式報表伺服器進行本機管理 &#40;SSRS&#41;](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
##  <a name="urls-for-report-server-in-sharepoint-integrated-mode"></a><a name="URLSharePoint"></a>SharePoint 整合模式中的報表伺服器 Url  
 如果獨立報表伺服器設定為在 SharePoint 產品或技術的大型部署內執行，URL 和虛擬目錄建構將受到以下方面的影響：  
  
-   報表和其他項目的 URL 會透過 SharePoint Web 應用程式 URL 來定址。 如果是特定報表的 URL 存取，請一定要使用包含網站路徑、文件庫、項目名稱和副檔名 (例如用於報表的 .rdl) 的完整 URL。 在報表中參考共用資料來源和模型時，以及當您將作業發行至報表伺服器時指定目標伺服器和資料夾時，必須指定完整的 URL。  
  
-   副檔名是用來區分不同類型的報表伺服器項目。 有效的副檔名包括報表定義的 .rdl、報表模型的 .smdl 以及針對 SharePoint 網站建立之共用資料來源的 .rsds。  
  
-   雖然 SharePoint 產品和技術有為其定義的 URL 保留項目，但是當您發行到伺服器時，可以忽略此保留項目。 如果是 SharePoint Web 應用程式，URL 保留會是內部作業。  
  
-   對於整合報表伺服器和 SharePoint 技術實例安裝在同一部電腦上的單一伺服器部署，您無法使用http://localhost/reportserver。 如果http://localhost用來存取 SharePoint Web 應用程式，您就必須使用非預設的網站或唯一的通訊埠指派來存取報表伺服器。 此外，如果此報表伺服器與 SharePoint 伺服陣列整合在一起，將不會針對此部署中安裝於遠端電腦上的節點來解析報表伺服器的 localhost 存取。  
  
-   報表管理員的 URL 保留項目和端點將無法針對 SharePoint 整合模式下執行的報表伺服器來設定。 如果真要設定，該項目在 SharePoint 整合模式下部署報表伺服器之後就無法再運作。 此模式不支援報表管理員。  
  
 如果您整合了報表伺服器向外延展部署，使其在較大的 SharePoint 產品或技術部署中執行，請讓報表伺服器節點負載平衡，並為向外延展部署定義單一虛擬伺服器 URL。 報表伺服器整合設定只允許您指定單一報表伺服器 URL。 如果是向外延展部署，此 URL 必須是向外延展部署中伺服器節點的存取點。  
  
## <a name="see-also"></a>另請參閱  
 [設定 SSRS Configuration Manager &#40;的 URL&#41;](configure-a-url-ssrs-configuration-manager.md)   
 [URL 保留項目語法 &#40;SSRS 組態管理員&#41;](url-reservation-syntax-ssrs-configuration-manager.md)  
  
  
