---
title: 支援的 SharePoint 和 Reporting Services 伺服器組合 | Microsoft Docs
ms.date: 07/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.topic: conceptual
helpviewer_keywords:
- SharePoint mode
- add-in for sharepoint
- rsSharePoint
ms.assetid: dc6a3372-db26-43f0-b7aa-f725acc635c2
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: f22aed510bf6c5a34d4c4c2a79db7d0f3a56bfe2
ms.sourcegitcommit: 182d77997133a6e4ee71e7a64b4eed6609da0fba
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2018
ms.locfileid: "50051120"
---
# <a name="supported-combinations-of-sharepoint-and-reporting-services-server"></a>支援的 SharePoint 與 Reporting Services 伺服器組合

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

針對以 SharePoint 模式安裝的 SQL Server Reporting Services 報表伺服器，您必須具備在 SharePoint 伺服器上安裝之 SharePoint 產品的適用 SharePoint 版本和 SQL Server Reporting Services 增益集 (rsSharePoint.msi)。 本主題摘要所支援的組合。

> [!NOTE]
> SQL Server 2016 後即不再提供 Reporting Services 與 SharePoint 的整合。

## <a name="supported-combinations-of-sharepoint-and-reporting-services-components"></a>支援的 SharePoint 與 Reporting Services 元件組合

 下表摘要說明支援的報表伺服器、適用 SharePoint 產品的 Reporting Services 增益集，以及 SharePoint 產品的組合。 未列在下表中的組合不受支援

### <a name="supported-combinations"></a>支援的組合

||報表伺服器|增益集|SharePoint 版本|
|-|-------------------|-------------|------------------------|
|1|SQL Server 2016|SQL Server 2016|SharePoint 2016|
|2|SQL Server 2016|SQL Server 2016|SharePoint 2013|
|3|SQL Server 2014|SQL Server 2014|SharePoint 2013|
|4|SQL Server 2014|SQL Server 2014|SharePoint 2010|
|5|SQL Server 2012 SP3|SQL Server 2014 與 SQL Server 2012 SP3|SharePoint 2013|
|6|SQL Server 2012 SP2|SQL Server 2014 與 SQL Server 2012 SP2|SharePoint 2013|
|7|SQL Server 2012 SP1|SQL Server 2014 與 SQL Server 2012 SP1|SharePoint 2013|
|8|SQL Server 2012 與 SQL Server 2012 SP1*|SQL Server 2014|SharePoint 2010|
|9|SQL Server 2012|SQL Server 2012|SharePoint 2010|
|10|SQL Server 2008 R2|SQL Server 2014|SharePoint 2010|
|11|SQL Server 2008 R2|SQL Server 2012 與 SQL Server 2012 SP1 或更新版本|SharePoint 2010|
|12|SQL Server 2008 R2|SQL Server 2008 R2|SharePoint 2010|
|13|SQL Server 2008 R2|SQL Server 2008 SP2|SharePoint 2007|
|14|SQL Server 2008 SP2|SQL Server 2008 R2|SharePoint 2010|
|15|SQL Server 2008 SP2|SQL Server 2008 與 SQL Server 2008 SP2|SharePoint 2007|

 *例外狀況：不支援 Power View 整合。

 如需詳細資訊，請參閱 [尋找適用於 SharePoint 產品之 Reporting Services 增益集的位置](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)。  

 **其他考量：**

- 請務必升級伺服器陣列內的所有 SharePoint 伺服器。 這包括應用程式和 Web 前端伺服器。

- SharePoint 2016 支援 (包括 Power View 整合) 需要 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集版的 SQL Server 2016 或更新版本。

- SharePoint 2013 支援 (包括 Power View 整合) 需要 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集版的 SQL Server 2012 SP1 或更新版本。

- Power View 是在 SQL Server 2012 引進。 因此，Power View 與 SharePoint 2010 的整合需要 SQL Server 2012 或更新版本的增益集。

- SQL Server 2012 (或更新版本) 報表伺服器不支援 SQL Server 2008 R2 增益集。 SharePoint 2010 必要條件安裝程式會自動安裝 SQL Server 2008 R2 增益集。 在安裝較新版本的增益集之前必須先解除安裝。 不支援就地升級增益集。

- **升級：** 已安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集的 SharePoint 2010 無法就地升級至 SharePoint 2013。 SharePoint 2013 需要 SQL Server 2012 SP1 或更新版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集與報表伺服器。 如需升級的詳細資訊，請參閱 [升級和移轉 Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)。

## <a name="next-steps"></a>後續步驟

 [尋找適用於 SharePoint 產品之 Reporting Services 增益集的位置](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)   
 [安裝 SQL Server 2016 的硬體與軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
