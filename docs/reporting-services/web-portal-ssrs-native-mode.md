---
title: 入口網站 (SSRS 原生模式) | Microsoft Docs
ms.custom: ''
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
ms.assetid: 7349e626-6ed5-4d21-b05f-cf042ad9ad70
caps.latest.revision: 15
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 0c88c0e5710a85b8e29e3d0852ac608f5cfca30d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="web-portal-ssrs-native-mode"></a>入口網站 (SSRS 原生模式)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Reporting Services 入口網站是一種 Web 體驗，可讓您檢視報表、行動報表、KPI，以及完整瀏覽報表伺服器執行個體中的項目。 您也可以使用入口網站來管理單一報表伺服器執行個體。

![ssRSPortal](../reporting-services/media/ssrsportal.png)

## <a name="what-is-the-web-portal"></a>什麼是入口網站

您可以使用入口網站來執行下列工作：

- 檢視、搜尋、列印與訂閱報表。

- 建立、保護和維護資料夾階層，以組織伺服器上的項目。

- 設定以角色為基礎的安全性，此安全性決定對項目與作業的存取權。

- 設定報表執行屬性、報表記錄和報表參數。

- 建立共用排程與共用資料來源，讓排程與資料來源連接更容易管理。

- 建立資料驅動訂閱，將報表傳遞至大型收件者清單。

- 建立連結報表，以不同方式重複使用現有報表並重新決定其用途。

- 下載常用工具，例如，報表產生器和行動報表發行工具。

- [建立 KPI](../reporting-services/working-with-kpis-in-reporting-services.md)。

- 傳送意見反應或功能要求。

您可以使用入口網站來瀏覽報表伺服器資料夾或搜尋特定報表。 您可以檢視報表、其一般屬性，以及過去在報表記錄中擷取的報表複本。 根據您的權限，您也可以訂閱報表，以傳遞至電子郵件收件匣或檔案系統上的共用資料夾。

> [!NOTE]
> 如需所支援瀏覽器和版本的相關資訊，請參閱 [規劃 Reporting Services 瀏覽器支援](../reporting-services/browser-support-for-reporting-services-and-power-view.md)。

入口網站僅適用於以原生模式執行的報表伺服器。 不支援針對 SharePoint 整合模式設定的報表伺服器。

部分入口網站功能只在指定的 [!INCLUDE[ssNoVersion](../includes/ssnoversion.md)] 版本中提供。 如需詳細資訊，請參閱 [SQL Server 2016 版本所支援的 Reporting Services 功能](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)。

在新的安裝上，只有本機管理員才有足夠的權限處理內容和設定。 若要授與權限給其他使用者，本機管理員必須建立角色指派，提供報表伺服器的存取權。 使用者在這之後可以存取的應用程式頁面和工作，會視該使用者的角色指派而定。 如需詳細資訊，請參閱[將報表伺服器的存取權授與使用者](security/grant-user-access-to-a-report-server-report-manager.md)

> [!NOTE]
> 如果您在伺服器執行所在的本機電腦上瀏覽至入口網站，可能會看到一則訊息，指出不允許您檢視這個資料夾。 這是因為通用存取控制 (UAC)，而且您不是以系統管理員身分執行瀏覽器所導致。您不能以系統管理員身分執行 Edge。您必須使用 Internet Explorer。 您可以從遠端瀏覽器至伺服器，或是以系統管理員身分啟動 Internet Explorer 並瀏覽至入口網站。 如果您想要從遠端使用入口網站，就必須為您的帳戶提供資料夾上的內容管理員權限。  

## <a name="start-and-use-the-web-portal"></a>啟動並使用入口網站

入口網站是一種 Web 應用程式，您可以在瀏覽器視窗的網址列中輸入 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] URL 來開啟。 當您啟動 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]時，您所看到的頁面、連結和選項會依據您在報表伺服器上擁有的權限而有所不同。 若要執行工作，您必須被指派包含此工作的角色。  指派至具有完整權限之角色的使用者，可以存取用於管理報表伺服器的完整應用程式功能表與頁面。 指派至具有檢視和執行報表權限之角色的使用者，只看得到支援這些活動的功能表與頁面。 每個使用者可以有針對不同報表伺服器的不同角色指派，甚至針對儲存在單一報表伺服器上之各種報表與資料夾的不同角色指派。

如需角色的詳細資訊，請參閱 [在原生模式報表伺服器上授與權限](../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)。

### <a name="start-the-web-portal"></a>啟動入口網站

若要從瀏覽器中啟動入口網站，請執行下列動作：

1. 開啟網頁瀏覽器。 如需支援的網頁瀏覽器清單，請參閱 [規劃 Reporting Services 瀏覽器支援](../reporting-services/browser-support-for-reporting-services-and-power-view.md)。

2. 在網頁瀏覽器的網址列中，輸入入口網站 URL。

    根據預設，URL 為 *http://[ComputerName]/reports*。

    報表伺服器可能會設定為使用特定的通訊埠。 例如， *http://[ComputerName]:80/reports* 或 *http://[ComputerName]:8080/reports*。

## <a name="grouping-by-categories"></a>依類別分組

入口網站會將項目分組為不同類別。 以下為可用的類別：

- KPI
- 行動報表
- 分頁的報表
- Power BI Desktop 報表
- Excel 活頁簿
- 資料集
- 資料來源
- 資源

您可以藉由選取右上角的 [檢視]，來控制要顯示的內容。 如果您選取 [顯示隱藏項]，則這些項目將以較淡的色彩來顯示。

![ssRSWebPortal-view](../reporting-services/media/ssrswebportal-view.png)

![ssRSWebPortal-hidden](../reporting-services/media/ssrswebportal-hidden.png)

### <a name="power-bi-desktop-reports-and-excel-workbooks"></a>Power BI Desktop 報表與 Excel 活頁簿

您可以上傳、組織及管理 Power BI Desktop 報表和 Excel 活頁簿的權限。 它們會在入口網站中分組在一起。

![ssRSWebPortal-view-pbi-and-excel](../reporting-services/media/ssrswebportal-view-pbi-and-excel.png)

將檔案儲存於 Reporting Services 內，類似於其他資源檔案。 選取這其中一個項目，即會將它們本機下載至您的桌面上。 您可以將它們重新上傳至報表伺服器，藉以儲存所做的變更。

## <a name="search-for-items"></a>搜尋項目

您可以輸入搜尋小組，而您將會看到可存取的所有項目。 結果會分類成 KPI、報表、資料集，以及其他項目。 您可以與結果互動，並將它們加到我的最愛。

![ssRSWebPortal-Search](../reporting-services/media/ssrswebportal-search.png)

## <a name="web-portal-tasks"></a>入口網站工作

[建立入口網站品牌形象](../reporting-services/branding-the-web-portal.md)

[使用 KPI](../reporting-services/working-with-kpis-in-reporting-services.md)

[使用共用資料集](../reporting-services/work-with-shared-datasets-web-portal.md)

## <a name="see-also"></a>另請參閱

[使用 SQL Server 行動報表發行工具建立行動報表](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
[設定 URL (SSRS 組態管理員)](../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
[Reporting Services 工具](../reporting-services/tools/reporting-services-tools.md)  
[規劃 Reporting Services 瀏覽器支援](../reporting-services/browser-support-for-reporting-services-and-power-view.md)  
[SQL Server 2016 版本所支援的 Reporting Services 功能](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)  

更多問題嗎？ [試試 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
