---
title: 設定 URL (SSRS 設定管理員) | Microsoft Docs
ms.custom: ''
ms.date: 05/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: install-windows
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- URL access [Reporting Services], syntax
ms.assetid: 851e163a-ad2a-491e-bc1e-4df92327092f
caps.latest.revision: 13
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5a2f13d7a3931656ba166a14a71ef45f7c8b83ce
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="configure-a-url--ssrs-configuration-manager"></a>設定 URL (SSRS 組態管理員)
  使用 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 或報表伺服器 Web 服務之前，您至少必須為每一個應用程式設定一個 URL。 如果您在「僅限檔案」模式下安裝了 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (意即在安裝精靈的 [報表伺服器安裝選項] 頁面中選取 [安裝但不設定伺服器] 選項)，就一定要設定 URL。 如果您在預設組態中安裝了 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，就表示已經為每一個應用程式設定了 URL。  
  
 使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具可設定 URL， URL 的所有部分都會定義在這個工具中。 與舊版不同的是，Internet Information Services (IIS) 網站不再提供 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和更新版本中 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 應用程式的存取權。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會提供可在大多數部署狀況下順利運作的預設值，包括與其他 Web 服務和應用程式的並存部署。 預設 URL 會併入執行個體名稱，好讓在相同電腦上執行多個報表伺服器執行個體時的 URL 衝突風險降到最低。  
  
 本主題提供下列工作的指示：  
  
-   為報表伺服器 Web 服務建立 URL。  
  
-   為 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]建立 URL。  
  
-   設定進階的 URL 屬性，以定義其他 URL。  
  
 如需如何儲存和維護 URL 或是互通性問題的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的[關於 URL 保留項目和註冊 &#40;SSRS 設定管理員&#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md) 和[並存安裝 Reporting Services 和 Internet Information Services &#40;SSRS 原生模式&#41;](../../reporting-services/install-windows/install-reporting-and-internet-information-services-side-by-side.md)。 若要檢閱 Reporting Services 安裝中常用的 URL 範例，請參閱本主題的＜ [URL 範例](#URLExamples) ＞。  
  
## <a name="prerequisites"></a>Prerequisites  
 在您建立或修改 URL 之前，請記住以下要點：  
  
-   您在報表伺服器電腦上必須是本機管理員群組的成員。  
  
-   如果相同電腦上安裝了 IIS，請檢查使用通訊埠 80 之任何網站上的虛擬目錄名稱。 如果您看到任何虛擬目錄使用預設 Reporting Services 虛擬目錄名稱 (意即 "Reports" 和 "ReportServer")，請為您設定的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 選擇不同的虛擬目錄名稱。  
  
-   您必須使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具來設定 URL， 請勿使用系統公用程式。 絕對不要直接在 RSReportServer.config 檔案的 **URLReservations** 區段中修改 URL 保留項目。 若要更新儲存於內部的基礎 URL 保留項目以及同步處理 RSReportServer.config 檔案中儲存的 URL 設定，必須要使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具。  
  
-   請選擇具有低報表活動的時間。 每當 URL 保留項目變更時，您就可以預期報表伺服器 Web 服務和 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 的應用程式定義域可能會回收使用。  
  
-   如需 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]URL 建構和使用方式的概觀，請參閱 [設定報表伺服器 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)建立 URL。  
  
### <a name="to-configure-a-url-for-the-report-server-web-service"></a>為報表伺服器 Web 服務設定 URL  
  
1.  啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，並連接到本機報表伺服器執行個體。  
  
2.  按一下 **[Web 服務 URL]**。  
  
3.  指定虛擬目錄。 此虛擬目錄名稱會識別哪一個應用程式將接收要求。 由於 IP 位址和通訊埠可由多個應用程式共用，所以此虛擬目錄名稱會指定哪一個應用程式要接收要求。  
  
     這個值必須是唯一的，以確保此要求可送到所要的目的地。 這是必要的值。 而且不區分大小寫。 虛擬目錄名稱與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 應用程式的執行個體之間為一對一的對應關係。 如果您對相同的應用程式執行個體建立多個 URL，必須在為此應用程式執行個體定義的所有 URL 中使用相同的虛擬目錄名稱。  
  
     如果是報表伺服器 Web 服務，預設虛擬目錄名稱會是 **ReportServer**。  
  
