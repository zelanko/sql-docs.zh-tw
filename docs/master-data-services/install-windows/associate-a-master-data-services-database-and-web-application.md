---
title: 建立資料庫與 Web 應用程式的關聯
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: ccb25672-f71d-4135-b548-f50eb45d8fa5
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 257928505c1aa95a61151f47c234469158761e89
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728150"
---
# <a name="associate-a-master-data-services-database-and-web-application"></a>建立 Master Data Services 資料庫與 Web 應用程式的關聯

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  將 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式與 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫產生關聯，以指定要用於 Web 作業的資料庫。  
  
## <a name="prerequisites"></a>必要條件  
  
-   [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 必須安裝在本機電腦上。 如需詳細資訊，請參閱 [安裝 Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)。  
  
-   必須存在本機 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式。 如需詳細資訊，請參閱[建立主資料管理員 Web 應用程式 &#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)。  
  
-   本機或遠端 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫必須存在。 如需詳細資訊，請參閱 [建立 Master Data Services 資料庫](../../master-data-services/install-windows/create-a-master-data-services-database.md)。  
  
### <a name="to-associate-a-master-data-services-database-and-web-application"></a>將 Master Data Services 資料庫與 Web 應用程式產生關聯  
  
1.  開啟 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
2.  按一下左窗格中的 **[Web 組態]** 。  
  
3.  在 [Web 組態] 頁面的 [Web 應用程式] 底下，從 [網站] 清單中選取包含您的 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式之網站。  
  
4.  在 [Web 應用程式] 方塊中，選取主控 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 的 Web 應用程式。  
  
5.  在 [將應用程式與資料庫產生關聯] 底下，按一下 [選取]。 [連接到資料庫] 對話方塊隨即開啟。  
  
6.  為主控 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 執行個體指定連接資訊，然後按一下 [連接]。  
  
7.  從 [Master Data Services 資料庫] 清單，選取要與 Web 應用程式產生關聯的資料庫，然後按一下 [確定]。  
  
8.  確認 [將應用程式與資料庫產生關聯] 底下的執行個體和資料庫資訊都正確無誤，然後按一下 [套用]。  
  
## <a name="next-steps"></a>後續步驟  
  
-   建立 Web 應用程式時，會自動啟用對 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web 服務的程式設計存取。 為了讓開發人員可存取服務中繼資料，輕鬆地為程式設計存取產生 Proxy 類別，啟用中繼資料發佈。 如需詳細資訊，請參閱 [建立主資料管理員 Web 服務 Proxy 類別](../../master-data-services/develop/create-master-data-manager-web-service-proxy-classes.md)。  
  
-   將使用者和群組加入至 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]。 如果沒有使用者或群組已獲授權存取 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]，您必須使用 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 系統管理員認證來開啟 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services)) 和 [Users and Groups &#40;Master Data Services&#41;](../../master-data-services/users-and-groups-master-data-services.md) (使用者和群組 (Master Data Services))。  
  
## <a name="see-also"></a>另請參閱  
 [安裝 Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)   
 [Web 組態頁面 &#40;Master Data Services 組態管理員&#41;](../../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)  
  
  
