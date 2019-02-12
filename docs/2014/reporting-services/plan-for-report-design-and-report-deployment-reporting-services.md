---
title: 規劃報表設計與報表部署 (Reporting Services 2014) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 1c1e265e-52a2-4de3-96fd-ca4abae01c02
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 59b1574f7c302a5cf3adc3bee04881eefd176080
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56032009"
---
# <a name="plan-for-report-design-and-report-deployment-reporting-services-2014"></a>規劃報表設計與報表部署 (Reporting Services 2014)
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 提供了數種撰寫與部署報表。 您可以使用本主題來協助針對一起運作的報表撰寫環境和報表伺服器進行規劃。 本主題為 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 元件支援之報表定義的概觀。 報表定義是以報表定義語言 (RDL) 或用戶端報表定義語言 (RDLC) 撰寫的 XML 檔案。 每個報表定義都符合列於檔案開頭的特定結構描述版本。  
  
 RDL 檔案是利用報表產生器 3.0 於 [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] 專案的報表設計師中撰寫。 RDLC 檔案則是使用包含在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]中的 ReportViewer 控制項撰寫。  
  
 本主題內容：  
  
-   [RDL 結構描述版本](#bkmk_rdl_schema_versions)  
  
-   [報表伺服器與 RDL 結構描述支援](#bkmk_report_server_rdl_schema_support)  
  
-   [報表撰寫與報表部署支援](#bkmk_report_authoring_and_deployment)  
  
-   [ReportViewer 控制項](#bkmk_reportviewer)  
  
##  <a name="bkmk_rdl_schema_versions"></a> RDL 結構描述版本  
 下表列出本主題其餘部分所使用的每個可用結構描述版本與縮寫：  
  
|縮寫|結構描述版本|  
|------------------|--------------------|  
|2010 RDL|https://schemas.microsoft.com/sqlserver/reporting/2010/01/reportdefinition|  
|2008 RDL|https://schemas.microsoft.com/sqlserver/reporting/2008/01/reportdefinition|  
|2005 RDL<br /><br /> 2005 RDLC|https://schemas.microsoft.com/sqlserver/reporting/2005/01/reportdefinition|  
|2000 RDL|https://schemas.microsoft.com/sqlserver/reporting/2003/10/reportdefinition|  
  
 如需有關 RDL 和 RDL 結構描述的詳細資訊，請參閱下列主題：  
  
-   [Microsoft SQL Server XML 結構描述](https://go.microsoft.com/fwlink/?LinkId=31850)  
  
-   [報表定義語言規格](https://go.microsoft.com/fwlink/?linkid=116865)  
  
-   [報表定義語言 &#40;SSRS&#41;](reports/report-definition-language-ssrs.md)  
  
 如需 ReportViewer 控制項的詳細資訊，請參閱 [ReportViewer 控制項 (Visual Studio)](https://msdn.microsoft.com/library/ms251671.aspx)。  
  
##  <a name="bkmk_report_server_rdl_schema_support"></a> 報表伺服器與 RDL 結構描述支援  
 報表定義檔案可以透過下列方式部署至 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 報表伺服器：  
  
-   **報表設計工具：** 將報表從報表設計師部署到 [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] 中。  
  
-   **報表產生器：** 從報表產生器中將報表儲存至報表伺服器。  
  
-   **報表管理員：** 從報表管理員中將報表上傳至原生模式報表伺服器。  
  
-   **SharePoint:** 將報表上傳至以 SharePoint 模式報表伺服器設定的 SharePoint 網站。  
  
-   **以程式設計的方式：** 使用 SOAP API 介面，以程式設計的方式將報表發行至報表伺服器。 如需詳細資訊，請參閱 [Report Server Web Service](report-server-web-service/report-server-web-service.md)。  
  
 下表依照報表伺服器的版本列出支援的 rdl 結構描述版本。  
  
|報表伺服器版本|RDL 結構描述版本|  
|---------------------------|------------------------|  
|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]<br /><br /> 或<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]<br /><br /> 或<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|2010 RDL<br /><br /> 2008 RDL<br /><br /> 2005 RDL<br /><br /> 2000 RDL|  
|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|2008 RDL<br /><br /> 2005 RDL<br /><br /> 2000 RDL|  
|[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]|2005 RDL<br /><br /> 2000 RDL|  
  
 當您將報表定義上傳至報表伺服器，或升級包含現有報表的報表伺服器時，報表伺服器會以原始格式保留報表定義。 **第一次使用時**，報表伺服器會將報表伺服器資料庫中的報表升級為二進位格式，而這個格式在後續檢視時都會保留著。 報表定義 (.rdl) 本身不會升級。  
  
 您可以從報表伺服器擷取報表定義檔案 (.rdl) 的唯讀複本。 在原生模式報表伺服器上，瀏覽至報表管理員，然後選取報表並按一下 **[下載]**。 在 SharePoint 模式部署中，瀏覽至文件庫，然後選取報表並按一下 **[下載複本]**。  
  
 若要升級報表定義，您必須在報表撰寫環境下開啟報表，然後儲存報表。  
  
 如需所支援之報表升級與結構描述版本的詳細資訊，請參閱 [升級報表](install-windows/upgrade-reports.md)。  
  
##  <a name="bkmk_report_authoring_and_deployment"></a> 報表撰寫與報表部署支援  
 報表撰寫環境是指 [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] 專案中的報表設計師，以及報表產生器。 報表撰寫環境為報表升級、報表設計、本機模式下的報表預覽、報表伺服器上的報表預覽，以及報表部署提供各種支援。  
  
 下表摘要說明撰寫與部署不同結構描述版本之報表定義的支援：  
  
|撰寫環境|撰寫的 RDL 版本|部署 RDL 版本|部署到報表伺服器版本|  
|---------------------------|--------------------------|------------------------|--------------------------------------|  
|SQL Server 2014 Data Tools 中的報表設計師 - Business Intelligence for Microsoft Visual Studio 2012，於 Microsoft 下載中心上。<br /><br /> 或<br /><br /> SQL Server 2012 Data Tools 中的報表設計師 - Business Intelligence for Microsoft Visual Studio 2012，於 Microsoft 下載中心上。<br /><br /> 或<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Data Tools 中的報表設計師，包含在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]中。|撰寫 2010 RDL。 開啟現有的 RDL 時：<br /><br /> 2000 RDL，升級至 2010 RDL<br /><br /> 2005 RDL，升級至 2010 RDL<br /><br /> 2008 RDL，升級至 2010 RDL|2008 RDL<br /><br /> 2010 RDL|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] Business Intelligence Development Studio 中的報表設計師|撰寫 2010 RDL。 開啟現有的 RDL 時：<br /><br /> 2000 RDL，升級至 2010 RDL<br /><br /> 2005 RDL，升級至 2010 RDL<br /><br /> 2008 RDL，升級至 2010 RDL|2008 RDL<br /><br /> 2010 RDL|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Business Intelligence Development Studio 中的報表設計師|撰寫 2008 RDL。 開啟現有的 RDL 時：<br /><br /> 2000 RDL，升級至 2008 RDL<br /><br /> 2005 RDL，升級至 2008 RDL|2008 RDL|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|  
|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 報表產生器|撰寫 2010 RDL。 開啟現有的 RDL 時：<br /><br /> 2000 RDL，升級至 2010 RDL<br /><br /> 2005 RDL，升級至 2010 RDL<br /><br /> 2008 RDL，升級至 2010 RDL|2010 RDL|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|  
|Visual Studio RDLC 報表設計師|2005 RDLC|N/A|N/A|  
  
 如需 [!INCLUDE[ss_dtbi_vs2013](../includes/ss-dtbi-vs2013-md.md)]的詳細資訊，請參閱下列主題：  
  
-   [SQL Server Data Tools 中的部署和版本支援 &#40;SSRS&#41;](tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)  
  
-   [Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843)。  
  
##  <a name="bkmk_reportviewer"></a> ReportViewer 控制項  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ReportViewer 控制項可採用本機預覽模式或遠端模式顯示 .rdlc 報表，此控制項可以顯示 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 報表伺服器上裝載的 .rdl 檔案。 下表提供 ReportViewer 控制項所支援、用於本機處理 (.rdlc) 的 RDL 版本清單。 伺服器端 RDL 支援的摘要在此節中 [報表伺服器與 RDL 結構描述支援](#bkmk_report_server_rdl_schema_support)。  
  
|產品中的 ReportViewer 控制項|用於本機預覽的 RDL 版本|  
|-------------------------------------|--------------------------------------|  
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2013<br /><br /> 或<br /><br /> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2012<br /><br /> 或<br /><br /> [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]|2008 RDL|  
|[!INCLUDE[vsprvslong](../includes/vsprvslong-md.md)]<br /><br /> 或<br /><br /> [!INCLUDE[vsOrcas](../includes/vsorcas-md.md)]|2005 RDL|  
  
 如需詳細資訊，請參閱下列內容：  
  
-   [將 RDLC 檔案轉換成 RDL 檔案](https://msdn.microsoft.com/library/ms252109.aspx)  
  
-   [ReportViewer 控制項 (Visual Studio)](https://msdn.microsoft.com/library/ms251671.aspx)  
  
-   [加入和設定 ReportViewer 控制項](https://msdn.microsoft.com/library/ms252104.aspx)  
  
## <a name="see-also"></a>另請參閱  
 [報表、報表組件和報表定義 &#40;報表產生器及 SSRS&#41;](report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [Reporting Services 工具](tools/reporting-services-tools.md)   
 [報表定義語言 &#40;SSRS&#41;](reports/report-definition-language-ssrs.md)  
  
  