4.  指定可唯一識別網路上之報表伺服器電腦的 IP 位址。 如果您想要指定主機標頭，或針對相同的應用程式執行個體定義其他 URL，您必須按一下 **[進階]**。 如需有關如何針對 URL 設定進階屬性的指示，請參閱本主題稍後的指示。 否則，請使用 **[Web 服務 URL]** 頁面，從下列值當中選取：  
  
    -   **[全部指派]** 會指定指派給電腦的任何一個 IP 位址都可以用於指向報表伺服器應用程式的 URL。 這個值也包含易記主機名稱 (如電腦名稱)，網域名稱伺服器可將該名稱解析為指派給電腦的 IP 位址。 這是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 的預設值。  
  
    -   **[全未指派]** 會指定報表伺服器將會接收另一個應用程式尚未處理的任何要求。 建議您避免使用這個選項。 如果您選取這個選項，則另一個具有更強式 URL 保留項目的應用程式就可能會攔截要送給報表伺服器的要求。  
  
    -   **[127.0.0.1]** 是用來存取 localhost 的 IPv4 位址， 它可支援報表伺服器電腦上的本機管理。 如果您只選取這個值，則只有在本機登入報表伺服器電腦的使用者才會擁有此應用程式的存取權。  
  
    -   **[::1]** 是 IPv6 格式的回送位址。  
  
    -   特定的 IP 位址也會出現在這個清單中。 IP 位址可以採用 IPv4 和 IPv6 格式。 *Nnn.nnn.nnn.nnn* 是電腦網路介面卡的 32 位元 IPv4 位址。 IPv6 位址為 128 位元，具有以冒號分隔的八個 4 位元組的欄位：\<前置詞>:*nnnn:nnnn:nnnn:nnnn:nnnn:nnnn*  
  
         如果您有多張網路介面卡或是您的網路同時支援 IPv4 和 IPv6 位址，您將會看到多個 IP 位址。 如果您只選取一個 IP 位址，它會將應用程式存取限制為只有該 IP 位址 (以及網域名稱伺服器對應至該位址的任何主機名稱)。 您無法使用 localhost 來存取報表伺服器，而且也不能使用安裝於報表伺服器電腦上之其他網路卡的 IP 位址。 一般來說，如果您選取這個值，這是因為您正在設定多個同時也指定明確 IP 位址或主機名稱的 URL 保留項目 (例如，一個項目用於內部網路連接的網路介面卡，另一個項目用於外部網路連接)。  
  
