---
title: "Reporting Services 報表伺服器 （SharePoint 模式） |Microsoft 文件"
ms.custom: 
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
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: a8cd1bd00ec92535fff73c5eaa4ff9bbe9274ef2
ms.contentlocale: zh-tw
ms.lasthandoff: 10/06/2017

---

# <a name="reporting-services-report-server-sharepoint-mode"></a>Reporting Services 報表伺服器 (SharePoint 模式)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  Reporting Services 報表伺服器設定為**SharePoint 模式**可以在 SharePoint 產品部署內執行。 SharePoint 模式的報表伺服器可以針對報表和其他 [!INCLUDE[ssRSnfoversion_md](../../includes/ssrsnoversion-md.md)] 內容類型使用 SharePoint 的共同作業和管理功能。 SharePoint 模式需要在 SharePoint Web 前端安裝適當版本的 Reporting Services 增益集適用於 SharePoint 產品。  
  
> [!NOTE]
> SQL Server 2016 之後已無法再使用 reporting Services 與 SharePoint 整合。

 如需有關安裝及設定的詳細資訊，請參閱以下主題：  
  
-   [安裝適用於 SharePoint 2010 的 Reporting Services SharePoint 模式](http://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c)。  
  
-   [將其他的報表伺服器加入至伺服陣列](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)。  
  
## <a name="feature-summary"></a>功能摘要

 將報表伺服器設定為以 SharePoint 整合模式執行會提供下列的額外功能；只有在以此模式部署報表伺服器時，才能使用這些功能：  
  
-   使用 SharePoint 文件管理和共同作業功能，包括警示。 SharePoint 網站會提供統一入口網站，用於在單一位置存取和管理所有報表項目。  
  
-   使用 SharePoint 權限和驗證提供者來控制對報表、模型和其他項目的存取。  
  
-   使用 SharePoint 部署拓撲將報表透過網際網路連接散發到防火牆以外。 報表伺服器會以針對網際網路存取所設定的較大 SharePoint 部署內容提供報表和資料處理服務。  
  
-   在 SharePoint 網站的自訂應用程式頁面中管理報表、模型、資料來源、排程和報表記錄。 您可以在 SharePoint 網站上設定屬性、定義排程和訂閱並且建立與管理報表記錄，其方法與使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的其他工具來建立及管理這些項目時相同。  
  
-   將報表、報表模型、資源和共用資料來源檔發行或上傳到 SharePoint 文件庫，包括 Office SharePoint Server 中的 Report Center。  
  
     使用報表設計師、模型設計師與報表產生器來建立要直接發行至 SharePoint 文件庫的報表和資料來源。 您也可以在 SharePoint 網站上使用「上傳」動作，將所有的報表定義和報表模型加入至 SharePoint 程式庫。  
  
     因為不論所使用的伺服器模式為何，報表伺服器都會以相同方式處理報表定義，所以報表資料和配置並不會受到伺服器模式的影響。 任何能夠在原生模式報表伺服器中執行的報表，也都可以在設定為 SharePoint 整合模式的報表伺服器上執行。  
  
-   使用新的 SharePoint 傳遞延伸模組向 SharePoint 程式庫訂閱報表並將報表傳遞至 SharePoint 程式庫。 您也可以透過電子郵件傳遞報表或將報表傳遞至共用資料夾。 報表伺服器傳遞延伸模組會用來傳遞報表。 您可以使用執行階段查詢的訂閱者資料，針對大規模的報表散發，建立資料驅動訂閱。  
  
-   您可以至 SharePoint 頁面以檢視 SharePoint web 應用程式中的之報表加入報表檢視器 web 組件。 Web 組件包含頁面導覽、 搜尋、 列印和匯出功能。  
  
-   根據新的 SOAP 端點進行程式設計，以建立能夠與 SharePoint 網站整合的自訂應用程式。 您也可以使用更新的 Windows Management Instrumentation (WMI) 提供者，以程式設計的方式設定以 SharePoint 整合模式執行的報表伺服器執行個體。  
  
-   連接模式中的 Microsoft Access 服務報告。  
  
-   AAM 區域、網際網路部署，以及 SharePoint 清單的 SharePoint 使用者 Token。  
  
## <a name="connected-mode-and-local-mode"></a>連接的模式與本機模式

 SQL Server 2008 R2 版本導入了全新的 *「本機模式」* (Local Mode)，可用於從已安裝適用於 SharePoint 2010 產品之 Microsoft SQL Server 2008 R2 或更新版的 Reporting Services 增益集的 SharePoint 2010 伺服器檢視報表。  
  
-   *本機模式*： 本機模式讓您從沒有與 Reporting Services 報表伺服器整合的 SharePoint 文件庫本機轉譯報表。 Reporting Services 增益集適用於 SharePoint 產品需要但不是 Reporting Services 報表伺服器。 增益集可以利用幾種不同的方式安裝，包括 SharePoint 2010 產品準備工具。 如需有關本機模式的詳細資訊，請參閱[本機模式與連接的模式報表在報表檢視器](../../reporting-services/report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md)和[如何適用於 SharePoint 產品的 Reporting Services 增益集尋找](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)。  
  
-   *連接模式*： 連接的模式的支援藉由使用 SharePoint 管理中心在 SharePoint 伺服器陣列整合 Reporting Services 報表伺服器。 與報表伺服器整合會啟用完整的端對端報表，並提供 SharePoint 2010 的共同作業功能以及報表伺服器的伺服器架構功能，包括：訂閱、快照集和伺服器架構處理。  
  
## <a name="unsupported-sharepoint-features"></a>不支援的 sharePoint 功能

 並非所有 SharePoint 功能都可供整合作業使用。 以下是 Reporting Services 不會直接整合之 SharePoint 功能的清單：  
  
-   Secure Store Service。  
  
-   您無法在文件庫中針對 Reporting Services 檔案使用 SharePoint Outlook 行事曆整合或 SharePoint 排程。  
  
-   SharePoint 商務資料目錄。  
  
-   在 Reporting Services 頁面上也不支援 SharePoint 個人化。 如果針對匿名存取啟用 SharePoint Web 應用程式，則不支援報表伺服器整合。  
  
-   SQL Server Reporting Services **不** 支援 SharePoint 文件庫版本控制。 如果您將報表項目儲存在已啟用「文件版本歷程記錄」設定的文件庫中，則 Reporting Services 功能將無法正確運作，而且會在 ULS 記錄中產生錯誤。 下列是 ULS 記錄中錯誤的範例：  
  
    -   「…與報表相關聯的資料來源已經停用」。  
  
     文件庫版本歷程記錄會在 [文件庫設定] 的 [版本設定] 頁面上設定。  
  
## <a name="supported-combinations-of-the-sharepoint-add-in-and-report-server"></a>支援的 SharePoint 增益集和報表伺服器組合

 在報表伺服器、適用 SharePoint 之 Reporting Services 增益集，以及 SharePoint 產品的所有組合中，並不支援所有功能。 如需詳細資訊，請參閱[支援的 SharePoint 和 Reporting Services 伺服器與增益集組合](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
> [!NOTE]  
>  正確版本的 Reporting Services 增益集必須搭配對應版本的 SharePoint 產品使用。  
  
## <a name="components-that-provide-integration"></a>提供整合的元件

 您可以結合在單一部署的伺服器，整合安裝[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Reporting Services 與 SharePoint 產品的執行個體  
  
 整合透過提供[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 Reporting Services 增益集適用於 SharePoint 產品。 Reporting Services 增益集是免費轉散發元件，您可以下載並執行適當的 SharePoint 版本的伺服器上安裝。  
  
> [!TIP]  
>  在報表伺服器、適用 SharePoint 之 Reporting Services 增益集，以及 SharePoint 產品的所有組合中，並不支援所有功能。 如需詳細資訊，請參閱[支援的 SharePoint 和 Reporting Services 伺服器與增益集組合](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)。  
  
-   在 SharePoint 上，Reporting Services 增益集提供 ReportServer proxy 端點、 報表檢視器 web 組件和應用程式頁面以便您可以檢視、 儲存和管理報表伺服器內容，在 SharePoint 網站或伺服陣列。  
  
-   在 Reporting Services 提供更新的程式檔、 SOAP 端點及自訂的安全性和傳遞延伸模組。 報表伺服器必須設定為以 SharePoint 整合模式執行，且專門支援透過 SharePoint 網站來存取及傳遞報表。  
  
 在 SharePoint 上安裝 Reporting Services 增益集，並設定整合的兩部伺服器之後，您可以上傳或發行至 SharePoint 文件庫中，報表伺服器內容類型，然後檢視及從 SharePoint 網站管理這些文件。 上傳或發行報表伺服器內容是一個重要的第一個步驟。web 組件和頁面變成可用，當您選取報表定義 (.rdl)、 報表模型 (.smdl) 和共用資料來源 (.rsds) 在 SharePoint 網站上。  
  
##  <a name="language-considerations"></a>語言串連

 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] ＞及＜ [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 產品所提供的語言比 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 將報表伺服器設定為在 SharePoint 產品的部署內執行時，可能會看到多種語言。 使用者介面、文件和訊息可能會以下列語言顯示：  
  
-   所有應用程式頁面、 工具、 錯誤、 警告和訊息源自 Reporting Services 會出現在其中一種 Reporting Services 執行個體所使用的語言[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]語言。  
  
-   Reporting Services 增益集，您開啟 SharePoint 網站、 報表檢視器 web 組件和報表產生器的應用程式頁面會出現在其中一種支援的語言。 若要檢視支援的語言清單，請移至[SQL Server 下載](http://msdn.microsoft.com/sql/downloads/)並尋找下載頁面上的 SQL Server 2016 Reporting Services 增益集。  
  
-   SharePoint 網站、SharePoint 管理中心、線上說明和訊息會以 Office Server 產品所支援的語言提供。  
  
 如果您的 SharePoint 產品或技術的語言與報表伺服器語言不同，Reporting Services 會嘗試使用最接近的相符項目會提供相同的語系的語言。 如果找不到接近的替代語言，報表伺服器就會使用英文。  
  
## <a name="related-tasks"></a>相關工作

 下表摘要說明 Reporting Services SharePoint 模式報表伺服器相關的工作：  
  
|**工作**|**連結**|  
|--------------|--------------|  
|安裝和設定 Reporting Services SharePoint 模式的詳細的步驟。|[安裝適用於 SharePoint 2010 的 Reporting Services SharePoint 模式](http://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c)和[將其他的報表伺服器加入至伺服陣列](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)。|  
|向外延展 Reporting Services SharePoint 部署加入其他報表伺服器。|[將其他的報表伺服器加入至伺服陣列](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)和[在 SharePoint 中的 SQL Server BI 功能的部署拓撲](http://msdn.microsoft.com/library/39f76bc7-94e6-4dbc-bfa5-d56f4430bb26)。|  
|加入其他 SharePoint web 前端，檢視和報表項目的安裝 Reporting Services 元件。|[將其他 Reporting Services web 前端加入至伺服器陣列](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)|  
|設定報表伺服器在 SharePoint 中的電子郵件。|[設定 Reporting Services 服務應用程式的電子郵件](../install-windows/configure-e-mail-for-a-reporting-services-service-application.md)|
|此版本的最新資訊位於 TechNet Wiki 上。|[SQL Server 2012 Reporting Services 提示、 秘訣和疑難排解](http://go.microsoft.com/fwlink/?LinkId=221297)。|  

## <a name="next-steps"></a>後續的步驟

[安裝或解除安裝 SharePoint 的 Reporting Services sdd 中](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
[報表檢視器 web 組件在 SharePoint 網站上](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
[測驗： 為 SharePoint 整合設定 SSRS 2012](http://go.microsoft.com/fwlink/?LinkId=306443)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)

