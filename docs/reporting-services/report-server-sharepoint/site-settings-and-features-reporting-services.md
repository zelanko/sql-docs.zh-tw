---
title: "Reporting Services 網站設定和網站功能 （SharePoint 模式） |Microsoft 文件"
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
ms.openlocfilehash: ea81c248f302e322d981b90147d42cb83a4804cc
ms.contentlocale: zh-tw
ms.lasthandoff: 10/06/2017

---
# <a name="reporting-services-site-settings-and-site-features-sharepoint-mode"></a>Reporting Services 網站設定和網站功能 （SharePoint 模式）

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Reporting Services SharePoint 模式有數個站台層級的自訂功能和可以從 SharePoint 網站設定 頁面管理的網站功能。 設定適用於整個網站，並且會影響所有 Reporting Services 服務應用程式。 您必須擁有「內容管理員」和「系統管理員」權限才能檢視此頁面。  

> [!NOTE]
> SQL Server 2016 之後已無法再使用 reporting Services 與 SharePoint 整合。

|網站設定|Description|  
|------------------|-----------------|  
|Reporting Services 網站設定|本主題所述的全站台的設定。|  
|管理資料警示|管理資料警示功能。|  
|報表伺服器檔案同步處理|預設停用的網站層級功能。<br /><br /> 在文件庫內直接加入或更新檔案時，將 SharePoint 文件庫中的報表伺服器檔案 (.rdl、.rsds、.smdl、.rsd、.rsc、.rdlx) 同步處理到報表伺服器。<br /><br /> 如需詳細資訊，請參閱 [在 SharePoint 管理中心啟動報表伺服器檔案同步處理功能](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)|  
  
## <a name="open-the-reporting-services-site-settings-page"></a>開啟 [Reporting Services 網站設定] 頁面
  
1.  從 SharePoint 網站**網站動作**功能表上，選取**站台設定**。  
  
2.  在**Reporting Services**區段中，選取**Reporting Services 網站設定**。  
  
## <a name="options-for-reporting-services-site-settings"></a>Reporting Services 網站設定的選項
  
|選項|說明|  
|------------|-----------------|  
|**啟用 RSClientPrint ActiveX 控制項下載**|控制項會顯示自訂列印對話方塊，其中支援與其他列印對話方塊一樣的一般功能，包括預覽列印、可指定要列印的特定頁面及範圍、頁面邊界和列印方向等選擇。 如需控制項的詳細資訊，請參閱 [在自訂應用程式中使用 RSClientPrint 控制項](../../reporting-services/report-server-web-service/net-framework/using-the-rsclientprint-control-in-custom-applications.md)|  
|**在本機模式中啟用遠端錯誤**|顯示或隱藏當遠端電腦在本機模式執行時的詳細錯誤訊息。 如果您看到類似以下的錯誤訊息，則啟用遠端錯誤可能會很實用：<br /><br /> `For more information about this error navigate to the report server on the local server machine or enable remote errors`|  
|**啟用報表的可存取性中繼資料**|開啟報表的 HTML 輸出中的可存取性中繼資料|  
|**啟用報表的精確資料視覺效果調整大小功能**|在 Tablix 內設定資料視覺效果調整大小行為，使大小完全符合。 其中包括圖表、量測計和地圖。 當停用此設定時，此行為適用於讓資料大致相符的視覺效果 (可能會留一些空白)。 這項設定僅適用於轉譯報表檢視器 web 組件中。 若要管理的伺服器端轉譯這個行為，您需要修改**rsreportserver.config**檔案。 如需詳細資訊，請參閱下列內容：<br /><br /> [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)。<br /><br /> [在 RSReportServer.Config 中自訂轉譯延伸模組參數](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)。<br /><br /> [HTML 裝置資訊設定](../../reporting-services/html-device-information-settings.md)。<br /><br /> 啟用 [精確] 可能會影響效能，因為判斷精確大小的處理所花的時間可能會比近似大小還要長。|  
  
## <a name="see-also"></a>另請參閱

 [管理 Reporting Services SharePoint 服務應用程式](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)  
  
  
