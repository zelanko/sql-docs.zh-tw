---
title: "Web 組態頁面 (Master Data Services 組態管理員) | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.mds.configmanager.webconfigpg.f1
ms.assetid: 7b900778-0169-4e42-9faf-98dc1c01313e
caps.latest.revision: 10
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: b382066dbac55174763e4c32ff4360de9a5026fd
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="web-configuration-page-master-data-services-configuration-manager"></a>Web 組態頁面 (Master Data Services 組態管理員)
  使用 [Web 組態] 頁面來設定網站和 Web 應用程式。 您也可以啟用 Data Quality Services。  
  
## <a name="configure-the-web-application"></a>設定 Web 應用程式  
  
|控制項名稱|說明|  
|------------------|-----------------|  
|**網站**|建立新網站、選取預設網站，或選取其他可用的網站 (如有列出)。 此清單會顯示本機電腦上的 Internet Information Services (IIS) 中所定義的網站。 建立新網站時，會自動建立新的 Web 應用程式。 選取預設或其他現有的網站時，您必須手動建立應用程式。|  
|**Web 應用程式**|選取要進行組態設定的 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式。 這個方塊只會顯示選定網站中的 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式。<br /><br /> 如果未顯示任何項目，請按一下 [建立] 來建立網站。|  
|**建立**|開啟 **[建立 Web 應用程式]** 對話方塊，您可以從這個對話方塊建立選定網站中的 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式。 只有當選取的網站沒有任何根 Web 應用程式設定為 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式時，這個按鈕才會啟用。|  
  
## <a name="associate-application-with-database"></a>將應用程式與資料庫產生關聯  
  
|控制項名稱|說明|  
|------------------|-----------------|  
|**Select**|開啟 **[連接到伺服器]** 對話方塊，您可以從這裡連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體，並選取要與選定 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 應用程式產生關聯的 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 資料庫。|  
|**SQL Server 執行個體**|顯示主控 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫的選定 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 執行個體名稱。 在您連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體並選取資料庫之前，這會是空白的。|  
|**資料庫**|顯示與選定 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 應用程式相關聯的 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 資料庫名稱。 在您連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體並選取資料庫之前，這會是空白的。|  
  
## <a name="enable-dqs-integration"></a>啟用 DQS 整合  
  
|控制項名稱|說明|  
|------------------|-----------------|  
|**啟用與 Data Quality Services 的整合**|選取此選項可啟用 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]中所提供的 Data Quality 功能。 如需相關資訊，請參閱 [Enable Data Quality Services Integration with Master Data Services](../master-data-services/install-windows/enable-data-quality-services-integration-with-master-data-services.md)。|  
  
## <a name="see-also"></a>另請參閱  
[Master Data Services 安裝和組態](../master-data-services/master-data-services-installation-and-configuration.md) [Web 應用程式需求 &#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md)   
 [建立主資料管理員 Web 應用程式 &#40;Master Data Services&#41;](../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  

