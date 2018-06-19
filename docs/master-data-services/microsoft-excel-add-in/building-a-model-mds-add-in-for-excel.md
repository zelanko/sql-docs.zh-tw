---
title: 建立模型 (適用於 Excel 的 MDS 增益集) | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8ae26ec3-c5d5-4c4f-a810-2951a7454439
caps.latest.revision: 5
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: ac99d1e032fc2e674696926c426c3477e15a7fef
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35408280"
---
# <a name="building-a-model-mds-add-in-for-excel"></a>建立模型 (適用於 Excel 的 MDS 增益集)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，系統管理員可以執行 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式中的管理功能子集。  
  
 系統管理員可在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 中執行的模型建立工作是：  
  
-   建立實體。 如需實體的詳細資訊，請參閱 [實體 &#40;Master Data Services&#41;](../../master-data-services/entities-master-data-services.md)。  
  
-   建立所有類型的屬性，包括網域屬性。 如需屬性的詳細資訊，請參閱 [屬性 &#40;Master Data Services&#41;](../../master-data-services/attributes-master-data-services.md) 和 [網域屬性 &#40;Master Data Services&#41;](../../master-data-services/domain-based-attributes-master-data-services.md)。  
  
 身為系統管理員，您必須透過使用 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式或 Web 服務來建立模型。 然後您可以使用 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] ，在模型中建立實體和屬性。 如需模型物件的詳細資訊，請參閱 [模型 &#40;Master Data Services&#41;](../../master-data-services/models-master-data-services.md)。  
  
## <a name="related-tasks"></a>相關工作  
 大多數管理工作仍必須在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式中或透過使用 Web 服務來完成。 下表顯示系統管理員可在 MDS 中使用哪些工具完成工作。  
  
|工作描述|工具|主題|  
|----------------------|----------|-----------|  
|建立模型。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式或 Web 服務|[建立模型 &#40;Master Data Services&#41;](../../master-data-services/create-a-model-master-data-services.md)|  
|建立實體。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式、Web 服務或 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|[建立實體 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/create-an-entity-mds-add-in-for-excel.md)|  
|建立網域屬性。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式、Web 服務或 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|[建立網域屬性 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/create-a-domain-based-attribute-mds-add-in-for-excel.md)|  
|建立屬性群組。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式或 Web 服務|[建立屬性群組 &#40;Master Data Services&#41;](../../master-data-services/create-an-attribute-group-master-data-services.md)|  
|建立商務規則。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式或 Web 服務|[建立及發行商務規則 &#40;Master Data Services&#41;](../../master-data-services/create-and-publish-a-business-rule-master-data-services.md)|  
|建立訂閱檢視。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式或 Web 服務|[建立訂閱檢視以匯出資料 &#40;Master Data Services&#41;](../../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)|  
|建立階層。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式或 Web 服務|[建立衍生階層 &#40;Master Data Services&#41;](../../master-data-services/create-a-derived-hierarchy-master-data-services.md)<br /><br /> [建立明確階層 &#40;Master Data Services&#41;](../../master-data-services/create-an-explicit-hierarchy-master-data-services.md)|  
|建立集合。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式或 Web 服務|[建立集合 &#40;Master Data Services&#41;](../../master-data-services/create-a-collection-master-data-services.md)|  
|建立資料的版本。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式或 Web 服務|[鎖定版本 &#40;Master Data Services&#41;](../../master-data-services/lock-a-version-master-data-services.md)|  
|部署模型。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式、Web 服務或 MDSModelDeploy 工具。|[使用 MDSModelDeploy 建立模型部署封裝](../../master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md)|  
  
## <a name="related-content"></a>相關內容  
  
-   [模型 &#40;Master Data Services&#41;](../../master-data-services/models-master-data-services.md)  
  
-   [實體 &#40;Master Data Services&#41;](../../master-data-services/entities-master-data-services.md)  
  
-   [屬性 &#40;Master Data Services&#41;](../../master-data-services/attributes-master-data-services.md)  
  
-   [網域屬性 &#40;Master Data Services&#41;](../../master-data-services/domain-based-attributes-master-data-services.md)  
  
-   [屬性群組 &#40;Master Data Services&#41;](../../master-data-services/attribute-groups-master-data-services.md)  
  
-   [商務規則 &#40;Master Data Services&#41;](../../master-data-services/business-rules-master-data-services.md)  
  
-   [概觀：匯出資料 &#40;Master Data Services&#41;](../../master-data-services/overview-exporting-data-master-data-services.md)  
  
-   [階層 &#40;Master Data Services&#41;](../../master-data-services/hierarchies-master-data-services.md)  
  
-   [集合 &#40;Master Data Services&#41;](../../master-data-services/collections-master-data-services.md)  
  
-   [版本 &#40;Master Data Services&#41;](../../master-data-services/versions-master-data-services.md)  
  
-   [安全性 &#40;Master Data Services&#41;](../../master-data-services/security-master-data-services.md)  
  
-   [部署模型 &#40;Master Data Services&#41;](../../master-data-services/deploying-models-master-data-services.md)  
  
  
