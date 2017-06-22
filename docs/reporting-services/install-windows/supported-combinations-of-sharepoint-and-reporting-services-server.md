---
title: "支援的 SharePoint 與 Reporting Services 伺服器組合 |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 10/07/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SharePoint mode
- add-in for sharepoint
- rsSharePoint
ms.assetid: dc6a3372-db26-43f0-b7aa-f725acc635c2
caps.latest.revision: 39
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 2e66cac836de44e8d2a9f23d88a600daaa26c0d1
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="supported-combinations-of-sharepoint-and-reporting-services-server"></a>支援的 SharePoint 與 Reporting Services 伺服器組合
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

  針對以 SharePoint 模式安裝的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器，您必須具備在 SharePoint 伺服器上安裝之 SharePoint 產品的適用 SharePoint 版本和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集 (rsSharePoint.msi)。  本主題摘要所支援的組合。  
  
## <a name="supported-combinations-of-sharepoint-and-reporting-services-components"></a>支援的 SharePoint 與 Reporting Services 元件組合  
 下表摘要說明支援的報表伺服器、適用 SharePoint 產品的 Reporting Services 增益集，以及 SharePoint 產品的組合。 未列在下表中的組合不受支援  
  
### <a name="supported-combinations"></a>支援的組合  
  
||報表伺服器|增益集|SharePoint 版本|  
|-|-------------------|-------------|------------------------|  
|1|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|SharePoint 2016|  
|2|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|SharePoint 2013|  
|3|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2013|  
|4|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|  
|5|SQL Server 2012 SP3|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 和 SQL Server 2012 SP3|SharePoint 2013|  
|6|SQL Server 2012 SP2|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 和 SQL Server 2012 SP2|SharePoint 2013|  
|7|[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 和 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2013|  
|8|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]*|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|  
|9|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|SharePoint 2010|  
|10|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|  
|11|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2010|  
|12|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|SharePoint 2010|  
|13|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|  
|14|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] R2|SharePoint 2010|  
|15|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|  
  
 *例外狀況：不支援 Power View 整合。  
  
 如需詳細資訊，請參閱 [尋找適用於 SharePoint 產品之 Reporting Services 增益集的位置](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)。  
  
 **其他注意事項：**  

- 請務必升級伺服器陣列內的所有 SharePoint 伺服器。 這包括應用程式和 Web 前端伺服器。

-   SharePoint 2016 支援 (包括 Power View 整合) 需要 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集版的 SQL Server 2016 或更新版本。  

-   SharePoint 2013 支援 (包括 Power View 整合) 需要 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集版的 SQL Server 2012 SP1 或更新版本。  
  
-   Power View 已在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中引進。 因此，Power View 與 SharePoint 2010 的整合需要 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或更新版本的增益集。  
  
-   SQL Server 2012 (或更新版本) 報表伺服器不支援 SQL Server 2008 R2 增益集。 SharePoint 2010 必要條件安裝程式會自動安裝 SQL Server 2008 R2 增益集。 在安裝較新版本的增益集之前必須先解除安裝。 不支援就地升級增益集。  
  
-   **升級：** 已安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集的 SharePoint 2010 無法就地升級至 SharePoint 2013。 SharePoint 2013 需要 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 或更新版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集與報表伺服器。 如需升級的詳細資訊，請參閱 [升級和移轉 Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [尋找適用於 SharePoint 產品之 Reporting Services 增益集的位置](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)   
 [安裝 SQL Server 2016 的硬體與軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
  


