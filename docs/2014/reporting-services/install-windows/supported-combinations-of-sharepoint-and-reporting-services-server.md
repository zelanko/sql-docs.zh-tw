---
title: 支援的 SharePoint 與 Reporting Services 伺服器與增益集 (SQL Server 2014) 組合 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- SharePoint mode
- add-in for sharepoint
ms.assetid: dc6a3372-db26-43f0-b7aa-f725acc635c2
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: b4e1a516f10c15b8e84d80ff91de1aa9d66d8e1b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034099"
---
# <a name="supported-combinations-of-sharepoint-and-reporting-services-server-and-add-in-sql-server-2014"></a>支援的 SharePoint 和 Reporting Services 伺服器與增益集 (SQL Server 2014) 的組合
  可以利用 SharePoint 模式安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器，並且與 SharePoint 部署相整合。 在報表伺服器、適用 SharePoint 之 Reporting Services 增益集，以及 SharePoint 產品的所有組合中，並不支援所有功能。 本主題摘要所支援的組合。 在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 中，以下的組合會產生整合：  
  
-   為 SharePoint 模式所設定的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器版本。  
  
-   SharePoint 產品。  
  
-   安裝在 SharePoint 伺服器上，SharePoint 產品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; SharePoint 2010 &#124; SharePoint 2007|  
  
## <a name="supported-combinations-of-sharepoint-and-reporting-services-components"></a>支援的 SharePoint 與 Reporting Services 元件組合  
 下表摘要說明支援的報表伺服器、適用 SharePoint 產品的 Reporting Services 增益集，以及 SharePoint 產品的組合。 未列在下表中的組合不受支援  
  
### <a name="supported-combinations"></a>支援的組合  
  
||報表伺服器|增益集|SharePoint 版本|支援|  
|-|-------------------|-------------|------------------------|---------------|  
|1|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2013|是|  
|2|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|是|  
|3|[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 和 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2013|是|  
|4|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|是<br /><br /> Exception:不支援 power view 整合。|  
|5|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|SharePoint 2010|是|  
|6|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|是|  
|7|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2010|是|  
|8|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|SharePoint 2010|是|  
|9|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|是|  
|10|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] R2|SharePoint 2010|是|  
|11|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|是|  
  
 如需詳細資訊[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]功能以及報表伺服器模式，請參閱[Reporting Services 報表伺服器](../reporting-services-report-server.md)。  
  
 **其他注意事項：**  
  
-   SharePoint 2013 支援 (包括 Power View 整合) 需要 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集版的 SQL Server 2012 SP1 或更新版本。  
  
-   Power View 已在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中引進。 因此，Power View 與 SharePoint 2010 的整合需要 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或更新版本的增益集。  
  
-   SQL Server 2012 (或更新版本) 報表伺服器不支援 SQL Server 2008 R2 增益集。 SharePoint 2010 必要條件安裝程式會自動安裝 SQL Server 2008 R2 增益集。 在安裝較新版本的增益集之前必須先解除安裝。 不支援就地升級增益集。  
  
-   **升級：** 使用 SharePoint 2010[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]無法升級增益集安裝，就地升級至 SharePoint 2013。 SharePoint 2013 需要 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 或更新版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集與報表伺服器。 如需升級的詳細資訊，請參閱 [升級和移轉 Reporting Services](upgrade-and-migrate-reporting-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [尋找適用於 SharePoint 產品之 Reporting Services 增益集的位置](where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [SQL Server 2014 各版本所支援的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [升級和移轉 Reporting Services](upgrade-and-migrate-reporting-services.md)  
  
  
