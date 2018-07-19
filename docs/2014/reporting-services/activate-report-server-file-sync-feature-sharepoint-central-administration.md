---
title: 啟用報表伺服器檔案同步處理功能，在 SharePoint 管理中心內 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 32d1988d-07e7-41c2-b636-e65ecfae4677
caps.latest.revision: 8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e85c5ff71ba83704752ae55057fb47777becd55b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37258154"
---
# <a name="activate-the-report-server-file-sync-feature-in-sharepoint-central-administration"></a>在 SharePoint 管理中心啟動報表伺服器檔案同步處理功能
  [ [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 報表伺服器檔案同步處理] 功能會利用 SharePoint 事件處理常式，同步處理報表伺服器目錄與文件庫中的項目。 當使用者經常直接上傳已發行的報表項目至 SharePoint 文件庫時，這項功能會很有幫助。 如果檔案同步處理功能未啟動，內容仍會同步處理，但是頻率會較低。  
  
 安裝之後，可以在 SharePoint 網站管理中啟用檔案同步處理功能[!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]增益集適用於 SharePoint 產品。  
  
 這項功能可以在每個網站以手動方式啟用及停用，但不能在網站集合層級啟用及停用。  
  
## <a name="prerequisites"></a>先決條件  
 必須安裝適用於 SharePoint 的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 增益集。 如果未安裝此增益集，網站功能清單中將不會顯示檔案同步處理功能。  
  
 若要確認安裝，請檢視 已安裝的應用程式中的清單[!INCLUDE[msCoName](../includes/msconame-md.md)]Windows**控制台**。 如果[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]安裝增益集，請遵循本主題中的指示來啟用報表伺服器檔案同步處理功能。  
  
### <a name="to-activate-or-deactivate-the-reporting-services-file-sync-feature-on-a-site"></a>在網站上啟用或停用報表伺服器檔案同步處理功能  
  
1.  從網站的主頁面按一下 **[網站動作]** 功能表，然後按一下 **[網站設定]**。  
  
2.  在 **[網站動作]** 中按一下 **[管理網站功能]**。  
  
3.  在清單中找到 **[報表伺服器檔案同步處理]** 。  
  
4.  按一下 **[啟用]**。  
  
> [!NOTE]  
>  若要停用報表伺服器檔案同步處理功能，您可以執行相同的程序，但是請按一下 [停用]。  
  
## <a name="see-also"></a>另請參閱  
 [疑難排解報表組件&#40;報表產生器及 SSRS&#41;](report-parts-report-builder-and-ssrs.md)   
 [啟用報表伺服器和 SharePoint 中的 Power View 整合功能](activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)   
 [安裝或解除安裝 Reporting Services 增益集，適用於 SharePoint &#40;SharePoint 2010 和 SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [安裝或解除安裝 Reporting Services 增益集，適用於 SharePoint &#40;SharePoint 2010 和 SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
