---
title: 比較報表檢視器中的本機模式與連線模式報表 | Microsoft Docs
description: SQL Server Reporting Services 報表可設定為在本機模式或連線模式中執行。 了解不同的模式。
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: d21d06182f259451f53fed45ba77a5cbacbb382d
ms.sourcegitcommit: 66a0672e47415dbd5cfd8d19075102c8c3973e70
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2020
ms.locfileid: "83766992"
---
# <a name="local-mode-vs-connected-mode-reports-in-the-report-viewer"></a>比較報表檢視器中的本機模式與連線模式報表

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表可以設定為在 *「本機模式」* 或 *「連接模式」* 中執行，以運用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器。 而是，當資料延伸模組支援本機模式報表時，您可以使用報表檢視器直接從 SharePoint 轉譯報表。 這種方法稱為 *「本機模式」* (Local Mode)。 在舊版 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，SharePoint 伺服器陣列需要連接到 SharePoint 模式中所設定的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器，以便讓報表檢視器控制項能夠呈現報表。 此方法稱為 *「遠端模式」* (Remote Mode) 或 *「連接模式」* (Connected Mode)。  

> [!NOTE]
> SQL Server 2016 後即不再提供 Reporting Services 與 SharePoint 的整合。

 在 *本機模式* 中，沒有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器。 您必須安裝 SharePoint 產品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集，但不需要 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器。 在本機模式中，使用者可以檢視報表，但是無法存取伺服器端的功能 (例如訂閱和資料警示)。  

## <a name="local-mode-vs-connected-mode-and-supported-extensions"></a>本機模式與連接模式及支援的延伸模組

 **本機模式：** 當您具有支援本機模式的資料延伸模組時，報表檢視器會直接從 SharePoint 呈現報表。 在 *本機模式* 中，沒有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器。 您必須安裝 SharePoint 產品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集，但不需要 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器。 在本機模式中，使用者可以檢視報表，但是 **無法** 存取伺服器端的功能 (例如，訂閱和資料警示)。  
  
 **連接模式**也稱為 *「遠端模式」* ，會要求 SharePoint 模式下的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器，連接到 SharePoint 伺服器陣列，讓報表檢視器控制項可以呈現報表。  
  
 下面是支援本機模式報表的資料處理延伸模組清單：  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Access 2010 報表延伸模組。 如需 Access Services 的詳細資訊，請參閱 [將 Access Services 與 SQL Reporting Services 配合使用：安裝 SQL Server 2008 R2 Reporting Services 增益集 (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=192686)。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 清單資料延伸模組。 如需 SharePoint 清單資料延伸模組的詳細資訊，請參閱 [Reporting Services &#40;SSRS&#41; 支援的資料來源](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)  
  
 您也可以部署自訂資料處理延伸模組來支援本機模式。 如需詳細資訊，請參閱＜ [Implementing a Data Processing Extension](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)＞。  
  
 本機模式支援轉譯具有 .rsds 檔案中之內嵌資料來源或共用資料來源的報表。 不過，您無法管理報表或其相關聯的資料來源。 如果您嘗試這樣做，將會收到在本機模式不支援這項動作的錯誤。 在 SharePoint 網站中管理資料來源，只有在連接模式下才支援。  
  
> [!NOTE]  
>  就如同舊版一樣，您無法在 .rsds 檔案中內嵌使用者名稱及密碼。  
  
## <a name="configure-local-mode-and-access-services-with-sharepoint-2013"></a>設定 SharePoint 2013 的本機模式和 Access Services

 您可以設定 SharePoint 2013 伺服器陣列支援現有 Access 2010 Web 資料庫和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本機模式。 如需詳細資訊，請參閱 [安裝及設定 SharePoint Server 2013 中 Web 資料庫的 Access Services 2010](https://technet.microsoft.com/library/ee748653\(office.15\).aspx)。  
  
 您無法為 SharePoint 2013 建立新的 Access Web 資料庫。 Access 2013 會使用您在 Access 中建立的新資料庫類型 *Access Web App* ，然後在 Web 瀏覽器中做為 SharePoint 應用程式使用並與其他人共用。  
  
 如需詳細資訊，請參閱下列內容。  
  
-   [Access 2013 的新功能](https://office.microsoft.com/access-help/what-s-new-in-access-2013-HA102809500.aspx) (https://office.microsoft.com/access-help/what-s-new-in-access-2013-HA102809500.aspx) 。  
  
-   [Access 應用程式的基本工作](https://office.microsoft.com/access-help/basic-tasks-for-an-access-app-HA102840210.aspx?CTT=5&origin=HA102809500) (https://office.microsoft.com/access-help/basic-tasks-for-an-access-app-HA102840210.aspx?CTT=5&origin=HA102809500) 。  
  
## <a name="configure-local-mode-reporting-with-sharepoint-2010"></a>設定 SharePoint 2010 的本機模式報表

 本機模式需要 ASP.NET 工作階段狀態。 安裝 Access Services 就會啟用 ASP.Net 工作階段狀態。 您也可以使用 PowerShell 來啟用。  
  
1.  開啟 SharePoint 2010 管理命令介面。  
  
2.  輸入以下命令：  
  
    ```  
    - Enable-SPSessionStateService  
    ```  
  
3.  出現提示時，請輸入資料庫的名稱。  
  
4.  執行 IIS 重設。  
  
 如需詳細資訊，請參閱 [將 Access Services 與 SQL Reporting Services 配合使用：安裝 SQL Server 2008 R2 Reporting Services 增益集 (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=192686) 和 [Enable-SPSessionStateService](https://technet.microsoft.com/library/ff607857\(v=office.15\).aspx)。  
  
## <a name="connected-mode"></a>連線模式

 如需 ADS 延伸模組與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 連線模式搭配使用的最新資訊，請參閱 [Access Services Report in SharePoint Site shows error in data extension 'ADS'](https://social.technet.microsoft.com/wiki/contents/articles/25298.access-services-report-in-sharepoint-site-shows-error-in-data-extension-ads.aspx) (SharePoint 網站中 Access Services 報表顯示資料延伸模組 'ADS' 中的錯誤)。  
  
## <a name="see-also"></a>另請參閱

 [Reporting Services 支援的資料來源](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
