---
title: 停用或暫停報表與訂閱處理 | Microsoft Docs
ms.custom: ''
ms.date: 09/29/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: subscriptions
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- pausing schedules
- subscriptions [Reporting Services], pausing
- report processing [Reporting Services], pausing
- shared data sources [Reporting Services]
- pausing subscription processing
- pausing report processing
- temporarily stopping report processing
- disabling shared data sources
- roles [Reporting Services], modifying
- shared schedules [Reporting Services], pausing
ms.assetid: 3cf9a240-24cc-46d4-bec6-976f82d8f830
caps.latest.revision: 47
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: dfddb0368d8c674c7f0148a395f97088d9143228
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33035525"
---
# <a name="disable-or-pause-report-and-subscription-processing"></a>停用或暫停報表與訂閱處理
  有好幾種方法，您可以用來停用或暫停 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表和訂閱處理。 本主題中的方法涵蓋了停用訂閱、中斷資料來源連接等範圍。 並非所有的方法都適用於兩種 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 伺服器模式。下表摘要說明這些方法和支援的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 伺服器模式：  
  
##  <a name="bkmk_top"></a> 本主題內容  
  
||支援的伺服器模式|  
|-|---------------------------|  
|[啟用和停用訂閱](#bkmk_disable_subscription)|原生模式|  
|[暫停共用排程](#bkmk_pause_schedule)|原生和 SharePoint 模式|  
|[停用共用資料來源](#bkmk_disable_shared_datasource)|原生和 SharePoint 模式|  
|[修改角色指派來禁止存取報表 (原生模式)](#bkmk_modify_role_assignment)|原生模式|  
|[移除角色的管理訂閱權限 (原生模式)](#bkmk_remove_manage_subscriptions_permission)|原生模式|  
|[停用傳遞延伸模組](#bkmk_disable_extensions)|原生和 SharePoint 模式|  
  
##  <a name="bkmk_disable_subscription"></a> 啟用和停用訂閱  
  
> [!TIP]  
>  [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]的新功能！ **啟用和停用訂閱**。 新的使用者介面選項可讓您快速停用及啟用訂閱。 停用的訂閱會維持其中的其他組態屬性，例如排程，並且可以輕鬆啟用。 您也可以程式設計方式啟用和停用訂閱或稽核哪些訂閱已停用。  
  
 ![eporting Services 訂閱功能區](../../reporting-services/subscriptions/media/ssrs-subscription-ribbon.png "Reporting Services 訂閱功能區")  
  
 在原生模式的報表管理員中，瀏覽至個別訂閱的 [我的訂閱]  頁面或 [管理]  頁面。 選取一或多個訂閱，然後按一下功能區上的停用按鈕 ![停用 Reporting Services 訂閱](../../reporting-services/subscriptions/media/ssrs-disable-subscription.png "停用 Reporting Services 訂閱")或啟用按鈕 ![啟用 Reporting Services 訂閱](../../reporting-services/subscriptions/media/ssrs-enable-subscription.png "啟用 Reporting Services 訂閱")。 已停用的訂閱會標示警告圖示 ![Reporting Services 訂閱的狀態警告](../../reporting-services/subscriptions/media/ssrs-subscription-warning.png "eporting Services 訂閱的狀態警告")，而狀態會列為 [已停用]。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 記錄中寫入一行資料列，而在啟用訂閱時寫入另一個項目。 例如，在報表伺服器記錄檔中：  
  
 `C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\LogFiles\ReportServerService__10_16_2014_00_02_18.log`  
  
 您會看到類似下列的資料列：  
  
 `library!ReportServer_0-1!b08!10/16/2014-16:21:14:: i INFO: Call to DisableSubscriptionAction(SubscriptionID=e843bc2b-023e-45a3-ba23-22f9dc9a0934)`  
  
 `library!ReportServer_0-1!2eec!10/16/2014-16:44:18:: i INFO: Call to EnableSubscriptionAction(SubscriptionID=e843bc2b-023e-45a3-ba23-22f9dc9a0934).`  
  
 ![PowerShell 相關內容](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 相關內容") **使用 Windows PowerShell 停用單一訂閱：** 使用下列 PowerShell 指令碼停用特定的訂閱。 更新伺服器名稱和訂閱識別碼。  
  
```  
#disable specific subscription  
$rs2010 = New-WebServiceProxy -Uri "http://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptionID = "subscription guid”;  
$rs2010.DisableSubscription($subscriptionID);  
  
```  
  
 您可以使用下列指令碼列出所有訂閱與其識別碼。 更新伺服器名稱。  
  
```  
#list all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "http://SERVERNAME /ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
$subscriptions | select subscriptionid, report, status, path  
  
```  
  
 ![PowerShell 相關內容](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 相關內容") **使用 Windows PowerShell 列出所有已停用的訂閱：** 使用下列 PowerShell 指令碼來列出目前的原生模式報表伺服器上所有已停用的訂閱。 更新伺服器名稱。  
  
```  
#list all disabled subscriptions  
$rs2010 = New-WebServiceProxy -Uri "http://uetestb03/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
Write-Host "--- Disabled Subscriptions ---";  
Write-Host "----------------------------------- ";  
$subscriptions | Where-Object {$_.Active.DisabledByUserSpecified -and $_.Active.DisabledByUser } | select subscriptionid, report, status, lastexecuted,path | format-table -auto  
```  
  
 ![PowerShell 相關內容](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 相關內容") **使用 Windows PowerShell 列出所有已停用的訂閱：** 使用下列 PowerShell 指令碼來列出目前的原生模式報表伺服器上所有已停用的訂閱。 更新伺服器名稱。  
  
```  
#enable all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "http://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/") | Where-Object {$_.status -eq "disabled" } ;  
ForEach ($subscription in $subscriptions)  
{  
    $rs2010.EnableSubscription($subscription.SubscriptionID);  
    $subscription | select subscriptionid, report, path  
}  
  
```  
  
 ![PowerShell 相關內容](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 相關內容") **使用 Windows PowerShell 停用所有訂閱：** 使用下列 PowerShell 指令碼列出停用**所有**訂閱。  
  
```  
#DISABLE all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "http://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/") ;  
ForEach ($subscription in $subscriptions)  
{  
    $rs2010.DisableSubscription($subscription.SubscriptionID);  
    $subscription | select subscriptionid, report, path  
}  
```  
  
##  <a name="bkmk_pause_schedule"></a> 暫停共用排程  
 如果報表或訂閱從共用排程執行，您可以暫停排程來禁止處理。 由排程驅動的所有報表與訂閱處理，會被延遲至排程繼續為止。  
  
-   **SharePoint 模式：** ![SharePoint 設定](../../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 設定") 在 [網站設定] 中，選取 [管理共用排程]。 選取排程，然後按一下 [暫停選取的排程] 。  
  
-   **原生模式：** 在報表管理員中，按一下 [網站設定] 。 選取排程，然後按一下 [暫停] 。  
  
##  <a name="bkmk_disable_shared_datasource"></a> 停用共用資料來源  
 使用共用資料來源的優點之一是您可以停用它，禁止執行報表或資料驅動訂閱。 停用共用資料來源會中斷報表與其外部來源的連接。 停用時，資料來源無法供所有使用它的報表與訂閱使用。  
  
 請注意，即使資料來源無法使用，報表仍然會載入。 報表不包含資料，但具備適當權限的使用者可以存取與報表相關聯的屬性頁面、安全性設定、報表記錄，以及訂閱資訊。  
  
-   **SharePoint 模式︰** 若要停用 SharePoint 模式報表伺服器中的共用資料來源，請瀏覽至包含資料來源的文件庫。 ![共用資料來源圖示](../../reporting-services/report-data/media/hlp-16datasource.png "共用資料來源圖示") 按一下資料來源，然後清除 [啟用此資料來源] 核取方塊。  
  
-   **原生模式：** 若要停用原生模式報表伺服器中的共用資料來源，請在報表管理員中開啟資料來源，並清除 [啟用此資料來源]  核取方塊。  
  
##  <a name="bkmk_modify_role_assignment"></a> 修改角色指派來禁止存取報表 (原生模式)  
 讓報表無法使用的一個方法，是暫時移除可以提供存取報表的角色指派。 無論建立資料來源連接的方式為何，此方法可以用於所有報表。 此方法僅會以報表為目標，不會影響其他報表或項目的作業。  
  
 若要移除角色指派，請在報表管理員中，開啟報表的 [安全性屬性] 頁面。 如果報表從父系繼承安全性，您可以按一下 [編輯項目安全性] 來建立嚴格的安全性原則，省略提供普遍存取權的角色指派 (例如，您可以移除提供 Everyone 存取權的角色指派，保留提供一小組使用者存取權的角色指派，例如系統管理員)。  
  
##  <a name="bkmk_remove_manage_subscriptions_permission"></a> 移除角色的管理訂閱權限 (原生模式)  
 若要讓使用者無法建立訂閱，請從角色中清除「管理個別訂閱」  工作。 當您移除這個工作後，[訂閱] 頁面就無法使用。 在報表管理員中，即使 [我的訂閱] 頁面原先含有訂閱，此時也會顯示空白 (無法刪除這個頁面)。 移除訂閱相關的工作會讓使用者無法建立與修改訂閱，但是不會刪除現有的訂閱。 現有的訂閱會繼續執行，直到刪除為止。 若要移除權限：  
  
1.  開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 con  
  
2.  連接至 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器。  
  
3.  展開 [安全性]  節點。  
  
4.  選取角色，並清除 [管理個別訂閱]  工作。  
  
##  <a name="bkmk_disable_extensions"></a> 停用傳遞延伸模組  
 在報表伺服器上安裝的所有傳遞延伸模組都會提供給有權建立給定報表之訂閱的任何使用者。 系統會自動提供和設定下列傳遞延伸模組：  
  
-   Windows 檔案共用  
  
-   SharePoint 文件庫 (只能從與 SharePoint 整合模式報表伺服器整合的 SharePoint 網站使用)  
  
 您必須先設定電子郵件傳遞，然後才能使用它。 如果您沒有設定它，便無法使用它。 如需詳細資訊，請參閱 [為電子郵件傳遞設定報表伺服器 (SSRS 組態管理員)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83)。  
  
 如果您想要關閉特定延伸模組，可以在 **RSReportServer.config** 檔中移除延伸模組項目。 如需詳細資訊，請參閱 [Reporting Services 組態檔](../../reporting-services/report-server/reporting-services-configuration-files.md) 和 [為電子郵件傳遞設定報表伺服器 (SSRS 組態管理員)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83)。  
  
 在您移除傳遞延伸模組之後，就無法再於報表管理員或 SharePoint 網站中使用它。 移除傳遞延伸模組可能會產生非使用中訂閱。 移除延伸模組之前，請務必刪除訂閱，或將它們設定為使用不同的傳遞延伸模組。  
  
## <a name="see-also"></a>另請參閱  
 [訂閱與傳遞 &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Reporting Services 組態檔](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [設定報表管理員 &#40;原生模式&#41;](../../reporting-services/report-server/configure-report-manager-native-mode.md)   
 [Reporting Services 報表伺服器 &#40;原生模式&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [報表管理員 &#40;SSRS 原生模式&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [安全性屬性頁面，項目 &#40;報表管理員&#41;](http://msdn.microsoft.com/library/351b8503-354f-4b1b-a7ac-f1245d978da0)  
  
  
