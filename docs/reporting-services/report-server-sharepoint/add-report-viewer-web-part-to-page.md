---
title: 將 SQL Server Reporting Services 報表檢視器網頁組件新增至 SharePoint 頁面 | Microsoft Docs
ms.date: 11/26/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7a101278bed81bf1c901cf22d25d82f46e8c94e7
ms.sourcegitcommit: 49082f9b6b3bc8aaf9ea3f8557f40c9f1b6f3b0b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2020
ms.locfileid: "77256726"
---
# <a name="add-sql-server-reporting-services-report-viewer-web-part-to-a-sharepoint-page"></a>將 SQL Server Reporting Services 報表檢視器網頁組件新增至 SharePoint 頁面

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)]  [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-and-later](../../includes/ssrs-appliesto-sharepoint-2013-and-later.md)] [!INCLUDE[ssrs-appliesto-not-sharepoint-online](../../includes/ssrs-appliesto-not-sharepoint-online.md)]

將報表檢視器網頁組件新增至 SharePoint 網頁，從 SQL Server Reporting Services 或 Power BI 報表伺服器顯示報表。

![SharePoint 頁面上的報表檢視器網頁組件](media/sharepoint-report-viewer-web-part-on-page.png)

## <a name="prerequisites"></a>Prerequisites

* 為順利載入報表，必須設定對 Windows Token 服務的宣告 (C2WTS) 以進行 Kerberos 限制委派。 如需如何設定 C2WTS 的詳細資訊，請參閱[對 Windows Token 服務的宣告 (c2WTS) 和 Reporting Services](../install-windows/claims-to-windows-token-service-c2wts-and-reporting-services.md)。

* 報表檢視器網頁組件必須部署到 SharePoint 伺服器陣列。 如需如何部署報表檢視器網頁組件解決方案專案的資訊，請參閱[在 SharePoint 網站上部署報表檢視器網頁組件](deploy-report-viewer-web-part.md)。

* 若要將網頁組件新增至網頁，您必須在網站層級，擁有「新增並自訂頁面」權限。 如果您要使用預設的安全性設定，此權限會授與具備「完整控制」等級之權限的**擁有者**群組成員。

## <a name="add-web-part"></a>新增網頁組件

1. 在 SharePoint 網站中，選取左上方的**齒輪**圖示，然後選取 [新增頁面]  。

    ![從齒輪圖示將頁面新增至 Sharepoint 網站。](media/sharepoint-add-a-page.png)

2. 提供頁面名稱並選取 [建立]  。

3. 在頁面的設計工具中，選取功能區中的 [插入]  索引標籤。 然後在 [組件]  區段內選取 [網頁組件]  。

    ![從 Office 功能區中插入網頁組件。](media/sharepoint-insert-web-part.png)

4. 在 [類別目錄]  下選取 [SQL Server Reporting Services (原生模式)]**。 選取 [組件]  下的 [報表檢視器]  。 然後選取 [新增]  。

    ![新增報表檢視器網頁組件。](media/sharepoint-report-viewer-web-part.png)

    您可能在一開始就看到錯誤。 之所以會出現錯誤，是因為預設報表伺服器的 URL 設定為 *https://localhost* ，而該位置可能無法取得報表伺服器。

## <a name="configure-the-report-viewer-web-part"></a>設定報表檢視器網頁組件

若要設定網頁組件指向特定報表，請執行下列步驟。

1. 編輯 SharePoint 頁面時，請選取網頁組件右上角的向下箭號，然後選取 [編輯網頁組件]  。

    ![從 [網頁組件] 下拉式清單編輯網頁。](media/sharepoint-edit-web-part.png)

2. 請輸入裝載報表之報表伺服器的**報表伺服器 URL**。 URL 看起來應該類似 *https://myrsserver/reportserver* 。

3. 輸入您想要在網頁組件內顯示的報表名稱與路徑。 它看起來會類似 */AdventureWorks Sample Reports/Company Sales*。 在此範例中，報表 *Company Sales* 位在 *AdventureWorks 範例報表*資料夾中。

4. 如果您的報表需要參數，請在提供報表伺服器 URL 及報表名稱後，選取 [參數]  區段內的 [載入參數]  。

5. 選取 [確定]  儲存網頁組件設定的變更。

6. 在 Office 功能區中選取 [儲存]  ，儲存 SharePoint 頁面的變更。

![SharePoint 頁面上的報表檢視器網頁組件](media/sharepoint-report-viewer-web-part-on-page.png)

## <a name="considerations-and-limitations"></a>考量與限制

* 報表檢視器網頁組件不能用在 SharePoint 的現代網頁中。
* Power BI 報表不能搭配報表檢視器網頁組件使用。
* 如未看到報表檢視器網頁組件新增至網頁，請確定您已[部署報表檢視器網頁組件](deploy-report-viewer-web-part.md)。

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
