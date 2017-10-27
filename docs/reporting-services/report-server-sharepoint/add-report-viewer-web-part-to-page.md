---
title: "將 SQL Server Reporting Services 報表檢視器 web 組件加入至 SharePoint 頁面 |Microsoft 文件"
ms.custom: Display a report, from SQL Server Reporting Services or Power BI Report Server, by adding a Report Viewer web part to a SharePoint page.
ms.date: 09/26/2017
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
ms.openlocfilehash: fbc68b6ff9f1edf5cf6ee13f6e93a3d2d1a8f834
ms.contentlocale: zh-tw
ms.lasthandoff: 10/06/2017

---

# <a name="add-sql-server-reporting-services-report-viewer-web-part-to-a-sharepoint-page"></a>將 SQL Server Reporting Services 報表檢視器 web 組件加入至 SharePoint 網頁

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

顯示報表，請從 SQL Server Reporting Services 或 Power BI 報表伺服器，將報表檢視器 web 組件加入至 SharePoint 網頁。

![在 SharePoint 網頁上的報表檢視器 web 組件](media/sharepoint-report-viewer-web-part-on-page.png)

## <a name="prerequisites"></a>必要條件

* 若要讓報表可順利載入，對 Windows Token Service (C2WTS) 必須設定 kerberos 的宣告會限制委派。 如需有關如何設定 C2WTS 的詳細資訊，請參閱[對 Windows Token Service (C2WTS) 和 Reporting Services 的宣告](../install-windows/claims-to-windows-token-service-c2wts-and-reporting-services.md)。

* 報表檢視器 web 組件必須部署在 SharePoint 伺服器陣列。 如需如何部署報表檢視器 web 組件的方案專案的資訊，請參閱[部署 SharePoint 網站上的報表檢視器 web 組件](deploy-report-viewer-web-part.md)。

* 若要將 web 組件加入至網頁，您必須新增並自訂頁面的權限在網站層級。 如果您使用預設安全性設定，此權限授與成員的**擁有者**具有完整控制權限等級的權限的群組。

## <a name="add-web-part"></a>新增網頁組件

1. 在 SharePoint 網站中，選取**齒輪**中左上方和選取圖示**加入頁面**。

    ![加入至 sharepoint 網站的頁面，從齒輪圖示。](media/sharepoint-add-a-page.png)

2. 提供您的頁面名稱，然後選取**建立**。

3. 在頁面的設計工具中，選取**插入**功能區中的索引標籤。 然後選取**web 組件**內**部分**> 一節。

    ![從 office 功能區中插入 web 組件。](media/sharepoint-insert-web-part.png)

4. 在下**類別**，請選取 * * SQL Server Reporting Services （原生模式）。 在下**部分**，選取**報表檢視器**。 然後選取**新增**。

    ![加入報表檢視器 web 組件。](media/sharepoint-report-viewer-web-part.png)

    這一開始可能會出現錯誤。 錯誤是因為預設報表伺服器 URL 設定為*http://localhost*而且可能無法在該位置。

## <a name="configure-the-report-viewer-web-part"></a>設定報表檢視器 web 組件

若要設定網頁組件，以指向特定的報表，請執行下列項目。

1. 編輯 SharePoint 網頁時，選取右上角的 web 組件中的向下箭號，然後選取**編輯網頁組件**。

    ![從 web 組件下拉式清單的編輯 web 網頁。](media/sharepoint-edit-web-part.png)

2. 輸入**報表伺服器 URL**裝載報表的報表伺服器。 這看起來應該類似*http://myrsserver/reportserver*。

3. 輸入您想要在 web 組件內顯示的報表的名稱與路徑。 這看起來類似*AdventureWorks Sample Reports/Company Sales*。 在此範例中，報表*Company Sales*處於資料夾，稱為*AdventureWorks 範例報表*。

4. 如果您的報表需要參數，您必須提供報表伺服器 URL 及報表的名稱之後，選取**載入參數**內**參數**> 一節。

5. 選取**確定**儲存至 web 組件組態的變更。

6. 選取**儲存**，在 Office 功能區中，將變更儲存至 SharePoint 頁面。

![在 SharePoint 網頁上的報表檢視器 web 組件](media/sharepoint-report-viewer-web-part-on-page.png)

## <a name="considerations-and-limitations"></a>考量與限制

* 報表檢視器 web 組件不能在 SharePoint 中的現代網頁。
* Power BI 報表不能與報表檢視器 web 組件。
* 如果您沒有看到報表檢視器 web 組件，加入您的網頁，請確定您有[部署報表檢視器 web 組件](deploy-report-viewer-web-part.md)。

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)

