---
title: "啟用報表伺服器和 Power View 整合功能，在 SharePoint 中的 |Microsoft 文件"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: e97378914a59fab938fc3e4c7926847effcffc94
ms.contentlocale: zh-tw
ms.lasthandoff: 10/06/2017

---
# <a name="activate-the-report-server-and-power-view-integration-features-in-sharepoint"></a>啟用報表伺服器和 SharePoint 中的 Power View 整合功能

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  安裝之後，預設會啟動 Reporting Services 網站集合功能[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]適用於 SharePoint 產品增益集。 在某些情況下，您需要手動啟用這些功能。  

> [!NOTE]
> SQL Server 2016 之後已無法再使用 reporting Services 與 SharePoint 整合。

 如果您安裝 SharePoint 產品之後安裝的 Reporting Services 增益集適用於 SharePoint 2010 產品，然後報表伺服器整合功能和 Power View 整合功能將只會針對啟用根網站集合。 其他網站集合，您需要手動啟用這些功能。 例如，如果您擁有的站台集合**http://[my 伺服器名稱] /sites/ [網站集合名稱]**您必須以手動方式啟動 Reporting Services 網站集合功能。  
  
 沒有根網站集合時，Reporting Services 增益集將會記錄類似下列的訊息。  
  
 「SharePoint Web 應用程式 80 沒有根網站集合」  
  
 增益集安裝記錄檔中，名為"RS_SP_ #.log"其中 # 是遞增的數字中找到的訊息。 記錄檔位於目前使用者 Temp 資料夾，例如 C:\Users\\[使用者名稱] \AppData\Local\Temp。如需使用增益集之記錄選項的詳細資訊，請參閱 [安裝或解除安裝 SharePoint 的 Reporting Services 增益集](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)。  

## <a name="activate-the-report-server-and-power-view-integration-site-collection-features"></a>啟動報表伺服器和 Power View 整合網站集合功能
  
1.  開啟您想要的網站，您的 Reporting Services 功能作用中的瀏覽器。  
  
2.  按一下 **[網站動作]**。  
  
3.  按一下 **[站台設定]**。  
  
4.  在網站集合管理群組中，按一下 **[網站集合功能]** 。  
  
5.  在清單中尋找 **[報表伺服器整合功能]** 或 **[Power View 整合功能]** 。  
  
6.  按一下 **[啟用]**。  
  
 若要停用功能，您可以使用相同的程序，但是要按一下 **[停用]** ，而不是 **[啟用]**。  
  
## <a name="activate-or-deactivate-reporting-services-central-administration-site-collection-feature"></a>啟用或停用 Reporting Services 管理中心 網站集合功能
  
1.  開啟瀏覽器，並移至 SharePoint 管理中心。  
  
2.  按一下 **[網站動作]**。  
  
3.  按一下 **[站台設定]**。  
  
4.  在網站集合管理群組中，按一下 **[網站集合功能]** 。  
  
5.  在清單中尋找 **[報表伺服器管理中心功能]** 。  
  
6.  按一下 **[啟用]**。  
  
 若要停用此功能，您可以使用相同的程序，但是要按一下 **[停用]** ，而不是 **[啟用]**。  
  
## <a name="next-steps"></a>後續的步驟

當此功能啟動之後，您就可以繼續伺服器整合。

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
