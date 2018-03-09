---
title: "建立主資料管理員 Web 應用程式 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 241d46d7-8008-47f6-bebd-0dfff1cc856a
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 475d655c3accf4c25afe13c615adc210575e2975
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/05/2018
---
# <a name="create-a-master-data-manager-web-application-master-data-services"></a>建立主資料管理員 Web 應用程式 (Master Data Services)
  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式提供了一個介面，可讓使用者處理主資料並且讓管理員設定及管理 MDS。  
  
 網站中一定要包含 Web 應用程式。 若要建立 Web 應用程式，您必須：  
  
-   使用預設網站，然後建立 Web 應用程式；  
  
-   使用現有網站，然後建立 Web 應用程式；或者  
  
-   建立新網站，這樣就會自動建立 Web 應用程式。  
  
 建立 Web 應用程式之後，將它與 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫產生關聯。  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   如需主控此 Web 應用程式之電腦需求的資訊，請參閱 [Web 應用程式需求 &#40;Master Data Services&#41;](../../master-data-services/install-windows/web-application-requirements-master-data-services.md)。  
  
## <a name="to-create-a-master-data-manager-web-application-in-a-new-website"></a>在新網站上建立主資料管理員 Web 應用程式  
 當您建立新網站時，根 Web 應用程式會是 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式。 此 Web 應用程式也會加入至新的應用程式集區。  
  
> [!NOTE]  
>  如果您依照此程序進行，將無法指定 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式的虛擬路徑和別名。 如果要指定 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]的虛擬路徑及別名，則必須在尚未設定為 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式的現有網站上建立 Web 應用程式。  
  
 此外， [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 只支援建立具有 HTTP 繫結的網站。 若要加入 HTTPS 繫結，請在 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 中建立新的網站和應用程式，然後參閱 [保護主資料管理員 Web 應用程式](../../master-data-services/install-windows/secure-a-master-data-manager-web-application.md) 取得詳細資訊。  
  
#### <a name="to-create-a-master-data-manager-web-application-in-a-new-website"></a>在新網站上建立主資料管理員 Web 應用程式  
  
1.  開啟 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
2.  按一下左窗格中的 **[Web 組態]**。  
  
3.  在 **[Web 組態]** 頁面上的網站清單中，選取 **[建立新網站]**。  
  
4.  在 **[建立網站]** 對話方塊中，指定新網站的資訊。 如需此對話方塊之使用者介面 (UI) 選項的詳細資訊，請參閱[建立網站對話方塊 &#40;Master Data Services 組態管理員&#41;](../../master-data-services/create-website-dialog-box-master-data-services-configuration-manager.md)。  
  
5.  按一下 [確定] 。  
  
## <a name="to-create-a-master-data-manager-web-application-in-an-existing-website"></a>在現有網站上建立主資料管理員 Web 應用程式  
 當您在現有網站上建立 Web 應用程式時，可以選擇 Web 應用程式的虛擬路徑及別名。 此 Web 應用程式會加入至新的應用程式集區。  
  
#### <a name="to-create-a-master-data-manager-web-application-in-an-existing-website"></a>在現有網站上建立主資料管理員 Web 應用程式  
  
1.  開啟 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
2.  按一下左窗格中的 **[Web 組態]**。  
  
3.  在 **[Web 組態]** 頁面的 **[網站]** 清單中，選取建立 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式所在的網站。  
  
4.  按一下 **[建立應用程式]**。  
  
5.  在 **[建立 Web 應用程式]** 對話方塊中，指定新 Web 應用程式的資訊。 如需此對話方塊之使用者介面 (UI) 選項的詳細資訊，請參閱[建立 Web 應用程式對話方塊 &#40;Master Data Services 組態管理員&#41;](../../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md)。  
  
6.  按一下 [確定] 。  
  
## <a name="next-steps"></a>Next Steps  
  
-   將此 Web 應用程式關聯至 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫。 如需詳細資訊，請參閱 [將 Master Data Services 資料庫與 Web 應用程式產生關聯](../../master-data-services/install-windows/associate-a-master-data-services-database-and-web-application.md)。  
  
-   如果要使用安全通訊端層 (SSL) 加密內容，可以選擇將主控 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式的網站設定成使用 HTTPS 繫結。 您必須使用 Internet Information Services (IIS) 工具 (如 IIS 管理員)，才可設定 Web 伺服器的伺服器憑證，以及設定 HTTPS 繫結與網站的 SSL 設定。 如需詳細資訊，請參閱 [Secure a Master Data Manager Web Application](../../master-data-services/install-windows/secure-a-master-data-manager-web-application.md)。  
  
## <a name="see-also"></a>另請參閱  
 [安裝 Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
