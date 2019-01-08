---
title: Web 組態頁面 (Master Data Services 組態管理員) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.webconfigpg.f1
ms.assetid: 7b900778-0169-4e42-9faf-98dc1c01313e
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: f45eef12a81ada02a26a0f4c2318523de31cbf0d
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53357768"
---
# <a name="web-configuration-page-master-data-services-configuration-manager"></a>Web 組態頁面 (Master Data Services 組態管理員)
  使用 **[Web 組態]** 頁面建立新的網站或 Web 應用程式。 當您選取 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式後，可以指定應用程式的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫，並啟用 Data Quality Services。  
  
## <a name="configure-the-web-application"></a>設定 Web 應用程式  
  
|控制項名稱|描述|  
|------------------|-----------------|  
|**網站**|建立新網站、選取預設網站，或選取其他可用的網站 (如有列出)。 此清單會顯示本機電腦上的 Internet Information Services (IIS) 中所定義的網站。 建立新網站時，會自動建立新的 Web 應用程式。 選取預設或其他現有的網站時，您必須手動建立應用程式。|  
|**Web 應用程式**|選取要進行組態設定的 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式。 這個方塊只會顯示選定網站中的 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式。<br /><br /> 如果沒有顯示任何項目，按一下 **[建立應用程式]** 來建立網站。|  
|**建立應用程式**|開啟 **[建立 Web 應用程式]** 對話方塊，您可以從這個對話方塊建立選定網站中的 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式。 只有當選取的網站沒有任何根 Web 應用程式設定為 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式時，這個按鈕才會啟用。|  
  
## <a name="associate-application-with-database"></a>將應用程式與資料庫產生關聯  
  
|控制項名稱|描述|  
|------------------|-----------------|  
|**Select**|開啟 **[連接到伺服器]** 對話方塊，您可以從這裡連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體，並選取要與選定 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 應用程式產生關聯的 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 資料庫。|  
|**SQL Server 執行個體**|顯示主控 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫的選定 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 執行個體名稱。 在您連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體並選取資料庫之前，這會是空白的。|  
|**[資料庫備份]**|顯示與選定 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 應用程式相關聯的 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 資料庫名稱。 在您連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體並選取資料庫之前，這會是空白的。|  
  
## <a name="enable-dqs-integration"></a>啟用 DQS 整合  
  
|控制項名稱|描述|  
|------------------|-----------------|  
|**啟用與 Data Quality Services 的整合**|選取此選項可啟用 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]中所提供的 Data Quality 功能。 如需相關資訊，請參閱 [啟用 Data Quality Services 與 Master Data Services 的整合](install-windows/enable-data-quality-services-integration-with-master-data-services.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [設定 Master Data Services 資料庫和網站](../../2014/master-data-services/set-up-the-database-and-website-for-master-data-services.md)   
 [Web 應用程式需求&#40;Master Data Services&#41;](install-windows/web-application-requirements-master-data-services.md)   
 [建立主資料管理員 Web 應用程式 &#40;Master Data Services&#41;](install-windows/create-a-master-data-manager-web-application-master-data-services.md)   
 [MDS 2014 與 「 服務無法使用 」 錯誤](https://blogs.msdn.com/b/womeninanalytics/archive/2015/08/19/mds-2014-and-service-unavailable-error.aspx)  
  
  
