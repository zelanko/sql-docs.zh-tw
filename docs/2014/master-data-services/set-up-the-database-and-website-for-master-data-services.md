---
title: 設定 Master Data Services 資料庫和網站 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.general.f1
ms.assetid: d50863e7-50d9-4ab8-aabb-fd68e2d132a1
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 478dea9095fe22a437aecf138c22374b5a70885b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66054097"
---
# <a name="set-up-the-database-and-website-for-master-data-services"></a>設定 Master Data Services 的資料庫與網站
  使用 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 設定 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) 的資料庫與網站  
  
 若要設定資料庫與網站，請完成下列工作。  
  
1.  使用 **中的 [資料庫組態]**[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]頁面，建立資料庫。  
  
     如需資訊，請參閱[資料庫組態頁面&#40;Master Data Services 組態管理員&#41;](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md)並[建立資料庫精靈 &#40;Master Data Services 組態管理員&#41;](../../2014/master-data-services/create-database-wizard-master-data-services-configuration-manager.md).  
  
2.  使用 **中的 [Web 組態]**[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]頁面，建立新的網站、選取預設網站，或選取另一個現有網站。 然後將 MDS 資料庫與您選取或建立的 Web 應用程式相關聯。  
  
     如需資訊，請參閱[Web 組態頁面&#40;Master Data Services 組態管理員&#41;](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md)並[建立網站 對話方塊中&#40;Master Data Services 組態管理員&#41;](../../2014/master-data-services/create-website-dialog-box-master-data-services-configuration-manager.md).  
  
3.  (選擇性) 使用 **中的 [Web 組態]**[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]頁面，啟用與 Data Quality Services 的整合。  
  
     如需詳細資訊，請參閱 < [Web 組態頁面&#40;Master Data Services 組態管理員&#41;](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md)並[使用 Master Data Services 啟用 Data Quality Services 整合](install-windows/enable-data-quality-services-integration-with-master-data-services.md)。  
  
 您也可以使用 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 指定 Web 應用程式與 MDS 資料庫相關聯之服務的設定。 例如，您可以指定載入資料的頻率，或傳送驗證電子郵件的頻率。 如需詳細資訊，請參閱 [系統設定 &#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Master Data Services 資料庫](../../2014/master-data-services/master-data-services-database.md)   
 [主資料管理員 Web 應用程式](../../2014/master-data-services/master-data-manager-web-application.md)  
  
  
