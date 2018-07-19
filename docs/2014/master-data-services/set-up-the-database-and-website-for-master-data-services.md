---
title: 設定 Master Data Services 資料庫和網站 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.general.f1
ms.assetid: d50863e7-50d9-4ab8-aabb-fd68e2d132a1
caps.latest.revision: 7
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fe3be8de50ad6752f5edb4f1ea888c172338aaa2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37322368"
---
# <a name="set-up-the-database-and-website-for-master-data-services"></a>設定 Master Data Services 的資料庫與網站
  使用[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]若要設定資料庫與網站[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)](MDS)  
  
 若要設定資料庫與網站，請完成下列工作。  
  
1.  建立資料庫，使用**Database Configuration**頁面中[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]。  
  
     如需資訊，請參閱[資料庫組態頁面&#40;Master Data Services 組態管理員&#41;](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md)並[建立資料庫精靈 &#40;Master Data Services 組態管理員&#41;](../../2014/master-data-services/create-database-wizard-master-data-services-configuration-manager.md).  
  
2.  建立新的網站，選取預設的網站，或選取另一個現有的網站，使用**Web 組態**頁面中[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]。 然後將 MDS 資料庫與您選取或建立的 Web 應用程式相關聯。  
  
     如需資訊，請參閱[Web 組態頁面&#40;Master Data Services 組態管理員&#41;](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md)並[建立網站 對話方塊中&#40;Master Data Services 組態管理員&#41;](../../2014/master-data-services/create-website-dialog-box-master-data-services-configuration-manager.md).  
  
3.  （選擇性）啟用與 Data Quality Services 使用的整合**Web 組態**頁面中[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]。  
  
     如需詳細資訊，請參閱 < [Web 組態頁面&#40;Master Data Services 組態管理員&#41;](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md)並[使用 Master Data Services 啟用 Data Quality Services 整合](install-windows/enable-data-quality-services-integration-with-master-data-services.md)。  
  
 您也可以使用[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]指定設定的 web 應用程式和 MDS 資料庫與相關聯的服務。 例如，您可以指定載入資料的頻率，或傳送驗證電子郵件的頻率。 如需詳細資訊，請參閱 [系統設定 &#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Master Data Services 資料庫](../../2014/master-data-services/master-data-services-database.md)   
 [主資料管理員 Web 應用程式](../../2014/master-data-services/master-data-manager-web-application.md)  
  
  
