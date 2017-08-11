---
title: "啟動報表伺服器檔案同步處理功能，在 SharePoint CA 中的 |Microsoft 文件"
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
ms.assetid: 32d1988d-07e7-41c2-b636-e65ecfae4677
caps.latest.revision: 9
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: d9f1b75bc40693248526282a6565db340930601b
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="activate-the-report-server-file-sync-feature-in-sharepoint-ca"></a>啟動報表伺服器檔案同步處理功能，在 SharePoint CA 中
  [ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器檔案同步處理] 功能會利用 SharePoint 事件處理常式，同步處理報表伺服器目錄與文件庫中的項目。 當使用者經常直接上傳已發行的報表項目至 SharePoint 文件庫時，這項功能會很有幫助。 如果檔案同步處理功能未啟動，內容仍會同步處理，但是頻率會較低。  
  
 安裝 SharePoint 產品的 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 增益集之後，可以在 SharePoint 網站管理中啟用檔案同步處理功能。  
  
 這項功能可以在每個網站以手動方式啟用及停用，但不能在網站集合層級啟用及停用。  
  
## <a name="prerequisites"></a>必要條件  
 必須安裝適用於 SharePoint 的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集。 如果未安裝此增益集，網站功能清單中將不會顯示檔案同步處理功能。  
  
 若要確認安裝，請檢視在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows **[控制台]**中已安裝應用程式的清單。 如果已安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集，請遵循本主題的指示來啟用報表伺服器同步處理功能。  
  
### <a name="to-activate-or-deactivate-the-reporting-services-file-sync-feature-on-a-site"></a>在網站上啟用或停用報表伺服器檔案同步處理功能  
  
1.  從網站的主頁面按一下 **[網站動作]** 功能表，然後按一下 **[網站設定]**。  
  
2.  在 **[網站動作]** 中按一下 **[管理網站功能]**。  
  
3.  在清單中找到 **[報表伺服器檔案同步處理]** 。  
  
4.  按一下 **[啟用]**。  
  
> [!NOTE]  
>  若要停用報表伺服器檔案同步處理功能，您可以使用相同的程序，但是按一下**停用**。  
  
## <a name="see-also"></a>另請參閱  
 [疑難排解報表組件 (報表產生器及 SSRS)](http://msdn.microsoft.com/en-us/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [在 SharePoint 中啟用報表伺服器和 Power View 整合功能](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)   
 [安裝或解除安裝 SharePoint 的 Reporting Services 增益集](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [安裝或解除安裝 SharePoint 的 Reporting Services 增益集](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
