---
title: Reporting Services 網站設定和網站功能 （SharePoint 模式） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: e0040fec-e2b7-4099-ae01-3b9bb9128bbd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 14708d286ea11a872a3260f41cae44e05e7fb30c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63283406"
---
# <a name="reporting-services-site-settings-and-site-featuressharepoint-mode"></a>Reporting Services 網站設定和網站功能 (SharePoint 模式)
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式有幾個網站層級自訂功能和網站功能，這些功能可以從 SharePoint [網站設定] 頁面進行管理。 這些設定適用於整個網站，而且會影響所有 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服務應用程式。 您必須擁有「內容管理員」和「系統管理員」權限才能檢視此頁面。  
  
|網站設定|描述|  
|------------------|-----------------|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 網站設定|本主題描述全網站的設定。|  
|管理資料警示|管理資料警示功能。|  
|報表伺服器檔案同步處理|預設停用的網站層級功能。<br /><br /> 在文件庫內直接加入或更新檔案時，將 SharePoint 文件庫中的報表伺服器檔案 (.rdl、.rsds、.smdl、.rsd、.rsc、.rdlx) 同步處理到報表伺服器。<br /><br /> 如需詳細資訊，請參閱 [在 SharePoint 管理中心啟動報表伺服器檔案同步處理功能](../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md)|  
  
## <a name="to-open-the-reporting-services-site-settings-page"></a>若要開啟 Reporting Services 網站設定頁面  
  
1.  從 SharePoint 站台**站台動作**功能表上，按一下**站台設定**。  
  
2.  在  **Reporting Services**區段中，按一下**Reporting Services 網站設定**。  
  
## <a name="options-for-reporting-services-site-settings"></a>Reporting Services 網站設定的選項  
  
|選項|描述|  
|------------|-----------------|  
|**啟用 RSClientPrint ActiveX 控制項下載**|控制項會顯示自訂列印對話方塊，其中支援與其他列印對話方塊一樣的一般功能，包括預覽列印、可指定要列印的特定頁面及範圍、頁面邊界和列印方向等選擇。 如需控制項的詳細資訊，請參閱 [在自訂應用程式中使用 RSClientPrint 控制項](report-server-web-service/net-framework/using-the-rsclientprint-control-in-custom-applications.md)|  
|**在本機模式中啟用遠端錯誤**|顯示或隱藏當遠端電腦在本機模式執行時的詳細錯誤訊息。 如果您看到類似以下的錯誤訊息，則啟用遠端錯誤可能會很實用：<br /><br /> `For more information about this error navigate to the report server on the local server machine or enable remote errors`|  
|**啟用報表的可存取性中繼資料**|開啟報表的 HTML 輸出中的可存取性中繼資料|  
|**啟用報表的精確資料視覺效果調整大小功能**|在 Tablix 內設定資料視覺效果調整大小行為，使大小完全符合。 其中包括圖表、量測計和地圖。 當停用此設定時，此行為適用於讓資料大致相符的視覺效果 (可能會留一些空白)。 此設定只適用於在報表檢視器 Web 組件中轉譯。 若要針對伺服器端轉譯來管理這個行為，您需要修改 **rsreportserver.config** 檔案。 如需詳細資訊，請參閱下列內容：<br /><br /> [RSReportServer 組態檔](report-server/rsreportserver-config-configuration-file.md)。<br /><br /> [在 RSReportServer.Config 中自訂轉譯延伸模組參數](customize-rendering-extension-parameters-in-rsreportserver-config.md)。<br /><br /> [HTML 裝置資訊設定](html-device-information-settings.md)。<br /><br /> 啟用 [精確] 可能會影響效能，因為判斷精確大小的處理所花的時間可能會比近似大小還要長。|  
  
## <a name="see-also"></a>另請參閱  
 [Manage a Reporting Services SharePoint Service Application](../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)  
  
  
