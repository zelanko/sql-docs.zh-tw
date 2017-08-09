---
title: "Reporting Services 網站集合功能 |Microsoft 文件"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e05ae162-a4b2-489d-9853-d6b09414e632
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b68204ab4c9a008db7c43d2c568d1c3ccedbcb7a
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---

# <a name="site-collection-features---reporting-services"></a>網站集合功能-Reporting Services

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式提供了三個 SharePoint 網站集合功能。 這些功能支援一般[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint 模式報表環境、 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]，SQL Server 2016 Reporting Services 增益集，以及管理作業的一項功能[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]在 SharePoint 管理中心內。  
  
## <a name="site-collection-features"></a>網站集合功能  
 下表描述 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 網站集合功能。  
  
|功能|說明|  
|-------------|-----------------|  
|**報表伺服器管理中心功能**|啟用管理與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器之整合的功能。 此功能只在 SharePoint 管理中心網站集合中安裝及使用。<br /><br /> 在安裝適用於 SharePoint 產品的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 增益集後，SharePoint 管理中心網站集合中會自動啟用報表伺服器整合功能。 在某些情況下，您必須手動啟動此功能。 若要啟用報表伺服器功能，請使用 SharePoint 管理中心內 [網站設定] 頁面中的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 頁面。<br /><br /> 適用於 SharePoint 產品的 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集 (含) 以後版本將會在安裝此增益集時，針對所有現有的網站集合啟用報表伺服器整合功能。 此外，新的網站集合將會自動啟用這項功能。|  
|**報表伺服器整合功能**|使用下列方式啟用豐富的報表功能 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]<br /><br /> 此功能預設為使用中。|  
|**Power View 整合功能**|針對 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿與 Analysis Services 表格式資料庫啟用互動式資料瀏覽及視覺化簡報。<br /><br /> 此功能可透過下列資料來源的操作功能表存取：<br /><br /> **.rdlx**<br /><br /> **.rsds**<br /><br /> **.bism** 連線檔案<br /><br /> <br /><br /> 如果 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 未出現在操作功能表中，請確認已啟用 [Power View 整合功能]。<br /><br /> 此功能預設為停用。|  

## <a name="next-steps"></a>後續的步驟

[在 SharePoint 中啟用報表伺服器和 Power View 整合功能](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)   
[站台設定和網站功能 &#40; reporting ServicesSharePoint 模式 &#41;](../../reporting-services/report-server-sharepoint/site-settings-and-features-reporting-services.md)   
[在 SharePoint 管理中心啟動報表伺服器檔案同步處理功能](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
