---
title: SharePoint 網站上的報表檢視器網頁組件 - SSRS | Microsoft Docs
ms.date: 11/15/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 882dafee6997f4e0a140872847cfa2fdc1109f05
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580570"
---
# <a name="report-viewer-web-part-on-a-sharepoint-site---reporting-services"></a>SharePoint 網站上的報表檢視器網頁組件 - Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)]  [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2016-2019](../../includes/ssrs-appliesto-sharepoint-2016-2019.md)] [!INCLUDE[ssrs-appliesto-not-sharepoint-online](../../includes/ssrs-appliesto-not-sharepoint-online.md)]

報表檢視器網頁組件是自訂的網頁組件。 您可以在 SharePoint 網站內的報表伺服器上，使用網頁組件來檢視、巡覽、列印與匯出報表。 報表檢視器網頁組件與 Microsoft SQL Server Reporting Services 報表伺服器所處理的報表定義 (.rdl) 檔建立關聯。 

最新的報表檢視器網頁組件也提供可以部署到 Power BI 報表伺服器的分頁報表。 網頁組件不適用於 Power BI 報表。

## <a name="why-the-report-viewer-web-part-is-re-introduced"></a>重新推出報表檢視器網頁組件的原因

報表檢視器網頁組件以前是適用於 SharePoint 產品的 Reporting Services 增益集的一部分。 網頁組件以前專門針對 SharePoint 整合模式中的報表伺服器。 SQL Server 2016 之後已取代 SharePoint 整合模式。

從 SQL Server 2017 開始，只有一種 Reporting services 安裝模式：**原生模式**。 您可以使用 *rs:Embed=true* URL 參數，內嵌所有使用網頁檢視器網頁組件的報表類型。 將報表內嵌到 SharePoint 頁面是客戶要求的整合內容，而更新的報表檢視器網頁能針對分頁報表啟用案例。

當網頁檢視器網頁組件足以將分頁報表內嵌到 SharePoint 頁面時，更新的報表檢視器網頁組件就可以提供其他功能。

* 顯示/隱藏特定的工具列按鈕
* 覆寫報表參數值
* 將篩選網頁組件連線到報表參數

## <a name="download-the-report-viewer-web-part-solution-package"></a>下載報表檢視器網頁組件解決方案套件

Microsoft 下載中心提供報表檢視器網頁組件。

[下載報表檢視器網頁組件解決方案套件](https://www.microsoft.com/download/details.aspx?id=55949)

## <a name="considerations-and-limitations"></a>考量與限制

列出的項目僅適用於更新的報表檢視器網頁組件。

* 網頁組件僅限用於「傳統的」  SharePoint 頁面。
* 報表檢視器網頁組件只支援內嵌分頁 (RDL) 報表。 如果想要內嵌 Power BI 報表或行動報表，您可以使用 *rs:Embed=true* URL 參數。

## <a name="next-steps"></a>後續步驟

若要開始使用更新的報表檢視器網頁組件，請參閱[在 SharePoint 網站上部署報表檢視器網頁組件](deploy-report-viewer-web-part.md)。
