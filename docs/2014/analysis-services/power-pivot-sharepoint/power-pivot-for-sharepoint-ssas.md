---
title: PowerPivot for SharePoint (SSAS) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c4c393d3-4856-47ac-ab5f-15da2f240d1d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 486db389b3cca8936a5350da61880637406a1387
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66071136"
---
# <a name="powerpivot-for-sharepoint-ssas"></a>PowerPivot for SharePoint (SSAS)
  PowerPivot for SharePoint 是以 SharePoint 模式執行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器。 PowerPivot for SharePoint 提供將 PowerPivot 資料裝載於 SharePoint 伺服器陣列的功能。 PowerPivot 資料是您使用下列其中一個項目建立的分析資料模型：  
  
-   PowerPivot for Excel 2010 增益集  
  
-   Excel 2013  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 | [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010  
  
 這些資料的伺服器裝載需要 SharePoint、Excel Services 和 PowerPivot for SharePoint 安裝。 資料載入到 PowerPivot for SharePoint 執行個體上，在此處可透過伺服器為 Excel 2010 活頁簿提供的 PowerPivot 資料重新整理功能或是為 Excel 2013 活頁簿提供的 SharePoint 2013 Excel Services，依排程間隔重新整理資料。  
  
## <a name="powerpivot-for-sharepoint-2013"></a>PowerPivot for SharePoint 2013  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 支援 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint 2013 Excel Services 使用包含資料模型和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Power View 報表的 Excel 活頁簿。  
  
 SharePoint 2013 中的 Excel Services 包含資料模型功能，可在瀏覽器中啟用與 PowerPivot 活頁簿的互動。 您不需要將 PowerPivot for SharePoint 2013 增益集部署至伺服器陣列。 您只需要在 SharePoint 模式下安裝 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器，並且在 Excel Services **[資料模型]** 設定中註冊伺服器即可。  
  
 若部署 PowerPivot for SharePoint 2013 增益集，會在 SharePoint 伺服器陣列中啟用其他功能與特性。 其他功能包括 PowerPivot 圖庫、排程資料重新整理及 PowerPivot 管理儀表板。  
  
 ![SSAS PowerPivot 模式 2 伺服器部署](../media/as-powerpivot-mode-2server-deployment.gif "SSAS PowerPivot 模式 2 伺服器部署")  
  
## <a name="powerpivot-for-sharepoint-2010"></a>PowerPivot for SharePoint 2010  
 PowerPivot for SharePoint 2010 提供將 PowerPivot 資料裝載於 SharePoint 2010 伺服器陣列的功能。 PowerPivot 資料是使用 PowerPivot for Excel 增益集在 Excel 中建立的分析資料模型。 這些資料的伺服器裝載需要 SharePoint 2010、Excel Services 和 PowerPivot for SharePoint 安裝。 資料載入到伺服器陣列中的 PowerPivot for SharePoint 執行個體，在此處可透過伺服器提供的 PowerPivot 資料重新整理功能，依排程間隔重新整理資料。  
  
### <a name="components-of-powerpivot-for-sharepoint-2010"></a>PowerPivot for SharePoint 2010 的元件  
 PowerPivot for SharePoint 實作為共用服務，這表示內建功能和基礎結構可用來管理、保護和使用 PowerPivot 服務應用程式。 伺服器和資料庫探索、重新導向和連接管理全都是在伺服器陣列層級管理。 管理中心提供用來管理伺服器識別、伺服器狀態和組態屬性之服務的管理介面。  
  
 PowerPivot for SharePoint 的完整部署包含在 SharePoint 伺服器陣列中與 Excel 和 Excel Services 整合的用戶端與伺服器元件。 Excel 活頁簿內的 PowerPivot 資料是一種 Analysis Services 資料庫，它需要 Analysis Services xVelocity 記憶體中分析引擎 (VertiPaq) 以載入和查詢資料。 在用戶端工作站上，xVelocity 引擎會在 Excel 中以同處理序執行。 在 SharePoint 伺服器陣列中，Analysis Services 會在應用程式伺服器上執行，並與處理 PowerPivot 資料要求的相關服務搭配使用。 下圖說明 PowerPivot 用戶端與伺服器元件：  
  
 ![GMNI_GeminiArch2](../media/gmni-geminiarch2.gif "GMNI_GeminiArch2")  
  
 PowerPivot Web 服務在 Web 應用程式伺服器上執行。 它會將來自 Web 應用程式的要求導向至伺服器陣列中的 PowerPivot 系統服務執行個體。  
  
 PowerPivot 系統服務會將載入要求發給 Analysis Services 伺服器，以及管理已載入記憶體之資料的進行中連接，並且於不再使用資料或系統資源有競爭時，快取或卸載資料。 它也會追蹤使用者活動。 在報表中收集及呈現伺服器健全狀況資料和其他使用量資料，以表示系統的執行效能。  
  
 SharePoint 整合模式的 Analysis Service 伺服器執行個體會完成部署。 它會載入、查詢和卸載資料。 如果活頁簿設定為使用 PowerPivot 資料重新整理，它也會處理資料。  每個執行個體會與相同安裝中的本機 PowerPivot 系統服務緊密結合在一起。  
  
##  <a name="bkmk_RelatedContent"></a> 本節內容  
 [管理中心的 PowerPivot 伺服器管理和設定](power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
 [使用 Windows PowerShell 的 PowerPivot 設定](power-pivot-configuration-using-windows-powershell.md)  
  
 [PowerPivot 設定工具](power-pivot-configuration-tools.md)  
  
 [PowerPivot 驗證及授權](power-pivot-authentication-and-authorization.md)  
  
 [PowerPivot 健全狀況規則-設定](configure-power-pivot-health-rules.md)  
  
 [PowerPivot 管理儀表板和使用量資料](power-pivot-management-dashboard-and-usage-data.md)  
  
 [PowerPivot Gallery](../../2014-toc/books-online-for-sql-server-2014.md)  
  
 [PowerPivot 資料存取](power-pivot-data-access.md)  
  
 [PowerPivot 資料重新整理](power-pivot-data-refresh.md)  
  
 [PowerPivot 資料摘要](power-pivot-data-feeds.md)  
  
 [PowerPivot BI 語意模型連接&#40;.bism&#41;](power-pivot-bi-semantic-model-connection-bism.md)  
  
 **其他章節內容**  
  
## <a name="additional-topics"></a>其他主題  
 [升級 PowerPivot for SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)  
  
 [PowerPivot for SharePoint 2013 安裝](../instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
 [Powerpivot for SharePoint 的 PowerShell 參考](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)  
  
 [授權拓撲和成本範例 SQL Server 2014 自助商業智慧](../../sql-server/install/example-license-topologies-costs-self-service-business-intelligence.md)  
  
## <a name="see-also"></a>另請參閱  
 [PowerPivot 規劃與部署](https://go.microsoft.com/fwlink/?linkID=220972)   
 [Powerpivot for SharePoint 災害復原](https://go.microsoft.com/fwlink/p/?LinkId=389570)  
  
  
