---
title: 部署檢查清單： 將 Reporting Services 安裝至現有的 SharePoint 伺服器陣列 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 436b4c3d-3f2f-464a-be7e-5c051d9ffb8f
caps.latest.revision: 12
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: d13c0329073781f54ac02b653b15ead4959bd96e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036725"
---
# <a name="deployment-checklist-install-reporting-services-into-an-existing-sharepoint-farm"></a>部署檢查清單：將 Reporting Services 安裝至現有的 SharePoint 伺服器陣列
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 報表伺服器可以安裝在新的 SharePoint 伺服器陣列，或在現有的 SharePoint 伺服器陣列。 本主題描述的可能案例和最佳作法安裝[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]至現有 SharePoint 伺服器陣列。  
  
## <a name="prerequisites"></a>必要條件  
 執行安裝程式之前，請檢閱下列資訊：  
  
|步驟|連結|  
|----------|----------|  
|建立或識別報表伺服器部署中使用的帳戶。 您必須擁有報表伺服器服務的服務帳戶，以及連接到報表伺服器資料庫的認證||  
|決定執行個體上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]來主控報表伺服器資料庫。 您可以使用的本機或遠端執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 您所選擇之執行個體所在的電腦上，應有足以容納您報表的儲存容量。||  
|(選擇性) 如果您想要在訂閱中使用報表伺服器電子郵件，請尋找會對組織提供電子郵件服務之 SMTP 伺服器或閘道的名稱|[為電子郵件傳遞設定報表伺服器&#40;SSRS 組態管理員&#41;](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)|  
|注意： 如果您要從先前的 CTP 版本升級電腦[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和組態檔進行了自訂變更，您必須對組態檔，相同的變更來升級之後[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 受影響的檔案是**web.config**和**client.config**。||  
  
## <a name="installation-scenarios"></a>安裝案例  
 下表說明可能的情況下，當您安裝[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]至現有 SharePoint 伺服器陣列。 本機模式讓您從沒有與整合的 SharePoint 文件庫本機轉譯報表[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]報表伺服器。 需要 SharePoint 產品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集，但不需要 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器。 如需本機模式的詳細資訊，請參閱[本機模式與連接模式報表在報表檢視器&#40;Reporting Services SharePoint 模式&#41;](../../../2014/reporting-services/local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md)和[如何尋找 Reporting Services 增益集適用於 SharePoint 產品](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)。  
  
|正在啟動組態|工作流程|正在結束組態|註解|  
|----------------------------|--------------|--------------------------|--------------|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 在本機模式中|Installation|已連接模式 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。||  
|連接模式[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]或 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|就地升級|已連接模式 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。||  
|連接模式[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]或 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|移轉|已連接模式 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。||  
  
## <a name="installation-and-in-place-upgrade-checklist"></a>安裝和就地升級檢查清單  
 下表摘要說明您應檢閱及用於安裝的步驟、工具及資訊：  
  
|步驟|連結|  
|----------|----------|  
|**安裝與初始組態**||  
|在所有 Web 前端 (WFE) 電腦上安裝 SharePoint 增益集。|[將其他 Reporting Services Web 前端加入至伺服器陣列](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)|  
|安裝 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Reporting Services 和 Database Engine。|[安裝適用於 SharePoint 2010 的 Reporting Services SharePoint 模式](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|至少建立一個 SSRS 服務應用程式並設定服務應用程式關聯。|請參閱 < 服務應用程式 > 一節[安裝 Reporting Services SharePoint Mode for SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|**其他組態**||  
|將 SSRS 內容類型加入您的文件庫。|[將報表伺服器內容類型加入至文件庫&#40;的 Reporting Services SharePoint 整合模式&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md)|  
|佈建 SQL Server Agent|[SSRS 服務應用程式的佈建訂閱及警示](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)|  
|設定服務應用程式的電子郵件設定|[Reporting Services 服務應用程式，設定電子郵件&#40;SharePoint 2010 和 SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)|  
|設定對 Windows Token 服務的宣告 (c2WTS)|[Claims to Windows Token Service &#40;C2WTS&#41;和 Reporting Services](../../../2014/sql-server/install/claims-to-windows-token-service-c2wts-and-reporting-services.md)|  
  
## <a name="migration-checklist"></a>移轉檢查清單  
 以下是從現有安裝移轉至新安裝的基本步驟清單。  
  
|步驟|連結|  
|----------|----------|  
|安裝及設定新伺服器。 這包括下列項目：<br /><br /> SharePoint 產品準備工具<br /><br /> SharePoint 2010 產品<br /><br /> SharePoint 2010 SP1<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 以 SharePoint 模式<br /><br /> SharePoint 2010 產品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集|[安裝適用於 SharePoint 2010 的 Reporting Services SharePoint 模式](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|至少建立一個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式||  
|備份[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]資料庫||  
|備份[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]加密金鑰||  
|還原 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料庫和加密金鑰||  
|對應至新的所有 web 應用程式[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]服務應用程式|The new installation <bpt id="p1">**</bpt>is now functional<ept id="p1">**</ept>|  
|移除舊伺服器上的整合 URL。|從 SharePoint 管理中心的 **[一般應用程式設定]** 頁面上，按一下 **[Reporting Services 整合]**。|  
|視需要從舊安裝解除安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。||  
  
## <a name="next-steps"></a>後續步驟  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services SharePoint 模式安裝&#40;SharePoint 2010 和 SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)   
 [使用 SharePoint 2010 伺服陣列中的 SQL Server BI 功能的指引](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)   
 [支援的 SharePoint 與 Reporting Services 伺服器與增益集組合&#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
  