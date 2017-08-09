---
title: "啟用報表伺服器和 Power View Integration Features in SharePoint |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c7f64a54-c555-4d31-bf99-3abe57dc8626
caps.latest.revision: 6
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: bca4115307f7bf9dab5ffc9d2ab02ababb209d65
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="site-collection-features---report-server-and-power-view"></a>網站集合功能-報表伺服器和 Power View
  在安裝適用於 SharePoint 產品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 網站集合功能。 在某些情況下，您必須手動啟用這些功能。  
  
 如果您在安裝 SharePoint 產品之後安裝適用於 SharePoint 2010 產品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集，只會針對根網站集合啟用報表伺服器整合功能和 Power View 整合功能。 如果是其他網站集合，您必須手動啟用這些功能。 例如，如果您擁有 **http://[我的伺服器名稱]/sites/[網站集合名稱]** 網站集合，您需要手動啟用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 網站集合功能。  
  
 如果沒有根網站集合，則 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集會記錄與下面類似的訊息。  
  
 「SharePoint Web 應用程式 80 沒有根網站集合」  
  
 此訊息可在名為 “RS_SP_#.log” 的增益集安裝記錄中找到，其中 # 是遞增的數字。 此記錄檔可在目前使用者的 Temp 資料夾中找到，例如 C:\Users\\[使用者名稱]\AppData\Local\Temp。 如需使用增益集之記錄選項的詳細資訊，請參閱 [安裝或解除安裝 SharePoint 的 Reporting Services 增益集](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)。  
  
 本主題內容：  
  
-   [若要啟用報表伺服器和 Power View 整合網站集合功能：](#bkmk_features)  
  
-   [若要啟用或停用 Reporting Services 管理中心的網站集合功能：](#bkmk_centraladmin)  
  
##  <a name="bkmk_features"></a> 若要啟用報表伺服器和 Power View 整合網站集合功能：  
  
1.  開啟瀏覽器，移至您想要啟用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能的網站。  
  
2.  按一下 **[網站動作]**。  
  
3.  按一下 **[站台設定]**。  
  
4.  在網站集合管理群組中，按一下 **[網站集合功能]** 。  
  
5.  在清單中尋找 **[報表伺服器整合功能]** 或 **[Power View 整合功能]** 。  
  
6.  按一下 **[啟用]**。  
  
 若要停用功能，您可以使用相同的程序，但是要按一下 **[停用]** ，而不是 **[啟用]**。  
  
##  <a name="bkmk_centraladmin"></a> 若要啟用或停用 Reporting Services 管理中心的網站集合功能：  
  
1.  開啟瀏覽器，並移至 SharePoint 管理中心。  
  
2.  按一下 **[網站動作]**。  
  
3.  按一下 **[站台設定]**。  
  
4.  在網站集合管理群組中，按一下 **[網站集合功能]** 。  
  
5.  在清單中尋找 **[報表伺服器管理中心功能]** 。  
  
6.  按一下 **[啟用]**。  
  
 若要停用此功能，您可以使用相同的程序，但是要按一下 **[停用]** ，而不是 **[啟用]**。  
  
## <a name="next-steps"></a>後續步驟  
 當此功能啟動之後，您就可以繼續伺服器整合。  
  
## <a name="see-also"></a>請參閱＜  
 [安裝或解除安裝 SharePoint 的 Reporting Services 增益集](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
