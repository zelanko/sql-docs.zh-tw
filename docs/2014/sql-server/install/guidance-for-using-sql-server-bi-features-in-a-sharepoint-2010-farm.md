---
title: SharePoint 2010 伺服陣列中使用 SQL Server BI 功能的指南 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 5f9a94c4-854b-4577-a8b1-7142f19904e3
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 25054c92124930d2d33b9f35eb43a1945d4a22bb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48197118"
---
# <a name="guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm"></a>在 SharePoint 2010 伺服器陣列中使用 SQL Server BI 功能的指引
  本主題摘要說明根據您使用之軟體版本的功能可用性， 也說明使用特定 SQL Server 功能的 SharePoint 2010 安裝需求。 如需有關 SharePoint 2013 的資訊，請參閱[在 SharePoint 中的 SQL Server BI 功能的部署拓撲](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md)。  
  
 本主題內容：  
  
-   [一般 SharePoint 2010 需求](#bkmk_generalsharepoint)  
  
-   [SharePoint 2010 Service Pack 1 (SP1)](#bkmk_sp1)  
  
-   [SharePoint 版本和 BI 功能的支援](#bkmk_vers)  
  
-   [SharePoint 2010 產品準備工具](#bkmk_prereq)  
  
-   [執行 SharePoint 安裝的需求與建議](#bkmk_install)  
  
##  <a name="bkmk_generalsharepoint"></a> 一般 SharePoint 2010 需求  
  
-   SharePoint 2010 產品只有 64 位元版本。 如果您已經安裝 32 位元版本的舊版 SharePoint，並在 SharePoint 整合模式下安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，您將無法升級至 SharePoint 2010。 如需詳細資訊，請檢閱 SharePoint 文件集。  
  
-   Reporting Services 包含 SharePoint 產品的增益集。 支援的增益集和報表伺服器組態可以比此處所示的層級更細微。 如需詳細資訊，請參閱 <<c0> [ 組合支援的 SharePoint 和 Reporting Services 伺服器與增益集&#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)。</c0>  
  
-   SharePoint 開發人員工具僅支援 SharePoint 獨立組態。  如需詳細資訊，請參閱 SharePoint 文件：[開發 SharePoint 方案的需求](http://msdn.microsoft.com/library/ee231582.aspx)。  
  
##  <a name="bkmk_vers"></a> SharePoint 版本和 BI 功能的支援  
 某些 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 商業智慧功能只有特定的 SharePoint 產品版本才有支援。  
  
|支援的功能|SharePoint 產品|  
|------------------------|------------------------|  
|[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]一項功能[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]增益集[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition。<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料警示。<br /><br /> [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].|[!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition。|  
|一般 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表檢視以及 SharePoint 的功能整合。|[!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Standard 和 Enterprise Edition。<br /><br /> [!INCLUDE[SPF2010](../../includes/spf2010-md.md)].|  
  
 如需詳細資訊，請參閱 <<c0> [ 支援的 SQL Server 2012 的版本功能](http://go.microsoft.com/fwlink/?linkid=232473)。  
  
##  <a name="bkmk_sp1"></a> SharePoint 2010 Service Pack 1 (SP1)  
 建議您將 SharePoint 2010 安裝更新為 SharePoint 2010 Service Pack 1 (SP1)。 下列情況都需要 SharePoint SP1：  
  
-   您想要針對 SharePoint 內容資料庫或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 目錄資料庫使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本的 Database Engine。  
  
-   您想要使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 組態工具。  
  
 SP1 的主要原因之一是為了使用在執行 SharePoint 安裝[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]是資料庫引擎功能**sp_dboption**，在舊版中已被取代，請在已停止[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]版本。 如需詳細資訊，請參閱[SQL Server 2014 中已停止的 Database Engine 功能](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)  
  
### <a name="sharepoint-2010-sp1-installation-guidance"></a>SharePoint 2010 SP1 安裝指引  
 [下載 SharePoint Server 2010 SP1](http://go.microsoft.com/fwlink/?LinkID=219697)並將它套用在伺服器陣列中的所有伺服器上。  
  
> [!NOTE]  
>  在現有的伺服器陣列，您必須使用下列其中一種**其他**步驟來完成 SharePoint SP1 升級。 如需詳細資訊，請參閱 <<c0> [ 當您安裝 Office 2010 SP1 和 SharePoint 2010 SP1 的已知問題](http://support.microsoft.com/kb/2532126)並[描述的 SharePoint Server 2010 SP1](http://support.microsoft.com/kb/2460045):  
  
-   **SharePoint 產品組態精靈:** 執行精靈以完成 SP1 升級和設定。  
  
-   **使用 psconfig 完成升級：** 執行命令`psconfig –upgrade`以完成 SP1 升級  
  
 如需詳細資訊，請參閱的 < 升級 > 一節[(SharePoint Server 2010)](http://technet.microsoft.com/library/cc263093.aspx)和[資源中心： 適用於 SharePoint 2010 產品的更新](http://technet.microsoft.com/sharepoint/ff800847.aspx)  
  
## <a name="sharepoint-installation-with-sql-server-bi-features"></a>具有 SQL Server BI 功能的 SharePoint 安裝  
  
###  <a name="bkmk_prereq"></a> SharePoint 2010 產品準備工具  
 SharePoint 產品準備工具可啟用作業系統中的伺服器角色，並安裝 SharePoint 安裝所需的其他必要條件軟體。 下表識別針對 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 設定伺服器的其他步驟。  
  
|元件|動作|  
|---------------|------------|  
|Reporting Services 增益集|SharePoint 2010 產品準備工具會安裝 Reporting Service 增益集的 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 包含 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 功能需要使用的新版本增益集。 您可以使用 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈] 安裝增益集，也可以從 MSDN 下載增益集。 如需有關何處可取得目前版本的增益集，以及如何將它安裝的詳細資訊，請參閱[適用於 SharePoint 產品中尋找 Reporting Services 增益集的位置](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)和[安裝或解除安裝 Reporting Services適用於 SharePoint 增益集&#40;SharePoint 2010 和 SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)。|  
|Analysis Services OLE DB 提供者 (MSOLAP)|SharePoint 2010 會將 SQL Server 2008 版的 OLE DB 提供者當做 Excel Services 部署的一部分來安裝。 此版本不支援 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料存取。 您應該在 SharePoint 伺服器上，安裝支援 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料連接的更新版提供者。 如需詳細資訊，請參閱[SharePoint 伺服器上安裝 Analysis Services OLE DB 提供者](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)|  
|ADO.NET 服務|SharePoint 2010 在先決條件清單中列出 ADO.NET 服務，但是先決條件安裝程式不會安裝此服務。 若要加入 ADO.NET 服務，您必須手動予以安裝。 如果您想使用 SharePoint 清單做為 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿或 Reporting Services 報表的資料摘要，則必須安裝 ADO.NET 服務。 如需相關指示，請參閱 <<c0> [ 安裝 ADO.NET Data Services 以支援資料摘要的 SharePoint 清單匯出](../../../2014/sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md)。|  
  
###  <a name="bkmk_install"></a> 執行 SharePoint 安裝的需求與建議  
 您安裝的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 功能和安裝這些功能的順序，會決定與 SharePoint 整合的可能層級。 例如，雖然有些功能整合層級可透過使用內建資料庫之 SharePoint 伺服器上的 Reporting Services 提供，但是大多數功能整合案例還是需要 SharePoint 的伺服器陣列安裝，因為只有伺服器陣列安裝可以提供某些 BI 功能所需的基礎結構。  
  
 SharePoint 伺服器陣列可以是單一伺服器或多部伺服器。 伺服器陣列安裝與獨立安裝的不同之處在於額外的基礎結構，例如「對 Windows Token 服務的宣告」。  
  
 當您選擇時，會啟用伺服器陣列**伺服器陣列**SharePoint 安裝程式中的選項。 如果您想使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 或 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]，則必須具有伺服器陣列安裝。 獨立 SharePoint 安裝是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 開發環境支援且常見的安裝。 但是針對實際執行環境，則建議 SharePoint 伺服器陣列安裝。  
  
 ![GMNI_SetupUI_SharePoint2010InstallType](../../../2014/sql-server/install/media/gmni-setupui-sharepoint2010installtype.gif "GMNI_SetupUI_SharePoint2010InstallType")  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共用服務也需要完整的伺服器安裝。  
  
 ![GMNI_SetupUI_SharePoint2010ServerType](../../../2014/sql-server/install/media/gmni-setupui-sharepoint2010servertype.gif "GMNI_SetupUI_SharePoint2010ServerType")  
  
 安裝程式精靈的最後一頁會提示您設定伺服器陣列，以及選擇性地設定預設 Web 應用程式和根網站集合。 大多數安裝程式使用者會遵循此安裝路徑。 如果基於某些原因而未設定伺服器陣列，您可以使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 組態工具中的伺服器陣列組態選項來設定伺服器陣列。  
  
 在舊版中，建議在安裝 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 時將伺服器陣列保留為未設定，因為如此可在您使用 SQL Server 安裝選項安裝準備使用狀態的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 時，減少所需的步驟。 在此版本中，這點不再重要。 您可以使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 組態工具來微調現有的伺服器陣列，讓伺服器陣列使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 安裝的建議設定。  
  
 您可以在現有的 SharePoint 伺服器陣列中安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 雖然您可以依照任何順序安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 或 SharePoint，不過 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的組態會因安裝順序而異。 如需詳細資訊，請參閱 <<c0> [ 加入伺服器陣列中的其他報表伺服器&#40;SSRS 向外延展&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)並[安裝 Reporting Services SharePoint Mode for SharePoint 2010</c0>](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
 ![GMNI_SetupUI_DoNotConfigureMOSS](../../../2014/sql-server/install/media/gmni-setupui-donotconfiguremoss.gif "GMNI_SetupUI_DoNotConfigureMOSS")  
  
## <a name="see-also"></a>另請參閱  
 [安裝和部署 SharePoint Server 2010](http://technet.microsoft.com/sharepoint/ee518643.aspx)   
 [多部伺服器的三層式伺服器陣列 (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?linkID=219834)  
  
  
