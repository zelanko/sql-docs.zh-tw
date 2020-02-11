---
title: SQL Server 2014 中 SQL Server Reporting Services 已被取代的功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, backward compatibility
- deprecated features [Reporting Services]
- HTML OWC rendering extension [Reporting Services]
- Report Server Web service, endpoints
ms.assetid: 3876c01e-f81d-4cce-9104-5106a8c369e6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d5cbef64cbed910018e7d2f8dae1844074aaa3f5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109346"
---
# <a name="deprecated-features-in-sql-server-reporting-services-in-sql-server-2014"></a>SQL Server 2014 中 SQL Server Reporting Services 已被取代的功能
  本主題描述已被取代的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 功能。 在此版本中仍然提供已被取代的功能，不過，這些功能排程在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]之後版本中移除。 已被取代的功能不應在新應用程式中使用。  
  
 本主題內容：  
  
-   [SQL Server 2014 Reporting Services 已淘汰的功能](#bkmk_2014)  
  
-   [SQL Server 2012 SP1 Reporting Services 已被取代的功能](#bkmk_2012sp1)  
  
-   [SQL Server 2012 Reporting Services 已淘汰的功能](#bkmk_2012)  
  
-   [SQL Server 2008 R2 Reporting Services 已被取代的功能](#bkmk_kj)  
  
##  <a name="bkmk_2014"></a>SQL Server 2014 Reporting Services 已淘汰的功能  
  
### <a name="features-not-supported-in-the-next-version-of-sql-server"></a>下一版的 SQL Server 不支援的功能  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] **下一**版的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]將不再支援下列功能。 請勿在新的開發工作中使用這些功能，並且儘速修改使用這些功能的應用程式。  
  
#### <a name="html-rendering-extension-device-information-settings"></a>HTML 轉譯延伸模組的裝置資訊設定  
 下列 HTML 轉譯延伸模組的裝置資訊設定已被取代。  
  
-   ActionScript  
  
-   ActiveXControls  
  
-   GetImage  
  
-   OnlyVisibleStyles  
  
-   ReplacementRoot  
  
-   ResourceStreamRoot  
  
-   StreamRoot  
  
-   UsePx  
  
-   縮放  
  
 如需有關 HTML 轉譯延伸模組的詳細資訊，請參閱＜ [HTML Device Information Settings](html-device-information-settings.md)＞  
  
#### <a name="microsoft-word-and-microsoft-excel-1997-2003-rendering"></a>Microsoft Word 和 Microsoft Excel 1997-2003 轉譯  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] BIFF8 轉譯延伸[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]模組會向[!INCLUDE[msCoName](../includes/msconame-md.md)] Word 和[!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 1997-2003 二進位交換檔案格式報告。 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]包含以[!INCLUDE[msCoName](../includes/msconame-md.md)] Office 2007-2010 Open XML 格式呈現的延伸模組。  
  
#### <a name="report-definition-language-rdl-2005-and-earlier"></a>報表定義語言 (RDL) 2005 和更早版本  
 報表定義語言 (RDL) 和更早版本已被取代。 如需 RDL 的詳細資訊，請參閱[報表定義語言 &#40;SSRS&#41;](reports/report-definition-language-ssrs.md)。  
  
 如需有關升級報表的詳細資訊，請參閱＜ [Upgrade Reports](install-windows/upgrade-reports.md)＞。  
  
#### <a name="sql-server-2005-and-earlier-custom-report-items"></a>SQL Server 2005 和更早版本的自訂報表項目  
 針對2005和更早版本編譯的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]自訂報表專案（CRI）已被取代。  
  
#### <a name="reporting-services-snapshots-2005-and-earlier"></a>Reporting Services Snapshots 2005 和更早版本  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]以[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005 和更早版本轉譯的快照集已被取代。  
  
#### <a name="report-models"></a>報表模型  
 語意模型語言 (SMDL) 報表模型已被取代。 雖然您可以繼續使用現有的報表模型做為報表中[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]的資料來源，但您應該考慮更新報表，以便移除它們對報表模型的相依性。  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]不包含用來建立或更新報表模型的工具。 如需詳細資訊，請參閱[SQL Server 2014 中 SQL Server Reporting Services 的重大變更](breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)。  
  
#### <a name="deprecated-methods-in-the-web-service-endpoint"></a>Web 服務端點中已被取代的方法  
 <xref:ReportService2010.ReportingService2010> Web 服務端點中的下列作業已被取代：  
  
-   <xref:ReportService2010.ReportingService2010.GetProperties%2A>  
  
-   <xref:ReportService2010.ReportingService2010.IsSSLRequired%2A>  
  
#### <a name="sharepoint-web-parts"></a>SharePoint Web 組件  
 安裝封包檔 **RSWebParts.cab** 以及可從此 cab 檔案解壓縮的 SharePoint Web 組件已被取代。 已被取代的 web 元件是報表瀏覽器（**spexplorer.dwp .dwp**）和報表檢視器（**spviewer.dwp**）。  
  
 如需已被取代之 web 元件的詳細資訊，請參閱[使用 SharePoint Web 組件查看和流覽原生模式報表（SSRS）](https://msdn.microsoft.com/library/ms159772.aspx)  
  
### <a name="features-not-supported-in-a-future-version-of-sql-server"></a>SQL Server 的未來版本不支援的功能  
 下一版的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 可支援下列 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]功能，但會在更新的版本中移除。 確實的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本尚未決定。  
  
 
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中沒有已被取代的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]功能。  
  
##  <a name="bkmk_2012sp1"></a>SQL Server 2012 SP1 Reporting Services 已淘汰的功能  
 本節描述 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中已被取代的 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]功能。 下一版的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 可支援下列 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]功能，但會在更新的版本中移除。 確實的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 版本尚未決定。  
  
