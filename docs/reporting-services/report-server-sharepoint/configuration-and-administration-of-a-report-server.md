---
title: 報表伺服器的設定及管理 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server-sharepoint
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 7959539dde52351bc9679b9b4629e2d1a4105562
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38049136"
---
# <a name="configuration-and-administration-of-a-sql-server-reporting-services-ssrs-report-server"></a>設定和管理 SQL Server Reporting Services (SSRS) 報表伺服器

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

SQL Server Reporting Services 是一種伺服器報表平台，提供齊全的現成工具與服務，協助您建立、部署和管理您組織的報表，並提供可讓您擴充和自訂報表功能的程式設計功能。 您可以將報表環境與 SharePoint 產品整合，以體驗使用 SharePoint 網站所提供之共同作業環境的優點。

> [!NOTE]
> SQL Server 2016 後即不再提供 Reporting Services 與 SharePoint 的整合。

使用下列章節可幫助您更佳了解概念、部署案例、程序等等，讓您將 Reporting Services 環境與 SharePoint 產品或技術整合：  
  
-   SharePoint 文件庫中的功能表選項  
  
    -   [SharePoint 使用者的資料警示管理員](../../reporting-services/data-alert-manager-for-sharepoint-users.md)  
  
    -   [建立及管理 SharePoint 模式報表伺服器的訂閱](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)  
  
    -   [從 SharePoint 網站更新報表資料來源的認證](../../reporting-services/report-data/update-credentials-in-report-data-sources-from-a-sharepoint-site.md)  
  
    -   [管理共用資料集](../../reporting-services/report-data/manage-shared-datasets.md)  
  
    -   [在已發行的報表上設定參數 &#40;SharePoint 整合模式中的 Reporting Services&#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md)  
  
    -   [設定處理選項 &#40;SharePoint 整合模式的 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)  
  
-   [Reporting Services 網站集合功能](../../reporting-services/report-server-sharepoint/site-collection-features-reporting-services.md)  
  
-   [在 SharePoint 中啟用報表伺服器和 Power View 整合功能](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)  
  
-   [Reporting Services 網站設定和網站功能 &#40;SharePoint 模式&#41;](../../reporting-services/report-server-sharepoint/site-settings-and-features-reporting-services.md)  
  
-   [在 SharePoint 管理中心啟動報表伺服器檔案同步處理功能](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)  
  
-   [將 Reporting Services 內容類型加入至 SharePoint 文件庫](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)  
  
-   [在報告檢視器中的本機模式與連線模式報表 &#40;SharePoint 模式的 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md)  
  
-   [將文件上傳到 SharePoint 文件庫 &#40;SharePoint 模式的 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)  
  
-   [設定處理選項 &#40;SharePoint 整合模式的 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)  
  
 如需更多的 Reporting Services 一般資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的 [Reporting Service](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)。 如需有關其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件、工具和資源的詳細資訊，請參閱《 [SQL Server 線上叢書](../../sql-server/sql-server-technical-documentation.md)》。  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
