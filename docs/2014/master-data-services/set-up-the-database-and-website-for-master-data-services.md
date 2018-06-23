---
title: 資料庫與網站設定 Master Data services |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.mds.configmanager.general.f1
ms.assetid: d50863e7-50d9-4ab8-aabb-fd68e2d132a1
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 09e3e92d20182be2feb1c357cc1d3f518c55e5ad
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133721"
---
# <a name="set-up-the-database-and-website-for-master-data-services"></a>設定 Master Data Services 的資料庫與網站
  使用[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]設定資料庫與網站[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)](MDS)  
  
 若要設定資料庫與網站，請完成下列工作。  
  
1.  建立資料庫，使用**資料庫組態**頁面[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]。  
  
     如需資訊，請參閱[資料庫組態頁面&#40;Master Data Services 組態管理員&#41;](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md)和[建立資料庫精靈&#40;Master Data Services 組態管理員&#41;](../../2014/master-data-services/create-database-wizard-master-data-services-configuration-manager.md).  
  
2.  建立新的網站，選取預設網站，或選取另一個現有的網站，使用**Web 組態**頁面[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]。 然後將 MDS 資料庫與您選取或建立的 Web 應用程式相關聯。  
  
     如需資訊，請參閱[Web 組態頁面&#40;Master Data Services 組態管理員&#41;](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md)和[建立網站對話方塊&#40;Master Data Services 組態管理員&#41;](../../2014/master-data-services/create-website-dialog-box-master-data-services-configuration-manager.md).  
  
3.  （選擇性）啟用與 Data Quality Services 使用的整合**Web 組態**頁面[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]。  
  
     如需詳細資訊，請參閱[Web 組態頁面&#40;Master Data Services 組態管理員&#41;](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md)和[Enable Data Quality Services Integration with Master Data Services](install-windows/enable-data-quality-services-integration-with-master-data-services.md)。  
  
 您也可以使用[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]指定 web 應用程式和服務與 MDS 資料庫相關聯的設定。 例如，您可以指定載入資料的頻率，或傳送驗證電子郵件的頻率。 如需詳細資訊，請參閱 [系統設定 &#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Master Data Services 資料庫](../../2014/master-data-services/master-data-services-database.md)   
 [主資料管理員 Web 應用程式](../../2014/master-data-services/master-data-manager-web-application.md)  
  
  