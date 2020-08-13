---
title: 什麼是 SQL Server Reporting Services | Microsoft Docs
description: 深入了解適用於內部部署行動和分頁 Reporting Services 報表的工具與服務。
ms.date: 05/06/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services]
- SSRS
- reports [Reporting Services], about reports
- Reporting Services
- SQL Server Reporting Services
ms.assetid: b8d18d3d-9db0-43e7-8286-7b46cc3a37ed
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e75947d7ea4b47c7c2fef3e37cfd6b5b73b48533
ms.sourcegitcommit: 4231364ab5bc15b74952ca5d20508b7ba9ca347e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/13/2020
ms.locfileid: "86291145"
---
# <a name="what-is-sql-server-reporting-services-ssrs"></a>什麼是 SQL Server Reporting Services (SSRS)？

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

尋找 Power BI 報表伺服器嗎？ 請參閱[什麼是 Power BI 報表伺服器？](https://docs.microsoft.com/power-bi/report-server/get-started)。

SQL Server Reporting Services (SSRS) 提供了一組內部部署工具和服務，可用於建立、部署及管理行動與分頁報表。

![SQL Server Reporting Services 整合一切](../reporting-services/media/ss-reporting-services-all-together.png "SQL Server Reporting Services 整合一切")

## <a name="create-deploy-and-manage-mobile-and-paginated-reports"></a>建立、部署和管理行動及分頁報表

SSRS 解決方案會以彈性方式提供正確的資訊給需要的使用者。 使用者可以透過下列方式取用報表：網頁瀏覽器、自己的行動裝置，或電子郵件。

SQL Server Reporting Services 提供更新產品套件：

* **「傳統」分頁報表**已經過更新，因此您可以建立具有現代化外觀的報表，並提供更新工具和新功能來建立這些報表。
* **新的行動報表** 具有可配合不同裝置和不同保留方式調整的回應式配置。
* 您可以在任何新式瀏覽器中檢視的**新式入口網站** 。 在新的入口網站，您可以組織並顯示行動與分頁的 Reporting Services 報表和 KPI。 您也可以在入口網站上儲存 Excel 活頁簿。

請繼續閱讀以深入了解各項內容。

### <a name="whats-new-in-reporting-services"></a>Reporting Services 的新功能

這些資訊來源可讓您持續掌握最新的 SQL Server Reporting Services 新功能。

* [Reporting Services 的新功能](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)
* [SQL Server Reporting Services 小組部落格](https://blogs.msdn.microsoft.com/sqlrsteamblog/)
* [Guy in a Cube YouTube 頻道](https://www.youtube.com/channel/UCFp1vaKzpfvoGai0vE5VJ0w)

## <a name="paginated-reports"></a>分頁報表

![ssrs-paginated-reports](../reporting-services/media/ssrs-paginated-reports.png)

Reporting Services 與「傳統」分頁報表相關聯，適用於已針對列印最佳化的固定版面配置文件，例如 PDF 和 Word 檔案。

該核心 BI 工作負載至今仍然存在，因此我們已將它現代化。 您現在可以使用報表產生器或 [SQL Server Data Tools (SSDT)](../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md) 中的報表設計師，建立具有現代化外觀和更新功能的報表。

* 我們已更新所有預設樣式和調色盤，因此根據預設，您可以使用新的極簡現代樣式來建立報表。
* 我們已更新 [參數] 窗格，因此您可以視需要排列參數。
* 您可以匯出成新的格式，例如 PowerPoint。 PowerPoint 中的 Reporting Services 視覺效果是即時且可供編輯的，而不只是螢幕擷取畫面。
* 您可以建立混合式 Power BI/Reporting Services 體驗︰您可以從這些報表將視覺效果釘選到您的 Power BI 儀表板，而不需要在 Power BI 中重新建立內部部署 Reporting Services 報表。 然後您可以在 Power BI 儀表板上集中監視所有項目。

## <a name="mobile-reports"></a>行動報表

![ssrs-mobile-reports](../reporting-services/media/ssrs-mobile-reports.png)

行動運算改變了我們需要使用的裝置，這表示今日的使用者有不同的報告需求。 當您採用平板電腦和手機時，並不適合使用固定式配置報表體驗。 針對寬螢幕電腦所設計的內容並不適合用於小型手機螢幕，此螢幕不僅更小，而且還有直向或橫向。

針對這些各式各樣的螢幕板型規格，您需要的是可配合這些不同的螢幕尺寸和顯示方向的回應式版面配置。 我們為此新增了一個報表類型，那就是行動報表；該報表是以我們約在一年前整合到產品的 Datazen 技術為基礎。 您可以使用 [SQL Server Migration Assistant for Datazen](https://www.microsoft.com/download/details.aspx?id=53128)，將現有的 Datazen 報表移轉至 Reporting Services。

您可以在新的 [行動報表發行工具](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md) 應用程式中建立這些行動報表。 接著可以在適用於 Windows 10、iOS、Android 和 HTML5 的[行動裝置適用原生 Power BI 應用程式](https://powerbi.microsoft.com/documentation/powerbi-power-bi-apps-for-mobile-devices/)中，存取您存放在 Power BI、雲端，或 SSRS 中的資料。

當您建立視覺效果時，行動報表發行工具會自動產生範例資料。 此功能可讓您看到資料的視覺效果，並了解每種視覺效果適用的資料類型。

## <a name="web-portal"></a>入口網站

![ssrs-web-portal](../reporting-services/media/ssrs-web-portal.png)

原生模式 Reporting Services 使用者的首頁，就是您可以在大部分瀏覽器中檢視的新式入口網站。 您可以在新的入口網站中存取您所有的 Reporting Services 行動裝置、分頁報表和 KPI。 KPI 可以在瀏覽器中呈現關鍵業務指標概覽，而不必開啟報表。

新的入口網站完全是報表管理員的重寫。 現在它是單一頁面的標準式 HTML5 應用程式，並已針對下列新式瀏覽器最佳化︰Microsoft Edge、Internet Explorer 10 和 11、Chrome、Firefox、Safari，以及所有主要瀏覽器。

入口網站的內容依類型組織：

* 分易報表
* 行動報表 
* KPI
* Excel 活頁簿
* 共用資料集
* 共用資料來源

您可以在這裡用安全的方式，以傳統資料夾階層儲存並管理它們。 標記您最愛的報表以便快速存取。 擁有適當權限的人員可以管理 SSRS 內容。

您仍然可以在新的入口網站中，為報表處理進行排程、視需要存取報表，以及訂閱已發行的報表。

深入了解 [入口網站](../reporting-services/web-portal-ssrs-native-mode.md)。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

## <a name="reporting-services-in-sharepoint-integrated-mode"></a>SharePoint 整合模式的 Reporting Services

您可以將報表發行至 SharePoint 整合模式的 Reporting Services。 您可以為報表處理進行排程、視需要存取報表、訂閱已發行的報表，並將報表匯出至 Microsoft Excel 之類的其他應用程式。 在發行到 SharePoint 網站的報表上建立資料警示，並在報表資料變更時，接收電子郵件訊息。  

深入了解 [SharePoint 整合模式下的 Reporting Services 報表伺服器](../reporting-services/report-server-sharepoint/reporting-services-report-server-sharepoint-mode.md)。

::: moniker-end

## <a name="ssrsnoversion-programming-features"></a>[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 程式設計功能

妥善運用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 程式設計功能，您就能夠擴充及自訂報表功能。 請使用 SSRS API 整合或擴充自訂應用程式中的資料和報表處理功能。

更多 [Analysis Services 開發人員文件](../reporting-services/reporting-services-developer-documentation.md)。

## <a name="next-steps"></a>後續步驟

* [安裝 Reporting Services](../reporting-services/install-windows/install-reporting-services.md)
* [下載 SQL Server Data Tools (SSDT)](https://go.microsoft.com/fwlink/?LinkID=616714)
* [安裝報表產生器](../reporting-services/install-windows/install-report-builder.md)

* 更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
