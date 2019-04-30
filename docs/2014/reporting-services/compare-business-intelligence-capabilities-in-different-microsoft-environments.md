---
title: 比較不同 Microsoft 環境中的商務智慧功能 |Microsoft Docs
ms.prod: sql-server-2014
ms.technology:
- reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 03/06/2017
ms.openlocfilehash: 13ae9380cc3f034ace5f43d83640eea665cb3b02
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267265"
---
# <a name="compare-business-intelligence-capabilities-in-different-microsoft-environments"></a>比較不同 Microsoft 環境中的商業智慧功能

Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 商業智慧可以部署在許多不同的環境，包括搭配 SharePoint Server、SharePoint Online 及 Power BI for Office 365 的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。 本主題會比較每個環境所支援的元件及功能。  
  
如需 SharePoint Server 及 SharePoint Online 之比較的詳細資訊，請參閱 [比較 SharePoint 方案及選項](http://products.office.com/SharePoint/compare-sharepoint-plans)。  
  
## <a name="author-and-manage-bi-reports-and-dashboards"></a>撰寫及管理 BI 報表及儀表板  
  
||SQL Server 2014 & SharePoint Server 2013|SharePoint Online 方案 2|Power BI for Office 365|  
|-|----------------------------------------------|------------------------------|-----------------------------|  
|BI 網站|[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 組件庫|否|Power BI 網站|  
|資料監管中心及查詢共用與管理|否|否|是 **<sup>1</sup>**|  
|Master Data Services (MDS) 與 Data Quality Services (DQS) 整合|是|否|否|  
|排程資料重新整理。|是，但並不支援包含 Power Query 資料的活頁簿。|否|是|  
|自然語言查詢 （問與答）|否|否|是 **<sup>2</sup>**|  
|預測預估|否|否|是 **<sup>3</sup>**|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 整合|是|否|否|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 整合 (多維度與表格式)|是|否|否|  
|將互動式 Power View 儀表板匯出至 PowerPoint 簡報|是|否|否|  
|瀏覽器中的儀表板撰寫|是|否|否|  
|使用量監視|是|否|是|  
|利用資料列層級安全性的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Cube|是|否|否|  
  
 **<sup>1</sup>**[了解資料管理中的資料管理人角色](https://support.office.com/Article/Understanding-the-Role-of-Data-Stewards-in-Data-Management-ae3352f3-4389-45e8-a682-7fd6edb92524?ui=en-US&rs=en-US&ad=US)和[影片：Power BI 資訊管理及資料監管中心](https://www.youtube.com/watch?v=8dHOj68ts7c)。  
  
 **<sup>2</sup>**[power BI 問與答最佳化 Power BI 活頁簿 （雲端模型）](https://powerbi.microsoft.com/nl-nl/blog/new-in-power-bi-cloud-modeling-for-q-and-a/)。  
  
 **<sup>3</sup>**  [Power View for Office 365 中的新預測功能簡介](https://blogs.msdn.com/b/powerbi/archive/2014/05/08/introducing-new-forecasting-capabilities-in-power-view-for-office-365.aspx)。  
  
## <a name="view-and-browse-bi-data-reports-and-dashboards"></a>檢視及瀏覽 BI 資料、報表與儀表板  
  
||SQL Server 2014 & SharePoint Server 2013|SharePoint Online 方案 2|Power BI for Office 365|  
|-|----------------------------------------------|------------------------------|-----------------------------|  
|在瀏覽器中檢視 Microsoft Excel 活頁簿|是，但活頁簿大小必須小於 2 GB|是，但活頁簿大小必須小於 10 GB|是，但活頁簿大小必須小於 250 GB|  
|在瀏覽器中探索 HTML5 的資料|否|否|是|  
|Mobile BI 應用程式可從遠端存取報表及儀表板|否|否|是 **<sup>1</sup>**|  
|以 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 為資料來源的 Excel 活頁簿 **<sup>2</sup>**|是|否|否|  
|可在不同瀏覽器及版本中使用這些功能|只有非 Power View 視覺效果才可以 **<sup>3</sup>**|是，但活頁簿檔案大小必須小於 10MB **<sup>3</sup>**|是 **<sup>3</sup>**|  
  
 **<sup>1</sup>**  [Microsoft Power BI](http://apps.microsoft.com/windows/app/microsoft-power-bi/b7e7c94d-2ea3-4fa6-a277-9d19a1f697ba)。  
  
 **<sup>2</sup>**  [以 PowerPivot 活頁簿為資料來源](http://blogs.technet.com/b/excel_services__powerpivot_for_sharepoint_support_blog/archive/2013/02/15/powerpivot-workbook-as-a-data-source.aspx)  
  
 **<sup>3</sup>**  [跨商業智慧 (BI) 工具的行動支援](https://msdn.microsoft.com/library/dn151146\(v=sql.110\).aspx) 及 [規劃 Reporting Services 和 Power View 瀏覽器支援 (Reporting Services 2014)](https://msdn.microsoft.com/library/ms156511.aspx)。  
  
## <a name="more-information"></a>詳細資訊  
  
- [Excel 和 Office 365 中的 BI 功能](https://support.office.com/article/BI-capabilities-in-Excel-and-Office-365-26c0548e-124c-4fd3-aab3-5f64568cb743)。  
  
- 如需使用同義字之需求的詳細資訊，請參閱[最佳化的 Power BI 問與答的同義字片語與](https://blog.pragmaticworks.com/optimizing-power-bi-qa-with-synonyms-phrasing-using-cloud-modeling)pragmaticworks.com 在。  
  
- [Office Online，挑選您公司的社交網路：Yammer 或新聞摘要？](https://support.office.com/article/Pick-your-enterprise-social-network-Yammer-or-Newsfeed-21954c85-4384-47d4-96c2-dfa1c9d56e66?ui=en-US&rs=en-US&ad=US).  
  
- [Power BI for Office 365](https://www.microsoft.com/powerbi/default.aspx)。  
  
- [Power BI 定價](https://www.microsoft.com/powerBI/pricing.aspx).  
  
- [分析和報告使用 Microsoft 商務智慧 (BI) 工具](../reporting-services/choosing-microsoft-business-intelligence-bi-tools-for-analysis-and-reporting.md)  
  
## <a name="community-content"></a>社群內容

[比較內部部署與雲端上的 Microsoft 自助 BI](http://businessintelligist.com/2014/02/07/microsoft-self-service-bi-on-premise-vs-could/)。