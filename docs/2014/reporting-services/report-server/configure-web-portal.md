---
title: 設定報表管理員 （原生模式） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Manager [Reporting Services], configuring
ms.assetid: e918986c-af15-48f6-8178-256aed829c6a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8bea75455bca695baa949d70bcef3909ac729cb7
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59953254"
---
# <a name="configure-report-manager-native-mode"></a>設定報表管理員 (原生模式)
  報表管理員是一個 Web 前端應用程式，可用來檢視報表、管理報表伺服器內容，以及將原生模式報表伺服器的存取權授與使用者。 如果您在安裝程式中選取 [Install in the default native mode configuration (以預設原生模式組態安裝)] 選項，報表管理員就會與報表伺服器 Web 服務一起安裝在相同的報表伺服器執行個體中，而且進行選擇性設定。 您也可以將報表管理員設定為後續安裝工作。 本主題會提供有關下列報表管理員組態狀況的資訊：  
  
-   [將報表管理員設定為使用預設 URL](#ConfigureRMURL)  
  
     報表管理員是使用者在網頁瀏覽器中存取的 Web 應用程式。 您至少必須定義用來在瀏覽器視窗中開啟應用程式的 URL。 此 URL 包含主機名稱、通訊埠和虛擬目錄。 此 URL 的預設值包括您針對報表伺服器 Web 服務 URL 所定義的主機名稱和通訊埠值，再加上 **reports** 虛擬目錄名稱。 如果您擁有具名執行個體，此虛擬目錄就是 **reports_instance**，其中 **instance** 是您 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體的名稱。  
  
-   **從遠端電腦執行報表管理員**。 根據網路組態而定，您可能需要啟用電腦上的通訊埠 80，允許使用報表管理員提出要求。  
  
    > [!TIP]  
    >  如果您嘗試存取遠端電腦上的報表管理員，但是在瀏覽器中收到連接錯誤訊息，常見的原因會是防火牆設定。 如需詳細資訊，請參閱 [設定供報表伺服器存取的防火牆](configure-a-firewall-for-report-server-access.md)。  
  
     必要時，啟用這兩部電腦的通訊埠 80，以便允許通過該通訊埠的要求。 如需詳細資訊，請參閱 [設定供報表伺服器存取的防火牆](configure-a-firewall-for-report-server-access.md)。  
  
-   [將報表管理員設定為使用特定報表伺服器 URL](#ConfigureSpecificURL)  
  
     根據預設，報表管理員會連接至在相同報表伺服器服務內執行的報表伺服器 Web 服務。 報表管理員會使用報表伺服器 Web 服務 URL 來建立連接。 如果您針對報表伺服器 Web 服務定義了多個 URL，報表管理員就會使用您所定義的最後一個 URL。 不過，在某些部署中，您可能會想讓報表管理員永遠透過靜態 URL 連接至 Web 服務。 您可能會想要這樣做的原因如下：如果您針對特定通訊埠或 IP 位址設定了封包篩選，而且想讓報表伺服器的所有連接都通過您所定義的篩選規則。  
  
-   [將報表管理員指向遠端報表伺服器](#ConfigureRemoteRS)  
  
     根據預設，報表管理員會提供在相同伺服器執行個體中執行之報表伺服器 Web 服務的前端存取權，但是如果您想要在不同的處理序中執行 Web 服務和報表管理員，或者您要針對每部伺服器以不同方式設定伺服器存取權 (例如，如果您要針對外部網路或網際網路連接上的使用者部署報表管理員，而且想要在報表伺服器與報表管理員之間放置防火牆)，就可以將報表管理員設定為連接至遠端報表伺服器 Web 服務。  
  
-   [自訂樣式和應用程式標題](#ModifyTitle)  
  
     您可以透過變更樣式和編輯顯示在報表管理員中的應用程式標題，以有限的方式自訂報表管理員、HTML 報表檢視器和報表工具列。  
  
-   [關閉報表管理員](#DisableRM)  
  
     當您安裝使用原生模式的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體時，預設就會啟用報表管理員。 不過，如果您擁有提供對等功能的自訂前端應用程式、您只想要使用 SOAP 或 URL 存取介面來存取報表伺服器，或者您要從不同的報表伺服器執行個體使用報表管理員，就可以關閉報表管理員。  
  
## <a name="prerequisites"></a>先決條件  
 若要使用報表管理員，您必須滿足下列必要條件：  
  
-   您必須擁有以最低限度方式設定的報表伺服器。 如需如何以最低限度方式設定報表伺服器的詳細資訊，請參閱[設定報表伺服器 &#40;Reporting Services 原生模式&#41;](configure-a-report-server-reporting-services-native-mode.md)。  
  
-   您的報表伺服器必須以原生模式執行。 您無法使用報表管理員搭配針對 SharePoint 整合模式所設定的報表伺服器。 在 SQL Server 2012 中，您無法將報表伺服器從一種模式切換為另一種模式。 如果您要變更您環境使用之報表伺服器的類型，必須安裝所需之模式的報表伺服器，然後將報表項目複製或移動到新的報表伺服器。 這項處理序通常稱為「移轉」。 移轉所需的步驟，取決於您要移轉到哪個模式以及您要從哪個版本移轉。 如需詳細資訊，請參閱＜ [Upgrade and Migrate Reporting Services](../install-windows/upgrade-and-migrate-reporting-services.md)＞。  
  
-   您也必須擁有啟用指令碼的 Internet Explorer 7.0 或更新版本。 如需詳細資訊，請參閱 <<c0> [ 規劃 Reporting Services 和 Power View 瀏覽器支援&#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)。</c0>  
  
##  <a name="ConfigureRMURL"></a> 將報表管理員設定為使用預設 URL  
 根據預設，報表管理員 URL 包含唯一的虛擬目錄名稱，再加上針對在相同執行個體中執行之報表伺服器 Web 服務所定義的通訊埠和主機名稱。 在大部分情況下，主機名稱就是報表伺服器電腦的網路名稱，但是它可能也是解析電腦的 IP 位址或主機標頭。 若要將報表管理員設定為使用預設 URL，請使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具中的 [報表管理員 URL] 頁面。  
  
#### <a name="to-configure-the-default-report-manager-url-and-virtual-directory"></a>設定預設的報表管理員 URL 和虛擬目錄  
  
1.  啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，並連接到報表伺服器執行個體。  
  
2.  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具中，按一下 [報表管理員 URL] 開啟設定 URL 的頁面。  
  
3.  針對報表管理員輸入唯一的虛擬目錄名稱。  
  
4.  按一下 **[套用]**。  
  
5.  如果您正在使用 [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] 或 Windows Server 2008，可能需要進行其他步驟，才能使用報表管理員。 如需詳細資訊，請參閱 [設定原生模式報表伺服器進行本機管理 &#40;SSRS&#41;](configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
##  <a name="ConfigureSpecificURL"></a> 將報表管理員設定為使用特定報表伺服器 URL  
 當您在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具中設定 URL 時，報表管理員就會針對在相同伺服器執行個體中執行的報表伺服器，自動偵測並使用任何全新和更新的 URL。 如果您的部署要求您針對所有報表伺服器要求使用單一靜態 URL，就可以在 RSReportServer.config 檔中指定該 URL。  
  
#### <a name="to-configure-a-static-report-server-url"></a>設定靜態報表伺服器 URL  
  
1.  在文字編輯器中開啟 **RsReportServer.config** 檔。 根據預設，其位於 \Program Files\Microsoft SQL Server\MSRS12.\<*instancename*>\Reporting Services\ReportServer。  
  
2.  尋找 `ReportServerURL`。  
  
3.  將它取代成報表伺服器執行個體的 URL。  
  
4.  儲存您的變更，然後關閉檔案。  
  
 如需組態檔的詳細資訊，請參閱[修改 Reporting Services 組態檔&#40;RSreportserver.config&#41; ](modify-a-reporting-services-configuration-file-rsreportserver-config.md)並[RSReportServer Configuration File](rsreportserver-config-configuration-file.md)。  
  
##  <a name="ConfigureRemoteRS"></a> 將報表管理員設定為使用遠端報表伺服器  
 若為將報表管理員和報表伺服器放置於不同電腦上的部署組態，您就必須擁有兩個個別的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]安裝。 報表管理員內嵌在報表伺服器服務中，而且無法單獨安裝。 如果您想要在不同的電腦上於自己的處理序中執行報表管理員，就必須安裝第二個報表伺服器。 這兩個伺服器執行個體都必須是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 報表伺服器。  
  
#### <a name="to-connect-report-manager-to-a-remote-report-server-instance"></a>將報表管理員連接至遠端報表伺服器執行個體  
  
1.  安裝兩個報表伺服器執行個體。  
  
2.  設定即將主控報表伺服器的第一個安裝：  
  
    1.  啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具。  
  
    2.  按一下 [Web 服務 URL] 設定報表伺服器的主機名稱、通訊埠和虛擬目錄。  
  
    3.  按一下 [資料庫] 設定報表伺服器資料庫。  
  
3.  設定即將主控報表管理員的第二個安裝：  
  
    1.  啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具。  
  
    2.  按一下 [報表管理員 URL] 輸入報表管理員的虛擬目錄名稱。  
  
     請勿設定資料庫。 請勿測試 URL。  
  
4.  在報表管理員電腦上，將 RSReportServer.config 中的組態設定修改成指向遠端報表伺服器執行個體。 啟動時，報表管理員就會讀取組態檔，以便取得報表伺服器的 URL：  
  
    1.  在文字編輯器中開啟 RSReportServer.config。 根據預設，它是位於 \Program Files\Microsoft SQL Server\MSRS11 項目。\< *instancename*> services\reportserver。  
  
    2.  尋找 `ReportServerURL`。  
  
    3.  將它取代成遠端報表伺服器執行個體的 URL。  
  
    4.  儲存您的變更，然後關閉檔案。  
  
5.  > [!TIP]  
    >  必要時，啟用這兩部電腦的通訊埠 80，以便允許通過該通訊埠的要求。 如需詳細資訊，請參閱 [設定供報表伺服器存取的防火牆](configure-a-firewall-for-report-server-access.md)。  
  
6.  重新啟動報表伺服器。  
  
7.  在瀏覽器視窗中開啟報表管理員。 如果它原本就已經開啟，請重新整理瀏覽器，以便確認報表管理員連接至遠端伺服器。 此時，您應該會看見目標伺服器的內容。  
  
8.  關閉您不要使用的伺服器功能：  
  
    -   在報表管理員電腦上，關閉 `WebServiceAndHTTPAccessEnabled` 和 `ScheduleEventsAndReportDeliveryEnabled`。  
  
    -   在報表伺服器電腦上，關閉 `ReportManagerEnabled`。  
  
 如需關閉功能的詳細資訊，請參閱 [開啟或關閉 Reporting Services 功能](turn-reporting-services-features-on-or-off.md)。  
  
##  <a name="ModifyTitle"></a> 自訂樣式或應用程式標題  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 不支援自訂報表管理員的樣式表。 不過，如果您具備 Web 開發的專業知識，就可以修改這些樣式，但風險自負。 如需哪些檔案包含樣式資訊的詳細資訊，請參閱 [自訂 HTML 檢視器及報表管理員的樣式表](../customize-style-sheets-for-html-viewer-and-report-manager.md)。  
  
 報表管理員具有顯示在頁面頂端的應用程式標題。 根據預設，這個標題是 **SQL Server Reporting Services**。 您可以自訂這個標題。 若要變更此標題，請使用報表管理員中的 [站台設定] 頁面。 若要在報表管理員中修改應用程式設定，您必須被指派至 [系統管理員] 角色，才能設定 [站台設定] 頁面上的屬性。 若要檢視應用程式標題，使用者必須被指派至 [系統使用者] 角色。  
  
#### <a name="to-modify-application-title"></a>修改應用程式標題  
  
1.  使用被指派報表伺服器之 [系統管理員] 權限的帳戶來登入。  
  
2.  開啟 Internet Explorer。  
  
3.  輸入報表管理員 URL。 根據預設，它是 http://\<**您的伺服器名稱**>/reports，但是如果您將 Reporting Services 安裝成具名執行個體，預設 URL 就是 http://\<**您的伺服器名稱**>/reports\<**_執行個體名稱**>。  
  
4.  按一下 **[站台設定]**。  
  
5.  在 [一般] 索引標籤的 [名稱] 中，將 **SQL Server Reporting Services** 取代成不同的名稱。  
  
6.  按一下 **[套用]**。  
  
##  <a name="DisableRM"></a> Turn Off Report Manager  
 如果您擁有提供對等功能的自訂應用程式，或者您要使用不同服務執行個體的報表管理員應用程式，就可以關閉報表管理員。 若要關閉報表管理員，您可以修改 RSReportServer.config 檔。  
  
#### <a name="to-turn-off-report-manager"></a>關閉報表管理員  
  
1.  在文字編輯器中開啟 RSReportServer.config 檔。 根據預設，它是位於 \Program Files\Microsoft SQL Server\MSRS11 項目。\< *instancename*> services\reportserver。  
  
2.  尋找 **IsReportManagerEnabled**。  
  
3.  將此值設定為 **False**。  
  
4.  儲存您的變更，然後關閉檔案。  
  
 如需如何修改組態檔的詳細資訊，請參閱[修改 Reporting Services 組態檔 &#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md)。 如需停用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中功能的詳細資訊，請參閱[開啟或關閉 Reporting Services 功能](turn-reporting-services-features-on-or-off.md)。  
  
## <a name="see-also"></a>另請參閱  
 [報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)   
 [規劃 Reporting Services 和 Power View 瀏覽器支援&#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)   
 [設定 URL &#40;SSRS 組態管理員&#41;](../install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [驗證 Reporting Services 安裝](../install-windows/verify-a-reporting-services-installation.md)   
 [自訂 HTML 檢視器及報表管理員的樣式表](../customize-style-sheets-for-html-viewer-and-report-manager.md)   
 [開啟或關閉 Reporting Services 功能](turn-reporting-services-features-on-or-off.md)   
 [管理 Reporting Services 原生模式報表伺服器](manage-a-reporting-services-native-mode-report-server.md)   
 [RSReportServer 組態檔](rsreportserver-config-configuration-file.md)   
 [設定原生模式報表伺服器進行本機管理 &#40;SSRS&#41;](configure-a-native-mode-report-server-for-local-administration-ssrs.md)  
  
  
