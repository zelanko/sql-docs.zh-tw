---
title: Reporting Services (SSRS) | Microsoft Docs
description: "深入了解行動和分頁 Reporting Services 報表及內部部署 Power BI 報表的工具與服務。"
ms.custom: 
ms.date: 07/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- reports [Reporting Services]
- SSRS
- reports [Reporting Services], about reports
- Reporting Services
- SQL Server Reporting Services
ms.assetid: b8d18d3d-9db0-43e7-8286-7b46cc3a37ed
caps.latest.revision: "70"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Active
ms.openlocfilehash: 85377a9d96bbaa8d7d94dacafc0989d3089ff7dd
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="what-is-sql-server-reporting-services-ssrs"></a>什麼是 SQL Server Reporting Services (SSRS)？

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../includes/ssrs-previous-versions.md)]

在內部部署建立、部署和管理行動和分頁 Reporting Services 報表及 Power BI 報表等工作，都可使用 SQL Server Reporting Services (SSRS) 和 Power BI 提供齊全的現成工具與服務來完成。

![SQL Server Reporting Services 全部整合](../reporting-services/media/ss-reporting-services-all-together.png "SQL Server Reporting Services 全部整合")

## <a name="create-deploy-and-manage-mobile-and-paginated-reports"></a>建立、部署和管理行動及分頁報表

SQL Server Reporting Services 是客戶可在自己的內部部署的解決方案，以便建立、發行和管理報表，然後以不同的方式將報表提供給正確的使用者，而不論使用者是在其行動裝置上的網頁瀏覽器中檢視報表，還是將報表當做 [收件匣] 中的電子郵件進行檢視。

SQL Server 2016 版的 Reporting Services 提供更新產品套件：

* **「傳統」分頁報表** 已經過更新，因此您可以建立具有現代化外觀的報表，並提供更新工具和新功能來建立這些報表。
* **新的行動報表** 具有可配合不同裝置和不同保留方式調整的回應式配置。
* 您可以在任何新式瀏覽器中檢視的**新式入口網站** 。 在新的入口網站，您可以組織並顯示行動和分頁的 Reporting Services 報表和 KPI，加上 Power BI Desktop 報表。 您也可以在入口網站上儲存 Excel 活頁簿。

請繼續閱讀以深入了解各項內容。

