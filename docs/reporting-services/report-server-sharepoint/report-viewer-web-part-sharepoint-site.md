---
title: "報表檢視器 web 組件在 SharePoint 網站上的 |Microsoft 文件"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: a37ed5efe7c365c601deb95d9fe761d227e7021e
ms.contentlocale: zh-tw
ms.lasthandoff: 10/06/2017

---
# <a name="report-viewer-web-part-on-a-sharepoint-site"></a>報表檢視器 web 組件在 SharePoint 網站上

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

報表檢視器 web 組件是自訂的 web 組件。 您可以使用 web 組件來檢視、 導覽、 列印和匯出在 SharePoint 網站內的報表伺服器上的報表。 報表檢視器 web 組件都與 Microsoft SQL Server Reporting Services 報表伺服器所處理的報表定義 (.rdl) 檔案。 

最新的報表檢視器 web 組件也可以部署到 Power BI 報表伺服器的服務編頁報表。 Web 組件不適用於 Power BI 報表中。

## <a name="why-the-report-viewer-web-part-is-re-introduced"></a>報表檢視器 web 組件會重新引進的原因

報表檢視器 web 組件，無法做為 Reporting Services 增益集適用於 SharePoint 產品的一部分。 Web 組件已針對報表伺服器以 SharePoint 整合模式。 SQL Server 2016 之後，SharePoint 整合的模式已被取代。

從 SQL Server 2017 開始，沒有一個 Reporting services 的安裝模式：**原生模式**。 您可以將所有的報表類型，使用 網頁檢視器 web 組件使用內嵌*rs： 內嵌 = true* URL 參數。 將報表內嵌到 SharePoint 頁面會要求客戶和更新的報表檢視器 web 組件整合劇本可讓此案例中的分頁報表。

網頁檢視器 web 組件便已足夠分頁的報表內嵌到 SharePoint 頁面上，而更新的報表檢視器 web 組件會提供額外的功能。

* 顯示/隱藏特定工具列按鈕
* 覆寫報表參數值
* 連接到報表參數的篩選 web 組件

## <a name="download-the-report-viewer-web-part-solution-package"></a>下載報表檢視器 web 組件的方案套件

Microsoft Download Center 上可用的報表檢視器 web 組件。

[下載報表檢視器 web 組件的方案套件](https://www.microsoft.com/download/details.aspx?id=55949)

## <a name="considerations-and-limitations"></a>考量與限制

列出的項目僅適用於更新的報表檢視器 web 組件。

* Web 組件可以只用於*傳統*SharePoint 頁面。
* 唯一的分頁 (RDL) 報表內嵌在報表檢視器 web 組件的支援。 如果您想要內嵌 Power BI 報表或行動報表，您可以使用*rs： 內嵌 = true* URL 參數。

## <a name="next-steps"></a>後續的步驟

若要開始使用更新的報表檢視器 web 組件，請參閱[部署 SharePoint 網站上的報表檢視器 web 組件](deploy-report-viewer-web-part.md)。

