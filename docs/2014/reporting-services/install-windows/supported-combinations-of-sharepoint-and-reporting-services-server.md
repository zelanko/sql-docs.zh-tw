---
title: 支援的 SharePoint 與 Reporting Services 伺服器與增益集 (SQL Server 2014) 組合 |Microsoft 文件
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SharePoint mode
- add-in for sharepoint
ms.assetid: dc6a3372-db26-43f0-b7aa-f725acc635c2
caps.latest.revision: 27
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 4aaaa578f438beabd9c9c661eaaf852971545695
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36144897"
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
|@shouldalert|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2013|是|  
|2|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|是|  
|3|[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 和 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2013|是|  
|4|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|是<br /><br /> 例外狀況：Power View 整合不受支援。|  
|5|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|SharePoint 2010|是|  
|6|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|是|  
|7|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2010|是|  
|8|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|SharePoint 2010|是|  
|9|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|是|  
|10|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] R2|SharePoint 2010|是|  
|11|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|是|  
  
 如需有關[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]功能和報表伺服器模式，請參閱[Reporting Services 報表伺服器](../reporting-services-report-server.md)。  
  
 **其他注意事項：**  
  
-   SharePoint 2013 支援 (包括 Power View 整合) 需要 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集版的 SQL Server 2012 SP1 或更新版本。  
  
-   Power View 已在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中引進。 因此，Power View 與 SharePoint 2010 的整合需要 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或更新版本的增益集。  
  
-   SQL Server 2012 (或更新版本) 報表伺服器不支援 SQL Server 2008 R2 增益集。 SharePoint 2010 必要條件安裝程式會自動安裝 SQL Server 2008 R2 增益集。 在安裝較新版本的增益集之前必須先解除安裝。 不支援就地升級增益集。  
  
-   **升級：** 已安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集的 SharePoint 2010 無法就地升級至 SharePoint 2013。 SharePoint 2013 需要 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 或更新版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集與報表伺服器。 如需有關升級的詳細資訊，請參閱[升級和移轉 Reporting Services](upgrade-and-migrate-reporting-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [如何尋找 Reporting Services 增益集適用於 SharePoint 產品](where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [SQL Server 2014 各版本所支援的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [升級和移轉 Reporting Services](upgrade-and-migrate-reporting-services.md)  
  
  