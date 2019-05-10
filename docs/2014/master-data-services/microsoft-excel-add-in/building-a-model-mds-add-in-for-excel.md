---
title: 建立模型 (適用於 Excel 的 MDS 增益集) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 8ae26ec3-c5d5-4c4f-a810-2951a7454439
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ee3473ba16ad3a03a95065aea94888654db53187
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2019
ms.locfileid: "65479340"
---
# <a name="building-a-model-mds-add-in-for-excel"></a>建立模型 (適用於 Excel 的 MDS 增益集)
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，系統管理員可以執行 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式中的管理功能子集。  
  
 系統管理員可在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 中執行的模型建立工作是：  
  
-   建立實體。 如需實體的詳細資訊，請參閱[實體 &#40;Master Data Services&#41;](../entities-master-data-services.md)。  
  
-   建立所有類型的屬性，包括網域屬性。 如需屬性的詳細資訊，請參閱[屬性 &#40;Master Data Services&#41;](../attributes-master-data-services.md) 和[網域屬性 &#40;Master Data Services&#41;](../domain-based-attributes-master-data-services.md)。  
  
 身為系統管理員，您必須透過使用 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式或 Web 服務來建立模型。 然後您可以使用 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] ，在模型中建立實體和屬性。 如需模型物件的詳細資訊，請參閱[模型 &#40;Master Data Services&#41;](../models-master-data-services.md)。  
  
## <a name="related-tasks"></a>相關工作  
 大多數管理工作仍必須在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式中或透過使用 Web 服務來完成。 下表顯示系統管理員可在 MDS 中使用哪些工具完成工作。  
  
|工作描述|工具|主題|  
|----------------------|----------|-----------|  
|建立模型。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式或 Web 服務|[建立模型 &#40;Master Data Services&#41;](../create-a-model-master-data-services.md)|  
|建立實體。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式、Web 服務或 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|[建立實體 &#40;適用於 Excel 的 MDS 增益集&#41;](create-an-entity-mds-add-in-for-excel.md)|  
|建立網域屬性。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式、Web 服務或 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|[建立網域屬性 &#40;適用於 Excel 的 MDS 增益集&#41;](create-a-domain-based-attribute-mds-add-in-for-excel.md)|  
|建立屬性群組。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式或 Web 服務|[建立屬性群組 &#40;Master Data Services&#41;](../create-an-attribute-group-master-data-services.md)|  
|建立商務規則。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式或 Web 服務|[建立及發行商務規則 &#40;Master Data Services&#41;](../create-and-publish-a-business-rule-master-data-services.md)|  
|建立訂閱檢視。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式或 Web 服務|[建立訂閱檢視&#40;Master Data Services&#41;](../create-a-subscription-view-to-export-data-master-data-services.md)|  
|建立階層。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式或 Web 服務|[建立衍生階層 &#40;Master Data Services&#41;](../create-a-derived-hierarchy-master-data-services.md)<br /><br /> [建立明確階層 &#40;Master Data Services&#41;](../create-an-explicit-hierarchy-master-data-services.md)|  
|建立集合。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式或 Web 服務|[建立集合 &#40;Master Data Services&#41;](../create-a-collection-master-data-services.md)|  
|建立資料的版本。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式或 Web 服務|[鎖定版本 &#40;Master Data Services&#41;](../lock-a-version-master-data-services.md)|  
|部署模型。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式、Web 服務或 MDSModelDeploy 工具。|[使用 MDSModelDeploy 建立模型部署封裝](../create-a-model-deployment-package-by-using-mdsmodeldeploy.md)|  
  
## <a name="related-content"></a>相關內容  
  
-   [模型 &#40;Master Data Services&#41;](../models-master-data-services.md)  
  
-   [實體 &#40;Master Data Services&#41;](../entities-master-data-services.md)  
  
-   [屬性 &#40;Master Data Services&#41;](../attributes-master-data-services.md)  
  
-   [網域屬性 &#40;Master Data Services&#41;](../domain-based-attributes-master-data-services.md)  
  
-   [屬性群組 &#40;Master Data Services&#41;](../attribute-groups-master-data-services.md)  
  
-   [商務規則 &#40;Master Data Services&#41;](../business-rules-master-data-services.md)  
  
-   [將資料匯出&#40;Master Data Services&#41;](../overview-exporting-data-master-data-services.md)  
  
-   [階層 &#40;Master Data Services&#41;](../hierarchies-master-data-services.md)  
  
-   [集合 &#40;Master Data Services&#41;](../collections-master-data-services.md)  
  
-   [版本 &#40;Master Data Services&#41;](../versions-master-data-services.md)  
  
-   [安全性 &#40;Master Data Services&#41;](../security-master-data-services.md)  
  
-   [部署模型 &#40;Master Data Services&#41;](../deploying-models-master-data-services.md)  
  
  
