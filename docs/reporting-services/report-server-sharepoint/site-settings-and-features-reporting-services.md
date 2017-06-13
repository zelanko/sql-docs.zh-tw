---
title: "Reporting Services 網站設定和網站功能 （SharePoint 模式） |Microsoft 文件"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e0040fec-e2b7-4099-ae01-3b9bb9128bbd
caps.latest.revision: 10
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 044346bd4532c691861689662edbcbb37812b7ff
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="site-settings-and-features---reporting-services"></a>站台設定和功能-Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式有幾個網站層級自訂功能和網站功能，這些功能可以從 SharePoint [網站設定] 頁面進行管理。 這些設定適用於整個網站，而且會影響所有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式。 您必須擁有「內容管理員」和「系統管理員」權限才能檢視此頁面。  
  
|網站設定|說明|  
|------------------|-----------------|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 網站設定|本主題描述全網站的設定。|  
|管理資料警示|管理資料警示功能。|  
|報表伺服器檔案同步處理|預設停用的網站層級功能。<br /><br /> 在文件庫內直接加入或更新檔案時，將 SharePoint 文件庫中的報表伺服器檔案 (.rdl、.rsds、.smdl、.rsd、.rsc、.rdlx) 同步處理到報表伺服器。<br /><br /> 如需詳細資訊，請參閱 [在 SharePoint 管理中心啟動報表伺服器檔案同步處理功能](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)|  
  
## <a name="to-open-the-reporting-services-site-settings-page"></a>若要開啟 Reporting Services 網站設定頁面  
  
1.  在 SharePoint 網站的 [網站動作] 功能表中，按一下 [網站設定]。  
  
2.  在 [Reporting Services] 區段中，按一下 [Reporting Services 網站設定]。  
  
## <a name="options-for-reporting-services-site-settings"></a>Reporting Services 網站設定的選項  
  
|選項|說明|  
|------------|-----------------|  
|**啟用 RSClientPrint ActiveX 控制項下載**|控制項會顯示自訂列印對話方塊，其中支援與其他列印對話方塊一樣的一般功能，包括預覽列印、可指定要列印的特定頁面及範圍、頁面邊界和列印方向等選擇。 如需控制項的詳細資訊，請參閱 [在自訂應用程式中使用 RSClientPrint 控制項](../../reporting-services/report-server-web-service/net-framework/using-the-rsclientprint-control-in-custom-applications.md)|  
|**在本機模式中啟用遠端錯誤**|顯示或隱藏當遠端電腦在本機模式執行時的詳細錯誤訊息。 如果您看到類似以下的錯誤訊息，則啟用遠端錯誤可能會很實用：<br /><br /> `For more information about this error navigate to the report server on the local server machine or enable remote errors`|  
|**啟用報表的可存取性中繼資料**|開啟報表的 HTML 輸出中的可存取性中繼資料|  
|**啟用報表的精確資料視覺效果調整大小功能**|在 Tablix 內設定資料視覺效果調整大小行為，使大小完全符合。 其中包括圖表、量測計和地圖。 當停用此設定時，此行為適用於讓資料大致相符的視覺效果 (可能會留一些空白)。 此設定只適用於在報表檢視器 Web 組件中轉譯。 若要針對伺服器端轉譯來管理這個行為，您需要修改 **rsreportserver.config** 檔案。 如需詳細資訊，請參閱下列內容：<br /><br /> [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)。<br /><br /> [在 RSReportServer.Config 中自訂轉譯延伸模組參數](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)。<br /><br /> [HTML 裝置資訊設定](../../reporting-services/html-device-information-settings.md)。<br /><br /> 啟用 [精確] 可能會影響效能，因為判斷精確大小的處理所花的時間可能會比近似大小還要長。|  
  
## <a name="see-also"></a>請參閱＜  
 [Manage a Reporting Services SharePoint Service Application](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)  
  
  
