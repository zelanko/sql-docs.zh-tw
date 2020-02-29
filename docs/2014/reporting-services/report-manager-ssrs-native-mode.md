---
title: 報表管理員（SSRS 原生模式） |Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 04/26/2019
ms.openlocfilehash: 5cefc88469ac3c98f3bb944c0e490f1ce7e88472
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/28/2020
ms.locfileid: "78172371"
---
# <a name="report-manager--ssrs-native-mode"></a>報表管理員 (SSRS 原生模式)
  「報表管理員」是 Web 架構的報表存取與管理工具，用來從遠端位置透過 HTTP 連線管理單一報表伺服器執行個體。 您也可以使用報表管理員的報表檢視器和導覽功能。 本主題內容：

-   [什麼是報表管理員](#bkmk_whatis_report_manager)

-   [啟動及使用報表管理員](#bkmk_start_report_manager)

-   [圖示描述](#bkmk_icon_descriptions)

##  <a name="bkmk_whatis_report_manager"></a>什麼是報表管理員？
 您可以使用報表管理員執行下列工作：

-   檢視、搜尋、列印與訂閱報表。

-   建立、保護和維護資料夾階層，以組織伺服器上的項目。

-   設定以角色為基礎的安全性，此安全性決定對項目與作業的存取權。

-   設定報表執行屬性、報表記錄和報表參數。

-   建立[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]連接到資料來源或[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]關聯式資料來源之資料的報表模型。

-   設定模型項目安全性以存取模型中的特定項目，或將項目對應到您事先建立之預先定義的點選連結報表。

-   建立共用排程與共用資料來源，讓排程與資料來源連接更容易管理。

-   建立資料驅動訂閱，將報表傳遞至大型收件者清單。

-   建立連結報表，以重複使用並以不同的方式重新決定現有報表的用途。

-   啟動報表產生器來建立可以在報表伺服器上儲存與執行的報表。

 您可以使用報表管理員來瀏覽報表伺服器資料夾，或搜尋特定報表。 您可以檢視報表、報表一般屬性，以及在報表記錄中所擷取的過去報表副本。 根據您的權限，您也可以訂閱報表，以傳遞至電子郵件收件匣或檔案系統上的共用資料夾。

> [!NOTE]
>  如需支援的瀏覽器和版本的詳細資訊，請參閱[規劃 Reporting Services 和 Power View 瀏覽器支援 &#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)。

 報表管理員僅適用於以原生模式執行的報表伺服器。 不支援針對 SharePoint 整合模式設定的報表伺服器。

 部分報表管理員的功能只在指定的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本中提供。 如需詳細資訊，請參閱＜ [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)＞。

 在新的安裝上，只有本機管理員才有足夠的權限處理內容和設定。 若要授與權限給其他使用者，本機管理員必須建立角色指派，提供報表伺服器的存取權。 使用者在這之後可以存取的應用程式頁面和工作，會視該使用者的角色指派而定。 如需詳細資訊，請參閱[將報表伺服器的存取權授與使用者 &#40;報表管理員&#41;](security/grant-user-access-to-a-report-server.md)。

 如果您使用的是 [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)] 或 Windows Server 2008，就必須設定報表管理員以進行本機管理。 如需詳細資訊，請參閱 [設定原生模式報表伺服器進行本機管理 &#40;SSRS&#41;](report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。

##  <a name="bkmk_start_report_manager"></a>啟動和使用報表管理員
 報表管理員是一種 Web 應用程式，您可以在瀏覽器視窗的位址列中輸入報表管理員 URL 來開啟。 當您啟動報表管理員時，您所看到的頁面、連結和選項會依據您所擁有的報表伺服器權限而有所不同。 若要執行工作，您必須被指派包含此工作的角色。 指派至具有完整權限之角色的使用者，可以存取用於管理報表伺服器的完整應用程式功能表與頁面。 指派至具有檢視和執行報表權限之角色的使用者，只看得到支援這些活動的功能表與頁面。 每個使用者可以有針對不同報表伺服器的不同角色指派，甚至針對儲存在單一報表伺服器上之各種報表與資料夾的不同角色指派。

 如需角色的詳細資訊，請參閱 [在原生模式報表伺服器上授與權限](security/granting-permissions-on-a-native-mode-report-server.md)。

> [!NOTE]
>  如果您使用的是 Windows Vista 或 Windows Server 2008，就必須先設定用於本機管理的報表伺服器，然後才可以使用報表管理員來管理本機報表伺服器執行個體。 如需有關如何設定伺服器的指示，請參閱[&#40;SSRS&#41;設定原生模式報表伺服器進行本機管理](report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。

## <a name="start-report-manager"></a>啟動報表管理員

#### <a name="to-start-report-manager-from-a-browser"></a>若要從瀏覽器啟動報表管理員

1.  開啟 [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 7.0 或更新版本。

2.  在網頁瀏覽器的網址列中，輸入報表管理員 URL。

    -   根據預設，URL 為 `http://[ComputerName]/reports`的技巧。

    -   報表伺服器可能會設定為使用特定的通訊埠。 例如，`http:// [ComputerName]:80/reports` 或 `http:// [ComputerName]:8080/reports`。

## <a name="configuring-report-manager"></a>設定報表管理員
 報表管理員組態包含定義應用程式的 URL。 如果您的部署包括在個別的電腦上執行報表管理員，則需要其他組態。

 您只能以少數方式自訂報表管理員。 例如，您可以在 [站台設定] 頁面修改應用程式標題。 如果您是 Web 開發人員，則可以修改包含報表管理員使用之樣式資訊的樣式表。 由於報表管理員並非專門為支援自訂而設計，因此您必須仔細地測試您所做的任何修改。 如果您覺得報表管理員並不符合您的需求，您可以開發自訂報表檢視器，或是設定 SharePoint Web 組件，以便在 SharePoint 網站中尋找及檢視報表。 如需詳細資訊，請參閱[設定報表管理員 &#40;原生模式&#41;](report-server/configure-web-portal.md)。

##  <a name="bkmk_icon_descriptions"></a>圖示描述
 下表描述報表管理員中使用的圖示。 如需報告工具列中所出現圖示的詳細資訊，請參閱[HTML 檢視器和報告工具列](html-viewer-and-the-report-toolbar.md)。

|圖示|描述|動作|
|----------|-----------------|------------|
|![報表圖示](media/hlp-16doc.gif "報表圖示")|Report|按一下報表圖示或名稱，開啟報表。 報表會在個別視窗中開啟。|
|![模型圖示](media/model-icon.gif "模型圖示")|報表模型|按一下報表模型圖示來開啟模型屬性頁面。|
|![連結報表圖示](media/hlp-16linked.gif "連結報表圖示")|連結報表|按一下報表圖示或名稱來開啟連結報表。 報表會在個別視窗中開啟。|
|![資料夾圖示](media/hlp-16folder.gif "資料夾圖示")|資料夾|按一下資料夾圖示或名稱來開啟資料夾。|
|![訂閱圖示](media/hlp-16subscription.gif "訂閱圖示")|訂用帳戶|按一下訂閱圖示或描述來編輯訂閱。|
|![資料驅動訂閱圖示](media/hlp-16subscriptiondd.gif "資料驅動訂閱圖示")|資料驅動訂閱|按一下資料驅動訂閱圖示或描述來編輯訂閱。|
|![一般資源圖示](media/hlp-16file.gif "一般資源圖示")|資源|按一下資源圖示或名稱來開啟資源。 資源會在個別視窗中開啟。|
|![共用資料來源圖示](media/hlp-16datasource.png "共用資料來源圖示")|共用資料來源項目|按一下共用資料來源圖，來開啟資料來源的屬性頁面、報表清單和訂閱清單。|
|![屬性頁面圖示](media/hlp-16prop.gif "屬性頁面圖示")|屬性頁面|按一下屬性圖示來存取其他頁面，以設定屬性和安全性。|

## <a name="see-also"></a>另請參閱

- [設定 URL &#40;SSRS 組態管理員&#41;](install-windows/configure-a-url-ssrs-configuration-manager.md)
- [規劃 Reporting Services 和 Power View 瀏覽器支援 &#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)
- [報表產生器 &#40;SSRS&#41;](tools/report-builder-authoring-environment-ssrs.md)
- - [Reporting Services 工具](tools/reporting-services-tools.md)
- [報表伺服器內容管理 &#40;SSRS 原生模式&#41;](report-server/report-server-content-management-ssrs-native-mode.md) 
[報表管理員 F1](../../2014/reporting-services/report-manager-f1-help.md)說明