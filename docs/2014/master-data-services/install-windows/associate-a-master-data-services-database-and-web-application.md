---
title: 建立 Master Data Services 資料庫與 Web 應用程式的關聯 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: ccb25672-f71d-4135-b548-f50eb45d8fa5
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: c6d507a2471b363cd55eea75e20128ef18f354dd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62924211"
---
# <a name="associate-a-master-data-services-database-and-web-application"></a>建立 Master Data Services 資料庫與 Web 應用程式的關聯
  將 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式與 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫產生關聯，以指定要用於 Web 作業的資料庫。  
  
## <a name="prerequisites"></a>先決條件  
  
-   [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 必須安裝在本機電腦上。 如需詳細資訊，請參閱 [安裝 Master Data Services](install-master-data-services.md)。  
  
-   必須存在本機 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式。 如需詳細資訊，請參閱[建立主資料管理員 Web 應用程式 &#40;Master Data Services&#41;](create-a-master-data-manager-web-application-master-data-services.md)。  
  
-   本機或遠端 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫必須存在。 如需詳細資訊，請參閱 [建立 Master Data Services 資料庫](create-a-master-data-services-database.md)。  
  
### <a name="to-associate-a-master-data-services-database-and-web-application"></a>將 Master Data Services 資料庫與 Web 應用程式產生關聯  
  
1.  開啟 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
2.  按一下左窗格中的 **[Web 組態]**。  
  
3.  在 [Web 組態] 頁面的 [Web 應用程式] 底下，從 [網站] 清單中選取包含您的 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式之網站。  
  
4.  在 [Web 應用程式] 方塊中，選取主控 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 的 Web 應用程式。  
  
5.  在 [將應用程式與資料庫產生關聯] 底下，按一下 [選取]。 [連接到資料庫] 對話方塊隨即開啟。  
  
6.  為主控 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體指定連接資訊，然後按一下 [連接]。  
  
7.  從 [Master Data Services 資料庫] 清單，選取要與 Web 應用程式產生關聯的資料庫，然後按一下 [確定]。  
  
8.  確認 [將應用程式與資料庫產生關聯] 底下的執行個體和資料庫資訊都正確無誤，然後按一下 [套用]。  
  
## <a name="next-steps"></a>後續步驟  
  
-   建立 Web 應用程式時，會自動啟用對 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web 服務的程式設計存取。 為了讓開發人員可存取服務中繼資料，輕鬆地為程式設計存取產生 Proxy 類別，啟用中繼資料發佈。 如需詳細資訊，請參閱 [建立主資料管理員 Web 服務 Proxy 類別](../develop/create-master-data-manager-web-service-proxy-classes.md)。  
  
-   將使用者和群組加入至 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]。 如果沒有使用者或群組已獲授權存取 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]，您必須使用 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 系統管理員認證來開啟 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../administrators-master-data-services.md) (管理員 (Master Data Services)) 和 [Users and Groups &#40;Master Data Services&#41;](../users-and-groups-master-data-services.md) (使用者和群組 (Master Data Services))。  
  
## <a name="see-also"></a>另請參閱  
 [安裝 Master Data Services](install-master-data-services.md)   
 [Web 組態頁面 &#40;Master Data Services 組態管理員&#41;](../web-configuration-page-master-data-services-configuration-manager.md)  
  
  
