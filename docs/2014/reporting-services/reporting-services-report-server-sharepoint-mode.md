---
title: Reporting Services 報表伺服器 (SharePoint 模式) | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: c89596d916f9a8ec2fea91cdea8f72b1958c5b6c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102830"
---
# <a name="reporting-services-report-server-sharepoint-mode"></a>Reporting Services 報表伺服器 (SharePoint 模式)

為 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式 **設定的** 報表伺服器可以在 SharePoint 產品部署內執行。 SharePoint 模式的報表伺服器可以針對報表和其他 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 內容類型使用 SharePoint 的共同作業和管理功能。 SharePoint 模式需要在 SharePoint Web 前端安裝適用於 SharePoint 產品的正確 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 增益集版本。  
  
如需有關安裝及設定的詳細資訊，請參閱以下主題：  
  
- [安裝適用於 SharePoint 2013 的 Reporting Services SharePoint 模式](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)  
  
- [Install Reporting Services SharePoint Mode for SharePoint 2010](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)。  
  
- [將其他報表伺服器加入至伺服陣列&#40;SSRS 向外延展&#41;](install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)。  
  
 如需本版新功能的資訊，請參閱 'SharePoint' 一節[What's New &#40;Reporting Services&#41;](../../2014/reporting-services/what-s-new-reporting-services.md)。  
  
 **本主題內容：**  
  
-   [功能摘要](#bkmk_featuresum)  
  
-   [連接模式與本機模式](#bkmk_connectedandlocal)  
  
-   [不支援的 SharePoint 功能](#bkmk_unsupportedsharepoint)  
  
-   [支援的 SharePoint 增益集與報表伺服器組合](#bkmk_supportedcombinations)  
  
-   [提供整合的元件](#bkmk_components)  
  
-   [語言串連](#bkmk_language)  
  
-   [相關工作](#bkmk_relatedtasks)  
  
##  <a name="bkmk_featuresum"></a> 功能摘要

 將報表伺服器設定為以 SharePoint 整合模式執行會提供下列的額外功能；只有在以此模式部署報表伺服器時，才能使用這些功能：  
  
-   使用 SharePoint 文件管理和共同作業功能，包括警示。 SharePoint 網站會提供統一入口網站，用於在單一位置存取和管理所有報表項目。  
  
-   使用 SharePoint 權限和驗證提供者來控制對報表、模型和其他項目的存取。  
  
-   使用 SharePoint 部署拓撲將報表透過網際網路連接散發到防火牆以外。 報表伺服器會以針對網際網路存取所設定的較大 SharePoint 部署內容提供報表和資料處理服務。  
  
-   在 SharePoint 網站的自訂應用程式頁面中管理報表、模型、資料來源、排程和報表記錄。 您可以在 SharePoint 網站上設定屬性、定義排程和訂閱並且建立與管理報表記錄，其方法與使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的其他工具來建立及管理這些項目時相同。  
  
-   將報表、報表模型、資源和共用資料來源檔發行或上傳到 SharePoint 文件庫，包括 Office SharePoint Server 中的 Report Center。  
  
     使用報表設計師、模型設計師與報表產生器來建立要直接發行至 SharePoint 文件庫的報表和資料來源。 您也可以在 SharePoint 網站上使用「上傳」動作，將所有的報表定義和報表模型加入至 SharePoint 程式庫。  
  
     因為不論所使用的伺服器模式為何，報表伺服器都會以相同方式處理報表定義，所以報表資料和配置並不會受到伺服器模式的影響。 任何能夠在原生模式報表伺服器中執行的報表，也都可以在設定為 SharePoint 整合模式的報表伺服器上執行。  
  
-   使用新的 SharePoint 傳遞延伸模組向 SharePoint 程式庫訂閱報表並將報表傳遞至 SharePoint 程式庫。 您也可以透過電子郵件傳遞報表或將報表傳遞至共用資料夾。 報表伺服器傳遞延伸模組會用來傳遞報表。 您可以使用執行階段查詢的訂閱者資料，針對大規模的報表散發，建立資料驅動訂閱。  
  
-   您可以加入至 SharePoint 頁面以檢視 SharePoint Web 應用程式中之報表的報表檢視器 Web 組件。 Web 組件包含頁面導覽、搜尋、列印和匯出功能。  
  
-   根據新的 SOAP 端點進行程式設計，以建立能夠與 SharePoint 網站整合的自訂應用程式。 您也可以使用更新的 Windows Management Instrumentation (WMI) 提供者，以程式設計的方式設定以 SharePoint 整合模式執行的報表伺服器執行個體。  
  
-   連接模式中的 Microsoft Access 服務報告。  
  
-   AAM 區域、網際網路部署，以及 SharePoint 清單的 SharePoint 使用者 Token。  
  
##  <a name="bkmk_connectedandlocal"></a> 連接模式與本機模式

 SQL Server 2008 R2 版本導入了全新的 *「本機模式」* (Local Mode)，可用於從已安裝適用於 SharePoint 2010 產品之 Microsoft SQL Server 2008 R2 或更新版的 Reporting Services 增益集的 SharePoint 2010 伺服器檢視報表。  
  
-   *本機模式*:本機模式可讓您從 SharePoint 文件庫本機轉譯報表，而不需要與 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 報表伺服器整合。 需要 SharePoint 產品的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 增益集，但不需要 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 報表伺服器。 增益集可以利用幾種不同的方式安裝，包括 SharePoint 2010 產品準備工具。 如需本機模式的詳細資訊，請參閱[本機模式與連線模式報表 [報表檢視器] &#40;Reporting Services SharePoint 模式&#41;](../../2014/reporting-services/local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md)並[哪裡可以找到的 Reporting Services 增益集適用於 SharePoint 產品](install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)。  
  
-   *連接模式*:連接的模式的支援藉由整合[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]至 SharePoint 伺服器陣列中使用 SharePoint 管理中心內的報表伺服器。 與報表伺服器整合可讓您完整端對端報表，並提供 SharePoint 2010 的共同作業功能以及報表伺服器，包括伺服器架構功能：訂用帳戶、 快照及伺服器架構處理。  
  
##  <a name="bkmk_unsupportedsharepoint"></a> 不支援的 SharePoint 功能

 並非所有 SharePoint 功能都可供整合作業使用。 以下是 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不會直接整合之 SharePoint 功能的清單：  
  
-   Secure Store Service。  
  
-   您無法在文件庫中針對 Reporting Services 檔案使用 SharePoint Outlook 行事曆整合或 SharePoint 排程。  
  
-   SharePoint 商務資料目錄。  
  
-   在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 頁面上也不支援 SharePoint 個人化。 如果針對匿名存取啟用 SharePoint Web 應用程式，則不支援報表伺服器整合。  
  
-   SQL Server Reporting Services **不** 支援 SharePoint 文件庫版本控制。 如果您將報表項目儲存在已啟用「文件版本歷程記錄」設定的文件庫中，則 Reporting Services 功能將無法正確運作，而且會在 ULS 記錄中產生錯誤。 下列是 ULS 記錄中錯誤的範例：  
  
    -   「…與報表相關聯的資料來源已經停用」。  
  
     文件庫版本歷程記錄會在 [文件庫設定] 的 [版本設定] 頁面上設定。  
  
##  <a name="bkmk_supportedcombinations"></a> 支援的 SharePoint 增益集與報表伺服器組合

 在報表伺服器、適用 SharePoint 之 Reporting Services 增益集，以及 SharePoint 產品的所有組合中，並不支援所有功能。 如需詳細資訊，請參閱 <<c0> [ 組合支援的 SharePoint 和 Reporting Services 伺服器與增益集&#40;SQL Server 2014&#41;</c0>](install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
> [!NOTE]  
>  正確版本的 Reporting Services 增益集必須搭配對應版本的 SharePoint 產品使用。  
  
##  <a name="bkmk_components"></a> 提供整合的元件

 若要將伺服器結合在單一部署內，可以將 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 的安裝與 SharePoint 產品的執行個體相整合  
  
 整合是透過 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和適用 SharePoint 產品的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 增益集所提供。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 增益集是可免費轉散發的元件，您可以下載並安裝在執行正確版本之 SharePoint 的伺服器上。  
  
> [!TIP]  
>  在報表伺服器、適用 SharePoint 之 Reporting Services 增益集，以及 SharePoint 產品的所有組合中，並不支援所有功能。 如需詳細資訊，請參閱[組合支援的 SharePoint 和 Reporting Services 伺服器與增益集&#40;SQL Server 2014&#41;](install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)。  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 增益集可以在 SharePoint 上提供 ReportServer Proxy 端點、報表檢視器 Web 組件以及應用程式頁面，使您能夠在 SharePoint 網站或伺服陣列上檢視、儲存和管理報表伺服器內容。  
  
-   在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 上提供了更新的程式檔、SOAP 端點及自訂安全性和傳遞延伸模組。 報表伺服器必須設定為以 SharePoint 整合模式執行，且專門支援透過 SharePoint 網站來存取及傳遞報表。  
  
 在 SharePoint 上安裝 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 增益集並將這兩個伺服器設定整合之後，您就可以將報表伺服器內容類型上傳或發行至 SharePoint 文件庫，然後從 SharePoint 網站檢視和管理這些文件。 上傳或發行報表伺服器內容是第一個重要步驟；當您在 SharePoint 網站上選取報表定義 (.rdl)、報表模型 (.smdl) 和共用資料來源 (.rsds) 時，Web 組件和網頁就會變成可以使用。  
  
##  <a name="bkmk_language"></a> 語言串連

 [!INCLUDE[SPF2010](../includes/spf2010-md.md)] ＞及＜ [!INCLUDE[SPS2010](../includes/sps2010-md.md)] 產品所提供的語言比 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
 將報表伺服器設定為在 SharePoint 產品的部署內執行時，可能會看到多種語言。 使用者介面、文件和訊息可能會以下列語言顯示：  
  
-   所有源自 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 的應用程式頁面、工具、錯誤、警告和訊息，都會由 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 執行個體所使用的語言以其中一種 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 語言來顯示。  
  
-   您在 SharePoint 網站、報表檢視器 Web 組件與報表產生器上開啟的應用程式頁面將會以 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 增益集的其中一種支援語言來顯示。 若要檢視支援語言的清單，請移至 [SQL Server 下載區](https://msdn.microsoft.com/sql/downloads/) ，然後尋找 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 增益集的下載頁面。  
  
-   SharePoint 網站、SharePoint 管理中心、線上說明和訊息會以 Office Server 產品所支援的語言提供。  
  
 如果 SharePoint 產品或技術的語言與報表伺服器語言不同，則 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 會嘗試使用相同語系中最接近的語言。 如果找不到接近的替代語言，報表伺服器就會使用英文。  
  
##  <a name="bkmk_relatedtasks"></a> 相關工作

 下表摘要說明與 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式報表伺服器相關的工作：  
  
|**工作**|**連結**|  
|--------------|--------------|  
|安裝和設定 SharePoint 模式之 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 的詳細步驟。|[安裝 Reporting Services SharePoint Mode for SharePoint 2010](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)並[加入伺服器陣列中的其他報表伺服器&#40;SSRS 向外延展&#41;](install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)。|  
|加入額外的報表伺服器，藉以向外延展您的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 部署。|[將其他報表伺服器加入至伺服陣列&#40;SSRS 向外延展&#41;](install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)並[在 SharePoint 中的 SQL Server BI 功能的部署拓撲](../sql-server/install/deployment-topologies-for-sql-server-bi-features-in-sharepoint.md)。|  
|加入針對檢視和報表項目安裝之 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 元件的其他 SharePoint Web 前端。|[將其他 Reporting Services Web 前端加入至伺服器陣列](install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)|  
|設定用於 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 資料警示和訂閱功能的電子郵件。|[設定 Reporting Services 服務應用程式的電子郵件 &#40;SharePoint 2010 和 SharePoint 2013&#41;](install-windows/configure-e-mail-for-a-reporting-services-service-application.md)|  
|此版本的最新資訊位於 TechNet Wiki 上。|[SQL Server 2012 Reporting Services 提示、秘訣和疑難排解](https://go.microsoft.com/fwlink/?LinkId=221297)。|  
  
## <a name="see-also"></a>另請參閱  
 [安裝或解除安裝 Reporting Services 增益集，適用於 SharePoint &#40;SharePoint 2010 和 SharePoint 2013&#41; ](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md) [硬體和軟體需求的 Reporting Services SharePoint 模式](../../2014/sql-server/install/hardware-and-software-requirements-for-reporting-services-in-sharepoint-mode.md) [在 SharePoint 網站上的報表檢視器 Web 組件](../../2014/reporting-services/report-viewer-web-part-on-a-sharepoint-site.md)