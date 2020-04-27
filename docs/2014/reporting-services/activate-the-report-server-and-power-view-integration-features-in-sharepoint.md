---
title: 在 SharePoint 中啟用報表伺服器和 Power View 整合功能 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c7f64a54-c555-4d31-bf99-3abe57dc8626
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e30ae6ea0e7fa314748c4da265650273c0a7d56e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66110031"
---
# <a name="activate-the-report-server-and-power-view-integration-features-in-sharepoint"></a>在 SharePoint 中啟用報表伺服器和 Power View 整合功能
  在[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]您安裝適用于 SharePoint 產品的[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]增益集之後，通常會預設啟用網站集合功能。 在某些情況下，您必須手動啟用這些功能。  
  
 如果您在安裝 SharePoint 產品之後安裝適用於 SharePoint 2010 產品的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 增益集，只會針對根網站集合啟用報表伺服器整合功能和 Power View 整合功能。 如果是其他網站集合，您必須手動啟用這些功能。 例如，如果您擁有 **http://[我的伺服器名稱]/sites/[網站集合名稱]** 網站集合，您需要手動啟用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 網站集合功能。  
  
 如果沒有根網站集合，則 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 增益集會記錄與下面類似的訊息。  
  
 「SharePoint Web 應用程式 80 沒有根網站集合」  
  
 此訊息會在增益集安裝記錄檔中找到，名稱為 "RS_SP_ # .log"，其中 # 是遞增的數位。 記錄檔會在目前使用者的 Temp 資料夾中找到，例如 C:\Users\\[使用者名稱] \appdata\local\temp。如需使用增益集記錄選項的詳細資訊，請參閱[安裝或卸載適用于 sharepoint 的 Reporting Services 增益集 &#40;sharepoint 2010 和 sharepoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)。  
  
 本主題內容：  
  
-   [若要啟用報表伺服器和 Power View 整合網站集合功能：](#bkmk_features)  
  
-   [若要啟用或停用 Reporting Services 管理中心的網站集合功能：](#bkmk_centraladmin)  
  
##  <a name="to-activate-the-report-server-and-power-view-integration-site-collection-features"></a><a name="bkmk_features"></a>若要啟用報表伺服器和 Power View 整合網站集合功能：  
  
1.  開啟瀏覽器，移至您想要啟用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 功能的網站。  
  
2.  按一下 **[網站動作]** 。  
  
3.  按一下 **[站台設定]** 。  
  
4.  在網站集合管理群組中，按一下 **[網站集合功能]** 。  
  
5.  在清單中尋找 **[報表伺服器整合功能]** 或 **[Power View 整合功能]** 。  
  
6.  按一下 [啟動]****。  
  
 若要停用功能，您可以使用相同的程序，但是要按一下 **[停用]** ，而不是 **[啟用]**。  
  
##  <a name="to-activate-or-deactivate-reporting-services-central-administration-site-collection-feature"></a><a name="bkmk_centraladmin"></a>若要啟用或停用 Reporting Services 管理中心網站集合功能：  
  
1.  開啟瀏覽器，並移至 SharePoint 管理中心。  
  
2.  按一下 **[網站動作]** 。  
  
3.  按一下 **[站台設定]** 。  
  
4.  在網站集合管理群組中，按一下 **[網站集合功能]** 。  
  
5.  在清單中尋找 **[報表伺服器管理中心功能]** 。  
  
6.  按一下 [啟動]****。  
  
 若要停用此功能，您可以使用相同的程序，但是要按一下 **[停用]** ，而不是 **[啟用]**。  
  
## <a name="next-steps"></a>後續步驟  
 當此功能啟動之後，您就可以繼續伺服器整合。  
  
## <a name="see-also"></a>另請參閱  
 [安裝或卸載適用于 SharePoint &#40;SharePoint 2010 和 SharePoint 2013 的 Reporting Services 增益集&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
