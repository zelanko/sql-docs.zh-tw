---
title: Reporting Services SharePoint 模式安裝 （SharePoint 2010 和 SharePoint 2013） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- default configuration [Reporting Services]
- installing Reporting Services, SharePoint integrated mode
- installation options [Reporting Services]
ms.assetid: ac6cba68-2665-4a39-8fa3-cb7d7e6723c0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ef049b4ded6408e651d5ec2c3db99c10bf7c27b6
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108770"
---
# <a name="reporting-services-sharepoint-mode-installation-sharepoint-2010-and-sharepoint-2013"></a>Reporting Services SharePoint 模式安裝 (SharePoint 2010 和 SharePoint 2013)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 在 SharePoint 模式是伺服器元件，可提供報表產生及傳遞，根據集合[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[msCoName](../../includes/msconame-md.md)]SharePoint 產品。  
  
 在 SharePoint 模式中執行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，可提供 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 與資料警示功能。 如需有關 SharePoint 模式中功能的詳細資訊，請參閱"功能支援與行為差異的伺服器模式 > 一節中[Reporting Services 報表伺服器](../reporting-services-report-server.md)  
  
 SharePoint 模式中的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 需要兩項基本安裝：  
  
|安裝|描述|  
|------------------|-----------------|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]增益集適用於 SharePoint 產品。|增益集會在 SharePoint 網站前端伺服器上，安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用者介面 (UI) 頁面與功能。 使用者介面包含 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]、SharePoint 管理中心內的管理頁面、SharePoint 文件庫中使用的功能頁面，以及 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料警示頁面。|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]以 SharePoint 模式安裝的報表伺服器|報表伺服器處理資料與報表的處理程序、訂閱的呈現方式，以及資料警示處理程序。 SharePoint 模式報表伺服器會架構與安裝為 SharePoint 共用服務。|  
  
 使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝媒體，安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 如需進階的部署案例的指示，請參閱[部署檢查清單：Reporting Services、 Power View 及 PowerPivot for SharePoint](../../sql-server/install/deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md)和[部署檢查清單：將 Reporting Services 安裝至現有的 SharePoint 伺服器陣列](../../sql-server/install/deployment-checklist-install-reporting-services-existing-sharepoint-farm.md)。  
  
## <a name="in-this-section"></a>本節內容  
 [支援的 SharePoint 與 Reporting Services 伺服器與增益集組合&#40;SQL Server 2014&#41;](supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
 [安裝適用於 SharePoint 2013 的 Reporting Services SharePoint 模式](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)  
  
 [安裝適用於 SharePoint 2010 的 Reporting Services SharePoint 模式](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
 [安裝或解除安裝 Reporting Services 增益集，適用於 SharePoint &#40;SharePoint 2010 和 SharePoint 2013&#41;](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
 [尋找適用於 SharePoint 產品之 Reporting Services 增益集的位置](where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
 [將其他報表伺服器加入至伺服器陣列 &#40;SSRS 向外延展&#41;](add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
 [將其他 Reporting Services Web 前端加入至伺服器陣列](add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 [設定 Reporting Services 服務應用程式的電子郵件 &#40;SharePoint 2010 和 SharePoint 2013&#41;](configure-e-mail-for-a-reporting-services-service-application.md)  
  
 [SSRS 服務應用程式的佈建訂閱及警示](provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  
  
 [Claims to Windows Token 服務的&#40;C2WTS&#41;和 Reporting Services](../../sql-server/install/claims-to-windows-token-service-c2wts-and-reporting-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料警示架構和工作流程](../reporting-services-data-alerts.md#AlertingWF)   
 [警示系統管理員的資料警示管理員](../data-alert-manager-for-alerting-administrators.md)  
  
  
