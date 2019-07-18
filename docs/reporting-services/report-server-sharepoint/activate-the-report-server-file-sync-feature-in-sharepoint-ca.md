---
title: 在 SharePoint 啟動報表伺服器檔案同步處理功能 | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 3a84c906df921bf4702d47e57400b7ad7b9e127f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65579448"
---
# <a name="activate-the-report-server-file-sync-feature-in-sharepoint"></a>在 SharePoint 啟動報表伺服器檔案同步處理功能

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器檔案同步處理] 功能會利用 SharePoint 事件處理常式，同步處理報表伺服器目錄與文件庫中的項目。 當使用者經常直接上傳已發行的報表項目至 SharePoint 文件庫時，這項功能會很有幫助。 如果檔案同步處理功能未啟動，內容仍會同步處理，但是頻率會較低。

> [!NOTE]
> SQL Server 2016 後即不再提供 Reporting Services 與 SharePoint 的整合。
  
 安裝 SharePoint 產品的 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 增益集之後，可以在 SharePoint 網站管理中啟用檔案同步處理功能。  
  
 這項功能可以在每個網站以手動方式啟用及停用，但不能在網站集合層級啟用及停用。  
  
## <a name="prerequisites"></a>Prerequisites

 必須安裝適用於 SharePoint 的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集。 如果未安裝此增益集，網站功能清單中將不會顯示檔案同步處理功能。  
  
 若要確認安裝，請檢視在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows **[控制台]** 中已安裝應用程式的清單。 如果已安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集，請遵循本主題的指示來啟用報表伺服器同步處理功能。  
  
### <a name="to-activate-or-deactivate-the-reporting-services-file-sync-feature-on-a-site"></a>在網站上啟用或停用報表伺服器檔案同步處理功能
  
1.  從網站的主頁面按一下 **[網站動作]** 功能表，然後按一下 **[網站設定]** 。  
  
2.  在 **[網站動作]** 中按一下 **[管理網站功能]** 。  
  
3.  在清單中找到 **[報表伺服器檔案同步處理]** 。  
  
4.  按一下 **[啟用]** 。  

> [!NOTE]
> 若要停用報表伺服器檔案同步處理功能，您可以執行相同的程序，但是請按一下 [停用]  。

## <a name="see-also"></a>另請參閱

 [針對報表組件進行疑難排解 (報表產生器及 SSRS)](https://msdn.microsoft.com/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [在 SharePoint 中啟用報表伺服器和 Power View 整合功能](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)   
 [安裝或解除安裝 SharePoint 的 Reporting Services 增益集](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [安裝或解除安裝 SharePoint 的 Reporting Services 增益集](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