### <a name="sharepoint-web-parts"></a>SharePoint Web 組件  
 安裝封包檔 **RSWebParts.cab** 以及可從此 cab 檔案解壓縮的 SharePoint Web 組件已被取代。 已被取代的 web 元件是報表瀏覽器（**spexplorer.dwp .dwp**）和報表檢視器（**spviewer.dwp**）。  
  
 如需已被取代之 web 元件的詳細資訊，請參閱[使用 SharePoint Web 組件查看和流覽原生模式報表（SSRS）](https://msdn.microsoft.com/library/ms159772.aspx)  
  
##  <a name="bkmk_2012"></a>SQL Server 2012 Reporting Services 已淘汰的功能  
 本節描述 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中已被取代的 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]功能。  
  
### <a name="html-rendering-extension-device-information-settings"></a>HTML 轉譯延伸模組的裝置資訊設定  
 下列 HTML 轉譯延伸模組的裝置資訊設定已被取代。  
  
-   ActionScript  
  
-   ActiveXControls  
  
-   GetImage  
  
-   OnlyVisibleStyles  
  
-   ReplacementRoot  
  
-   ResourceStreamRoot  
  
-   StreamRoot  
  
-   UsePx  
  
-   縮放  
  
 如需有關 HTML 轉譯延伸模組的詳細資訊，請參閱＜ [HTML Device Information Settings](html-device-information-settings.md)＞  
  
### <a name="microsoft-word-and-microsoft-excel-1997-2003-rendering"></a>Microsoft Word 和 Microsoft Excel 1997-2003 轉譯  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] BIFF8 轉譯延伸[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]模組會向[!INCLUDE[msCoName](../includes/msconame-md.md)] Word 和[!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 1997-2003 二進位交換檔案格式報告。 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]包含以[!INCLUDE[msCoName](../includes/msconame-md.md)] Office 2007-2010 Open XML 格式呈現的延伸模組。  
  
### <a name="report-definition-language-rdl-2005-and-earlier"></a>報表定義語言 (RDL) 2005 和更早版本  
 報表定義語言 (RDL) 和更早版本已被取代。 如需 RDL 的詳細資訊，請參閱[報表定義語言 &#40;SSRS&#41;](reports/report-definition-language-ssrs.md)。  
  
 如需有關升級報表的詳細資訊，請參閱＜ [Upgrade Reports](install-windows/upgrade-reports.md)＞。  
  
### <a name="sql-server-2005-and-earlier-custom-report-items"></a>SQL Server 2005 和更早版本的自訂報表項目  
 針對2005和更早版本編譯的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]自訂報表專案（CRI）已被取代。  
  
### <a name="reporting-services-snapshots-2005-and-earlier"></a>Reporting Services Snapshots 2005 和更早版本  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]以[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005 和更早版本轉譯的快照集已被取代。  
  
### <a name="report-models"></a>報表模型  
 語意模型語言 (SMDL) 報表模型已被取代。 雖然您可以繼續使用現有的報表模型做為報表中[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]的資料來源，但您應該考慮更新報表，以便移除它們對報表模型的相依性。  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]不包含用來建立或更新報表模型的工具。 如需詳細資訊，請參閱[SQL Server 2014 中 SQL Server Reporting Services 的重大變更](breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)。  
  
### <a name="deprecated-methods-in-the-web-service-endpoint"></a>Web 服務端點中已被取代的方法  
 <xref:ReportService2010.ReportingService2010> Web 服務端點中的下列作業已被取代：  
  
-   <xref:ReportService2010.ReportingService2010.GetProperties%2A>  
  
-   <xref:ReportService2010.ReportingService2010.IsSSLRequired%2A>  
  
##  <a name="bkmk_kj"></a>SQL Server 2008 R2 Reporting Services 已淘汰的功能  
  
> [!NOTE]  
>  因為 SQL Server 2008 R2 是 SQL Server 2008 的次要版本更新，所以建議您也檢閱 SQL Server 2008 章節中的內容。  
  
### <a name="report-server-web-service-endpoints"></a>報表伺服器 Web 服務端點  
 Web 服務 <xref:ReportService2005.ReportingService2005> 和 <xref:ReportService2006.ReportingService2006> 在此版本中已被取代。 這些端點已由新端點所取代：<xref:ReportService2010.ReportingService2010>。  
  
 新端點包含可在已被取代之端點中使用的所有功能，以及 SQL Server 2008 R2 中所引進的新功能。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 的新 &#40;&#41;](what-s-new-reporting-services.md)   
 [回溯相容性](../getting-started/backward-compatibility.md)   
 [SQL Server 2014 中 SQL Server Reporting Services 的行為變更](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [SQL Server 2014 中 SQL Server Reporting Services 已停止的功能](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)  
  
  
