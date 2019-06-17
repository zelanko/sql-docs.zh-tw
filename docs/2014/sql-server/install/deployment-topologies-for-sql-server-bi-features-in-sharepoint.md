---
title: 在 SharePoint 中的 SQL Server BI 功能的部署拓撲 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 39f76bc7-94e6-4dbc-bfa5-d56f4430bb26
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 7ef3ecf31c0539f3b3cb2cf5a4f04b044e625bd1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095598"
---
# <a name="deployment-topologies-for-sql-server-bi-features-in-sharepoint"></a>Deployment Topologies for SQL Server BI Features in SharePoint
  本主題說明在 SharePoint 2010 和 SharePoint 2013 環境中安裝 SQL Server 商業智慧功能 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] 的常見拓撲。 例如，單一伺服器和三層式安裝。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; SharePoint 2010|  
  
 **本主題內容：**  
  
-   [SharePoint 2013 範例部署拓撲](#bkmk_example_deployments_2013)  
  
    -   [PowerPivot for SharePoint 2013 和 Reporting Services 三重伺服器部署](#bkmk_bi_Sharepoint2013_3tier)  
  
    -   [PowerPivot for SharePoint 2013 單一伺服器部署](#bkmk_powerpivot_sharepoint2013_1server)  
  
    -   [PowerPivot for SharePoint 2013 雙重伺服器部署](#bkmk_powerpivot_sharepoint2013_2server)  
  
    -   [PowerPivot for SharePoint 2013 三重伺服器部署](#bkmk_powerpivot_sharepoint2013_3server)  
  
    -   [PowerPivot for SharePoint 2013 和 Reporting Services 單一伺服器部署](#bkmk_powerpivot_ssrs_sharepoint2013_1server)  
  
    -   [PowerPivot for SharePoint 2013 和 Reporting Services 雙重伺服器部署](#bkmk_powerpivot_ssrs_sharepoint2013_2server)  
  
-   [SharePoint 2010 範例部署拓撲](#bkmk_example_deployments_2010)  
  
    -   [單一伺服器部署](#bkmk_sharepoint2010_1server)  
  
    -   [雙層部署](#bkmk_sharepoint2010_2server)  
  
    -   [三層部署](#bkmk_sharepoint2010_3server)  
  
    -   [三層向外延展部署](#bkmk_sharepoint2010_scaleserver)  
  
##  <a name="bkmk_example_deployments_2013"></a> SharePoint 2013 範例部署拓撲  
 SQL Server 安裝選項 **[PowerPivot for SharePoint]** 不會相依於 SharePoint。 它不會使用 SharePoint 物件模型或介面來支援整合。 因此， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可以安裝在執行 Windows Server 2008 R2 或更新版本的任何電腦上。 它可以是 SharePoint 伺服器陣列中的應用程式伺服器，但這並非必要條件。 其中一個設定步驟是將 Excel Services 指向執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的伺服器。 如果需要負載平衡和容錯功能，建議您安裝並註冊多部以 SharePoint 模式執行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器。  
  
 **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式** 需要使用 SharePoint Server 2013 而且會運用 SharePoint 服務應用程式架構。  
  
 下列各節將說明一般部署拓撲：  
  
###  <a name="bkmk_bi_Sharepoint2013_3tier"></a> PowerPivot for SharePoint 2013 和 Reporting Services 三重伺服器部署  
 在下面的三重伺服器部署中，SQL Server Database Engine、以 SharePoint 模式執行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器，以及 SharePoint，會個別在不同的伺服器上執行。 [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] 2013 安裝程式套件 (**spPowerPivot.msi**) 必須在 SharePoint 伺服器上執行。  
  
 ![SSAS 和 SSRS SharePoint 模式 3 伺服器部署](../../../2014/sql-server/install/media/as-and-rs-3server-deployment.gif "SSAS 和 SSRS SharePoint 模式 3 伺服器部署")  
  
|||  
|-|-|  
|**(1)**|Excel 服務應用程式。 此服務應用程式是在 SharePoint 安裝過程中建立。|  
|**(2)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式。 預設名稱是 **[預設的 PowerPivot 服務應用程式]** 。|  
|**(3)**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式。|  
|**(4)**|從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝媒體或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 功能套件安裝 SharePoint 的 Reporting Services 增益集。|  
|**(5)**|執行 **spPowerPivot.msi** ，以安裝資料提供者、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 組態工具、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫及排程資料重新整理。|  
|**(6)**|SharePoint 模式的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器。 在 **[資料模型設定]** 中設定 Excel Services 應用程式使用此伺服器。|  
|**(7)**|SharePoint 內容、組態和服務應用程式資料庫。|  
  
 ![SharePoint 設定](../../../2014/analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 設定")[透過 Microsoft SQL Server Connect 提交意見與連絡資訊](https://connect.microsoft.com/SQLServer/Feedback)(https://connect.microsoft.com/SQLServer/Feedback) 。  
  
###  <a name="bkmk_powerpivot_sharepoint2013_1server"></a> PowerPivot for SharePoint 2013 單一伺服器部署  
 單一伺服器部署對於測試很有用，但是不建議用於實際部署。  
  
 下圖說明單一伺服器 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署之一部分的元件。  
  
 ![PowerPivot for SharePoint 單一伺服器部署](../../../2014/sql-server/install/media/as-powerpivot-mode-1server-deployment.gif "PowerPivot for SharePoint 單一伺服器部署")  
  
|||  
|-|-|  
|**(1)**|Excel 服務應用程式。 此服務應用程式是在 SharePoint 安裝過程中建立。|  
|**(2)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式。 預設名稱是 **[預設的 PowerPivot 服務應用程式]** 。|  
|**(3)**|SharePoint 內容、組態和服務應用程式資料庫。|  
|**(4)**|SharePoint 模式的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器。 在 **[資料模型設定]** 中設定 Excel Services 應用程式使用此伺服器。|  
  
###  <a name="bkmk_powerpivot_sharepoint2013_2server"></a> PowerPivot for SharePoint 2013 雙重伺服器部署  
 在下列雙重伺服器部署中，SQL Server Database Engine 和 SharePoint 模式的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會在與 SharePoint 不同的伺服器上執行。 若為 SharePoint 2013， [!INCLUDE[ssGeminiLongvnext](../../includes/ssgeminilongvnext-md.md)] 安裝程式套件 (**spPowerPivot.msi**) 是安裝在 SharePoint 伺服器上。  
  
 [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] 擴充 SharePoint Server 2013，以便加入伺服器端資料重新整理處理、 資料提供者，[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]圖庫及管理支援[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]活頁簿與 Excel 活頁簿具有進階資料模型。  
  
 此安裝程式套件屬於 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 功能套件的一部分。 可以從下載的 feature pack[!INCLUDE[msCoName](../../includes/msconame-md.md)]下載中心[適用於 Microsoft® SharePoint® 的 Microsoft® SQL Server® 2014 PowerPivot®](https://go.microsoft.com/fwlink/?LinkID=296473) (超連結"<https://go.microsoft.com/fwlink/?LinkID=296473>"\t"_blank" <https://go.microsoft.com/fwlink/?LinkID=296473>)。  
  
 ![SSAS PowerPivot 模式 2 伺服器部署](../../../2014/analysis-services/media/as-powerpivot-mode-2server-deployment.gif "SSAS PowerPivot 模式 2 伺服器部署")  
  
|||  
|-|-|  
|**(1)**|Excel 服務應用程式。 此服務應用程式是在 SharePoint 安裝過程中建立。|  
|**(2)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式。 預設名稱是 **[預設的 PowerPivot 服務應用程式]** 。|  
|**(3)**|執行 **spPowerPivot.msi** ，以安裝資料提供者、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 組態工具、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫及排程資料重新整理。|  
|**(4)**|SharePoint 模式的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器。 在 **[資料模型設定]** 中設定 Excel Services 應用程式使用此伺服器。|  
|**(5)**|SharePoint 內容、組態和服務應用程式資料庫。|  
  
###  <a name="bkmk_powerpivot_sharepoint2013_3server"></a> PowerPivot for SharePoint 2013 三重伺服器部署  
 在下面的三重伺服器部署中，SQL Server Database Engine、以 SharePoint 模式執行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器，以及 SharePoint，會個別在不同的伺服器上執行。 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 安裝程式套件 (spPowerPivot.msi) 必須安裝在 SharePoint 伺服器上。  
  
 ![PowerPivot 模式 3 伺服器部署做](../../../2014/sql-server/install/media/as-powerpivot-mode-3server-deployment.gif "以 PowerPivot 模式 3 伺服器部署")  
  
|||  
|-|-|  
|**(1)**|Excel 服務應用程式。 此服務應用程式是在 SharePoint 安裝過程中建立。|  
|**(2)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式。 預設名稱是 **[預設的 PowerPivot 服務應用程式]** 。|  
|**(3)**|執行 spPowerPivot.msi，以安裝資料提供者、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 組態工具、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫及排程資料重新整理。|  
|**(4)**|SharePoint 模式的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器。 在 **[資料模型設定]** 中設定 Excel Services 應用程式使用此伺服器。|  
|**(5)**|SharePoint 內容、組態和服務應用程式資料庫。|  
  
###  <a name="bkmk_powerpivot_ssrs_sharepoint2013_1server"></a> PowerPivot for SharePoint 2013 和 Reporting Services 單一伺服器部署  
 單一伺服器部署對於測試很有用，但是不建議用於實際部署。  
  
 ![SSAS 和 SSRS SharePoint 模式 1 伺服器部署](../../../2014/sql-server/install/media/as-and-rs-1server-deployment.gif "SSAS 和 SSRS SharePoint 模式 1 伺服器部署")  
  
|||  
|-|-|  
|**(1)**|Excel 服務應用程式。 此服務應用程式是在 SharePoint 安裝過程中建立。|  
|**(2)**|PowerPivot 服務應用程式。 預設名稱是 **[預設的 PowerPivot 服務應用程式]** 。|  
|**(3)**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式。|  
|**(4)**|從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝媒體或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 功能套件安裝 SharePoint 的 Reporting Services 增益集。|  
|**(5)**|SharePoint 內容、組態和服務應用程式資料庫。|  
|**(6)**|SharePoint 模式的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器。 在 **[資料模型設定]** 中設定 Excel Services 應用程式使用此伺服器。|  
  
###  <a name="bkmk_powerpivot_ssrs_sharepoint2013_2server"></a> PowerPivot for SharePoint 2013 和 Reporting Services 雙重伺服器部署  
 在下列雙重伺服器部署中，SQL Server Database Engine 和以 SharePoint 模式執行的 Analysis Services 伺服器會與 SharePoint 在不同的伺服器上執行。 PowerPivot for SharePoint 2013 安裝程式套件 **(spPowerPivot.msi)** 必須在 SharePoint 伺服器上執行。  
  
 ![SSAS 和 SSRS SharePoint 模式 2 伺服器部署](../../../2014/sql-server/install/media/as-and-rs-2server-deployment.gif "SSAS 和 SSRS SharePoint 模式 2 伺服器部署")  
  
|||  
|-|-|  
|**(1)**|Excel 服務應用程式。 此服務應用程式是在 SharePoint 安裝過程中建立。|  
|**(2)**|PowerPivot 服務應用程式。 預設名稱是 **[預設的 PowerPivot 服務應用程式]** 。|  
|**(3)**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式。|  
|**(4)**|從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝媒體或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 功能套件安裝 SharePoint 的 Reporting Services 增益集。|  
|**(5)**|執行 **spPowerPivot.msi** 以安裝資料提供者、PowerPivot 組態工具、PowerPivot 圖庫及排程資料重新整理。|  
|**(6)**|SharePoint 模式的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器。 在 **[資料模型設定]** 中設定 Excel Services 應用程式使用此伺服器。|  
|**(7)**|SharePoint 內容、組態和服務應用程式資料庫。|  
  
##  <a name="bkmk_example_deployments_2010"></a> SharePoint 2010 範例部署拓撲  
 下圖顯示在每個階層上執行的服務和提供者。 請注意，該圖表包含許多內建服務；某些 SQL Server BI 案例需要這些服務。 在 SharePoint 中部署 PowerPivot for SharePoint 或 Reporting Services 需要或是建議使用 Excel Services、Secure Store Services 及「對 Windows Token 服務的宣告」。 此外，某些 PowerPivot 資料存取案例還需要 MSOLAP OLE DB 提供者和 ADO.NET Services。 如果您想根據在 SharePoint 外部主控的表格式模型資料庫，建立 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 報表，您也可以在資料層上安裝 Analysis Services。  
  
 ![邏輯架構圖](../../../2014/sql-server/install/media/sql11bisetup.gif "邏輯架構圖")  
  
##  <a name="bkmk_sharepoint2010_1server"></a> 單一伺服器部署  
 您可以將所有伺服器元件 (包括資料層) 安裝在單一電腦上。 如果您要評估軟體或在 SharePoint 模式下開發包含 Reporting Services 的自訂應用程式，此部署組態相當實用。 此部署最容易設定。 所有元件都安裝在相同的電腦上，因此它也使用最少的授權數目。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 及 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會當做 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的單一授權複本來安裝。  
  
 若要在單一伺服器上安裝所有功能，請在相同的實體伺服器上循序安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 及 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 。 如需有關獨立伺服器組態的指示，請參閱[部署檢查清單：Reporting Services、 Power View 及 PowerPivot for SharePoint](deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md)。  
  
##  <a name="bkmk_sharepoint2010_2server"></a> 雙層部署  
 雙層部署通常是 SharePoint Server 2010 在一部電腦上，而 SQL Server Database Engine 在第二部電腦上。 將資料層移至專用伺服器是兩部電腦之伺服器陣列的最常見組態。 在雙層伺服器陣列中，您需要在 SharePoint 伺服器上安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 。 前端的所有 Web 服務和應用程式層的共用服務會在相同的實體伺服器上執行。 雙層部署的安裝步驟與獨立部署非常類似；在這兩個部署中，您都會在相同的實體伺服器上循序安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 及 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 。  
  
##  <a name="bkmk_sharepoint2010_3server"></a> 三層部署  
 三層部署通常會分隔 Web 前端服務與處理中或需要大量記憶體的應用程式。 在此拓撲中，您只需要在應用程式伺服器上安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 。 您可以在伺服器組態期間，透過部署至伺服器陣列中之應用程式的方案，將在 Web 前端執行的 Web 服務當做後置安裝工作來安裝。 下圖描述三層部署。  
  
 ![3 個伺服器拓撲](../../../2014/sql-server/install/media/sql11bisetup-3server.gif "3 個伺服器拓撲")  
  
##  <a name="bkmk_sharepoint2010_scaleserver"></a> 三層向外延展部署  
 此拓撲描述在多部伺服器上執行相同共用服務的向外延展部署，可服務 PowerPivot 資料或 Reporting Services 報表的大量要求，並提供更佳的處理能力。 下圖顯示三個應用程式伺服器叢集，每個叢集執行不同的共用服務組合。 在 SharePoint 環境中，服務探索及可用性會內建於伺服器陣列中。 在執行相同共用服務應用程式之多部實體伺服器之間的平衡負載，是共用服務架構的一部分。  
  
 部署多伺服器陣列時，請務必遵循下列 SharePoint 文章中的指示：[多部伺服器的三層式伺服器陣列 (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?linkID=219834)。  
  
 ![5 個伺服器拓撲](../../../2014/sql-server/install/media/sql11bisetup-5server.gif "5 個伺服器拓撲")  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services SharePoint 模式安裝&#40;SharePoint 2010 和 SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)   
 [PowerPivot for SharePoint 2013 安裝](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)   
 [PowerPivot for SharePoint 2010 安裝](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