5.  指定通訊埠。 通訊埠 80 是預設值，因為它可以與其他應用程式共用。 如果您想要使用自訂通訊埠編號，請記得一定要在用來存取報表伺服器的 URL 中指定它。 您可以使用下列方法來尋找可用的通訊埠：  
  
    -   從命令提示字元輸入下列命令，以傳回所使用的 TCP 通訊埠清單：  
  
         `netstat –anp tcp`  
  
    -   請檢閱 Microsoft 技術支援文件 [TCP/IP 連接埠指派資訊](http://support.microsoft.com/kb/174904)，以閱讀有關 TCP 通訊埠指派以及已知通訊埠 (0 到 1023)、已註冊的通訊埠 (1024 到 49151) 和動態或私人通訊埠 (49152 到 65535) 之間差異的資訊。  
  
    -   如果您正在使用 Windows 防火牆，您必須開啟此通訊埠。 如需指示，請參閱 [Configure a Firewall for Report Server Access](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)。  
  
6.  如果您尚未這樣做，請確認 IIS (如果已安裝) 並沒有與您打算使用之名稱相同的虛擬目錄。  
  
7.  如果您安裝了 SSL 憑證，您可以現在選取它，以便將此 URL 繫結至電腦上所安裝的 SSL 憑證。  
  
8.  如果您選擇性地選取 SSL 憑證，您就可以指定自訂通訊埠。 預設值是 443，但是您可以使用任何可用的通訊埠。  
  
9. 按一下 **[套用]** ，即可建立此 URL。  
  
10. 按一下頁面 **[URL]** 區段中的連結來測試此 URL。 請注意，在您可以測試此 URL 之前，必須先建立及設定報表伺服器資料庫。 如需指示，請參閱[建立原生模式報表伺服器資料庫 &#40;SSRS 設定管理員&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)。  

> [!NOTE]  
>  如果您有現有的 SSL 繫結和 URL 保留項目，而您想要變更 SSL 繫結，例如使用不同的憑證或主機標頭，則建議您依序完成以下步驟：  
>   
>  1.  先移除所有 URL 保留項目。  
> 2.  然後移除所有 SSL 繫結。  
> 3.  然後重新建立 URL 和 SSL 繫結。  
>   
>  前述步驟可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員完成。  
>   
>  Microsoft Windows 針對每個 IP 位址與通訊埠組合支援一個繫結。 如果您將報表伺服器設定為使用特定主機標頭值，同時將通訊埠至 IP 位址組合上的憑證發給不同的主機標頭值，則會在瀏覽器中看見一個警告，指出憑證與所使用的 URL 不相符。  
>   
>  若要更正這個問題，請刪除所有繫結，然後使用唯一的設定建立新繫結，或設定包含萬用字元的 Reporting Services URL 註冊。
  
### <a name="to-create-a-url-reservation-for-the-includessrswebportalincludesssrswebportalmd"></a>建立 URL 保留項目 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]  
  
1.  啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，並連接到報表伺服器執行個體。  
  
2.  按一下 [入口網站 URL]。  
  
3.  指定虛擬目錄。 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 會接聽與報表伺服器 Web 服務相同的 IP 位址和通訊埠。 如果您設定 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 指向不同的報表伺服器 Web 服務，您必須修改 RSReportServer.config 檔案中的 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] URL 設定。  
  
4.  如果您安裝了 SSL 憑證，就可以選取它，以便要求送給 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 的所有要求都透過 HTTPS 路由傳送。  
  
     如果您選擇性地選取 SSL 憑證，您就可以指定自訂通訊埠。 預設值是 443，但是您可以使用任何可用的通訊埠。  
  
5.  按一下 **[套用]** ，即可建立此 URL。  
  
6.  按一下頁面 **[URL]** 區段中的連結來測試此 URL。  
  
## <a name="setting-advanced-properties-to-specify-additional-urls"></a>設定進階屬性來指定其他 URL  
 您可以藉由指定不同的通訊埠或主機名稱，為報表伺服器 Web 服務或 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 保留多個 URL (可以是 IP 位址，或是網域名稱伺服器可解析為指派給電腦之 IP 位址的主機標頭名稱)。 您可以藉由建立多個 URL，設定對相同報表伺服器執行個體的不同存取路徑。 例如，若要啟用對報表伺服器的內部網路和外部網路存取，您可能會使用預設 URL 來存取內部網路，並使用額外的完整主機名稱來存取外部網路：  
  
-   `http://myserver01/reportserver`  
  
-   `http://www.adventure-works.com/reportserver`  
  
 您不能為相同的應用程式執行個體設定多個虛擬目錄名稱。 每一個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 應用程式執行個體都會對應到單一虛擬目錄名稱。 如果您在相同電腦上有多個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體，應用程式的虛擬目錄名稱應該包含此執行個體名稱，以確保每一個要求都會到達所要的目標。  
 
  **主機標頭**  
 如果您已經在網域名稱伺服器上定義解析為電腦的主機標頭，您可以在設定報表伺服器存取的 URL 中指定該主機標頭。  
  
 主機標頭是可讓多個網站共用單一 IP 位址和通訊埠的唯一名稱。 主機標頭名稱要比 IP 位址和通訊埠編號更容易記得和輸入。 主機標頭名稱的一個範例為 www.adventure-works.com。  
  
 **SSL 通訊埠**  
 為 SSL 連接指定通訊埠。 SSL 的預設通訊埠是 443。  
  
 **SSL 憑證**  
 指定您安裝在這部電腦上之 SSL 憑證的憑證名稱。 如果此憑證對應到萬用字元，您可以將它用於報表伺服器連接。  
  
 指定註冊憑證的完整電腦名稱。 所指定的名稱必須與註冊的憑證名稱相同。  
  
 您必須安裝了憑證，才能使用此選項。 您也必須修改 RSReportServer.config 檔案中的 UrlRoot 組態設定，使它指定註冊憑證之電腦的完整名稱。 如需詳細資訊，請參閱《 [線上叢書》中的](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) 在原生模式報表伺服器上設定 SSL 連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
### <a name="to-set-advanced-properties-on-a-url"></a>設定 URL 的進階屬性  
  
1.  在 [Web 服務 URL] 或 [入口網站 URL] 頁面上，按一下 [進階]。  
  
2.  按一下 **[加入]**。  
  
3.  按一下 IP 位址或主機標頭名稱。 如果您指定主機標頭，請務必指定 DNS 服務可以解析的名稱。 如果您要指定公開可用的網域名稱，請包含整個 URL，包括 `http://www` 在內。  
  
4.  指定通訊埠。 如果您指定自訂通訊埠，應用程式的 URL 一定要包含通訊埠編號。  
  
5.  按一下 [確定] 。  
  
6.  開啟瀏覽器視窗，並輸入此 URL 加以測試。  
  
## <a name="urls-for-multiple-report-server-instances-on-the-same-computer"></a>相同電腦上多個報表伺服器執行個體的 URL  
 如果您為多個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]執行個體保留 URL，您應該遵循命名慣例，好讓您可以避免命名衝突。 如需詳細資訊，請參閱[多重執行個體報表伺服器部署的 URL 保留項目 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/url-reservations-for-multi-instance-report-server-deployments.md)。  
  
##  <a name="URLExamples"></a> URL 組態的範例  
 下列清單顯示一些報表伺服器 URL 的範例：  
  
-   `http://localhost/reportserver`  
  
-   `http://localhost/reportserver_SQLEXPRESS`  
  
-   `http://sales01/reportserver`  
  
-   `http://sales01:8080/reportserver`  
  
-   `https://sales.adventure-works.com/reportserver`  
  
-   `https://www.adventure-works.com:8080/reportserver01`  
  
 您用以存取 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 的 URL 共用類似的格式，而且通常建立在主控報表伺服器的相同網站之下。 唯一不同的是虛擬目錄名稱 (在這個範例中為 **reports** ，但是您可以將它設定成想要使用的任何名稱)：  
  
-   `http://localhost/reports`  
  
-   `http://localhost/reports_SQLEXPRESS`  
  
-   `http://sales01/reports`  
  
-   `http://sales01:8080/reports`  
  
-   `https://sales.adventure-works.com/reports`  
  
-   `https://www.adventure-works.com:8080/reports`  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [設定報表伺服器 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)