> [!NOTE]
> 尋找 Power BI 報表伺服器嗎？ 請參閱[開始使用 Power BI 報表伺服器](https://powerbi.microsoft.com/documentation/reportserver-get-started/)。

### <a name="whats-new-in-reporting-services"></a>Reporting Services 的新功能

這些資訊來源可讓您持續掌握最新的 SQL Server 2016 Reporting Services 新功能。

* [Reporting Services 的新功能](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)
* [SQL Server Reporting Services 小組部落格](https://blogs.msdn.microsoft.com/sqlrsteamblog/)
* [Guy in a Cube YouTube 頻道](https://www.youtube.com/channel/UCFp1vaKzpfvoGai0vE5VJ0w)

## <a name="paginated-reports"></a>分頁報表

![ssrs-paginated-reports](../reporting-services/media/ssrs-paginated-reports.png)

Reporting Services 與「傳統」分頁文件樣式報表相關聯，您擁有的資料愈多，資料表中的資料列愈多，而且報表會有愈多頁面。 這適合用來產生針對列印最佳化之固定式配置、像素完美的文件，例如 PDF 和 Word 檔案。

該核心 BI 工作負載至今仍然存在，因此我們已將它現代化。 您現在可以使用[報表產生器](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)或 [SQL Server Data Tools (SSDT) 中的報表設計師](../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)，建立具有現代化外觀和更新功能的報表。

* 我們已更新所有預設樣式和調色盤，因此根據預設，您可以使用新的極簡現代樣式來建立報表。
* 我們已更新 [參數] 窗格，因此您可以視需要排列參數。
* 您可以匯出成新的格式，例如 PowerPoint。 PowerPoint 中的 Reporting Services 視覺效果為即時且可供編輯，而不只是螢幕擷取畫面。
* 您可以建立混合式 Power BI/Reporting Services 體驗︰您可以從這些報表將視覺效果釘選到您的 Power BI 儀表板，而不需要在 Power BI 中重新建立內部部署 Reporting Services 報表。 然後您可以在 Power BI 儀表板上集中監視所有項目。

## <a name="mobile-reports"></a>行動報表

![ssrs-mobile-reports](../reporting-services/media/ssrs-mobile-reports.png)

行動運算改變了我們需要使用的裝置，這表示今日的使用者有不同的報告需求。 當您採用平板電腦和手機時，並不適合使用固定式配置報表體驗。 針對寬螢幕電腦所設計的內容並不適合用於小型手機螢幕，此螢幕不僅更小，而且還有直向或橫向。

針對這些各式各樣的螢幕板型規格，您需要的不是固定式配置，而是可配合這些不同裝置和不同保留方式調整的回應式配置。 我們為此新增了一個報表類型，那就是行動報表；該報表是以我們約在一年前整合到產品的 Datazen 技術為基礎。 您可以使用 [SQL Server Migration Assistant for Datazen](https://www.microsoft.com/download/details.aspx?id=53128)，將現有的 Datazen 報表移轉至 Reporting Services。 

您可以在新的 [行動報表發行工具](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md) 應用程式中建立這些行動報表。 接著在適用於 Windows 10、iOS、Android 和 HTML5 之 [行動裝置的原生 Power BI 應用程式](https://powerbi.microsoft.com/documentation/powerbi-power-bi-apps-for-mobile-devices/) 中，您可以存取 Power BI 中的雲端資料，以及您的內部部署 SQL Server 2016 Reporting Services 資料。 當您建立視覺效果時，行動報表發行工具會自動為每個視覺效果產生範例資料，因此您會看到資料的視覺效果，並了解每種視覺效果適用的資料類型。

## <a name="web-portal"></a>入口網站

![ssrs-web-portal](../reporting-services/media/ssrs-web-portal.png)

原生模式 Reporting Services 使用者的首頁，就是您可以在任何新式瀏覽器中檢視的新式入口網站。 您可以在新的入口網站上，存取所有 Reporting Services 行動和分頁報表，加上 Power BI Desktop 報表。 如需詳細資訊，請參閱 [Reporting Services 中的 Power BI 報表](../reporting-services/power-bi-reports-in-reporting-services.md)。  

您可以將自訂商標套用至您的入口網站。 而且您可以直接在入口網站中建立 KPI。 KPI 可以在瀏覽器中呈現關鍵業務指標概覽，而不必開啟報表。 

新的入口網站完全是報表管理員的重寫。 現在它是單一頁面的標準式 HTML5 應用程式，並已針對下列新式瀏覽器最佳化︰Edge、Internet Explorer 10 和 11、Chrome、Firefox、Safari，以及所有主要瀏覽器。

入口網站的內容依類型組織：Reporting Services 行動和分頁報表及 KPI，加上 Power BI Desktop 報表、Excel 活頁簿、共用資料集和共用資料來源，用為報表的建置組塊。 您可以在這裡用安全的方式，以傳統資料夾階層儲存並管理它們。 您可以標記 [我的最愛]，而且如果您具有相關角色，也可以管理內容。

您仍然可以在新的入口網站中，為報表處理進行排程、視需要存取報表，以及訂閱已發行的報表。

深入了解[入口網站 (SSRS 原生模式)](../reporting-services/web-portal-ssrs-native-mode.md)。

## <a name="reporting-services-in-sharepoint-integrated-mode"></a>SharePoint 整合模式的 Reporting Services

您可以將報表發行至 SharePoint 整合模式的 Reporting Services。 您可以為報表處理進行排程、視需要存取報表、訂閱已發行的報表，並將報表匯出至 Microsoft Excel 之類的其他應用程式。 在發行到 SharePoint 網站的報表上建立資料警示，並在報表資料變更時，接收電子郵件訊息。  

深入了解 [SharePoint 整合模式下的 Reporting Services 報表伺服器](../reporting-services/report-server-sharepoint/reporting-services-report-server-sharepoint-mode.md)。

## <a name="includessrsnoversionincludesssrsnoversion-mdmd-programming-features"></a>[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 程式設計功能

利用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 程式設計功能，讓您可以擴充和自訂報表功能，使用 API 整合或擴充自訂應用程式中的資料和報表處理。

更多 [Analysis Services 開發人員文件](../reporting-services/reporting-services-developer-documentation.md)。 

## <a name="next-steps"></a>後續步驟

* [安裝 Reporting Services](../reporting-services/install-windows/install-reporting-services.md)  
* [安裝報表產生器](../reporting-services/install-windows/install-report-builder.md)   
* [下載 SQL Server Data Tools (SSDT)](http://go.microsoft.com/fwlink/?LinkID=616714)  
* [Reporting Services 中的 Power BI 報表](../reporting-services/power-bi-reports-in-reporting-services.md)

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
