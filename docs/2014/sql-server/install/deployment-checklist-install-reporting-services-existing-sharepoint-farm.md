---
title: 部署檢查清單：將 Reporting Services 安裝到現有的 SharePoint 伺服器陣列 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 436b4c3d-3f2f-464a-be7e-5c051d9ffb8f
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: e7a66be0d4e002643ffe1c72ce8c44aa50f61c0e
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952617"
---
# <a name="deployment-checklist-install-reporting-services-into-an-existing-sharepoint-farm"></a>部署檢查清單：將 Reporting Services 安裝至現有的 SharePoint 伺服器陣列
  您可以將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 報表伺服器安裝至新的 SharePoint 伺服器陣列中，或安裝至現有的 SharePoint 伺服器陣列中。 此主題描述將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝至現有 SharePoint 伺服器陣列中的可能案例和最佳作法。  
  
## <a name="prerequisites"></a>Prerequisites  
 執行安裝程式之前，請檢閱下列資訊：  
  
|步驟|連結|  
|----------|----------|  
|建立或識別報表伺服器部署中使用的帳戶。 您必須擁有報表伺服器服務的服務帳戶，以及連接到報表伺服器資料庫的認證||  
|決定主控報表伺服器資料庫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 您可以使用本機或遠端 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。 您所選擇之執行個體所在的電腦上，應有足以容納您報表的儲存容量。||  
|(選擇性) 如果您想要在訂閱中使用報表伺服器電子郵件，請尋找會對組織提供電子郵件服務之 SMTP 伺服器或閘道的名稱|[設定報表伺服器用於以電子郵件&#40;傳遞 SSRS Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)|  
|注意：如果您要從先前的 CTP 版本升級電腦 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 而且已對設定檔進行自訂變更，則在升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]之後，您將需要對設定檔進行相同的變更。 受影響的檔案為**web.config**和**client .config**。||  
  
## <a name="installation-scenarios"></a>安裝案例  
 下表說明將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝至現有 SharePoint 伺服器陣列中的可能案例。 本機模式可讓您從 SharePoint 文件庫本機轉譯報表，而不需要與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器整合。 需要 SharePoint 產品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集，但不需要 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器。 如需原生模式的詳細資訊，請參閱[報表查看&#40;器中的原生模式與連接模式報表 Reporting Services sharepoint&#41;模式](../../../2014/reporting-services/local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md)，以及[尋找適用于 sharepoint 產品之 Reporting Services 增益集的位置](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)。  
  
|正在啟動組態|工作流程|正在結束組態|註解|  
|----------------------------|--------------|--------------------------|--------------|  
|本機模式的 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|安裝|已連接模式 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。||  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]已連接模式 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 {3}|就地升級|已連接模式 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。||  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]已連接模式 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 {3}|移轉|已連接模式 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。||  
  
## <a name="installation-and-in-place-upgrade-checklist"></a>安裝和就地升級檢查清單  
 下表摘要說明您應檢閱及用於安裝的步驟、工具及資訊：  
  
|步驟|連結|  
|----------|----------|  
|**安裝和初始設定**||  
|在所有 Web 前端 (WFE) 電腦上安裝 SharePoint 增益集。|[將其他 Reporting Services Web 前端加入至伺服器陣列](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)|  
|安裝 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Reporting Services 和 Database Engine。|[安裝適用於 SharePoint 2010 的 Reporting Services SharePoint 模式](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|至少建立一個 SSRS 服務應用程式並設定服務應用程式關聯。|請參閱[安裝適用于 sharepoint 2010 的 Reporting Services Sharepoint 模式](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)中的「服務應用程式」一節|  
|**其他設定**||  
|將 SSRS 內容類型加入您的文件庫。|[將報表伺服器內容類型加入至 SharePoint &#40;整合模式 Reporting Services 的程式庫&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md)|  
|佈建 SQL Server Agent|[SSRS 服務應用程式的佈建訂閱及警示](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)|  
|設定服務應用程式的電子郵件設定|[設定 Reporting Services 服務應用程式的電子郵件 &#40;SharePoint 2010 和 SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)|  
|設定對 Windows Token 服務的宣告 (c2WTS)|[對 Windows Token 服務&#40;的宣告&#41; C2WTS 和 Reporting Services](../../../2014/sql-server/install/claims-to-windows-token-service-c2wts-and-reporting-services.md)|  
  
## <a name="migration-checklist"></a>移轉檢查清單  
 以下是從現有安裝移轉至新安裝的基本步驟清單。  
  
|步驟|連結|  
|----------|----------|  
|安裝及設定新伺服器。 這包括下列項目：<br /><br /> SharePoint 產品準備工具<br /><br /> SharePoint 2010 產品<br /><br /> SharePoint 2010 SP1<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint 模式的 {2}<br /><br /> SharePoint 2010 產品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集|[安裝適用於 SharePoint 2010 的 Reporting Services SharePoint 模式](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|至少建立一個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式||  
|備份 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料庫||  
|備份 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 加密金鑰||  
|還原 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料庫和加密金鑰||  
|將所有 Web 應用程式對應至新的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]服務應用程式|The new installation <bpt id="p1">**</bpt>is now functional<ept id="p1">**</ept>|  
|移除舊伺服器上的整合 URL。|從 SharePoint 管理中心的 **[一般應用程式設定]** 頁面上，按一下 **[Reporting Services 整合]** 。|  
|視需要從舊安裝解除安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。||  
  
## <a name="next-steps"></a>後續步驟  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services sharepoint 模式安裝&#40;sharepoint 2010 和 SharePoint 2013&#41; ](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)   
 [在 SharePoint 2010 伺服器陣列中使用 SQL SERVER BI 功能的指引](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)   
 [支援的 SharePoint 和 Reporting Services 伺服器與增益集&#40;的組合 SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
  
