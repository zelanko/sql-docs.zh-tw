---
title: 停用或暫停報表與訂閱處理 | Microsoft Docs
description: 管理訂閱、暫停共用排程、停用共用資料來源、封鎖報表存取、管理訂閱權限與移除傳遞延伸模組。
ms.date: 06/19/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
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
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1ea16180c9a4e67f40302de7d70ae357b8393010
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91986624"
---
# <a name="disable-or-pause-report-and-subscription-processing"></a>停用或暫停報表與訂閱處理  
有好幾種方法，您可以用來停用或暫停 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表和訂閱處理。 此文章中的方式包括停用訂用帳戶以中斷資料來源連線。 並非所有的方法都可以使用這兩種 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 伺服器模式。 下表摘要說明這些方法和支援的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 伺服器模式：  
  
##  <a name="in-this-article"></a><a name="bkmk_top"></a> 本文內容  
  
|方法|支援的伺服器模式|  
|-|---------------------------|  
|[啟用和停用訂閱](#bkmk_disable_subscription)|原生模式|  
|[暫停共用排程](#bkmk_pause_schedule)|原生和 SharePoint 模式|  
|[停用共用資料來源](#bkmk_disable_shared_datasource)|原生和 SharePoint 模式|  
|[修改角色指派來禁止存取報表 (原生模式)](#bkmk_modify_role_assignment)|原生模式|  
|[移除角色的管理訂閱權限 (原生模式)](#bkmk_remove_manage_subscriptions_permission)|原生模式|  
|[停用傳遞延伸模組](#bkmk_disable_extensions)|原生和 SharePoint 模式|  
  
##  <a name="enable-and-disable-subscriptions"></a><a name="bkmk_disable_subscription"></a> 啟用和停用訂用帳戶  
  
>[!TIP]  
>SQL 2016 Reporting Services 的新功能，「啟用和停用訂用帳戶」  。 新的使用者介面選項可讓您快速啟用及停用訂用帳戶。 停用的訂閱會維持其中的其他組態屬性，例如排程，並且可以輕鬆重新啟用。 您也能以程式設計方式啟用及停用訂用帳戶或稽核哪些訂用帳戶已停用。  
  
  ![[訂用帳戶] 頁面的 [啟用] 和 [停用] 按鈕 ](../../reporting-services/subscriptions/media/disable-or-pause-report-and-subscription-processing/subscription-enable-and-disable-buttons.png)  
  
在入口網站中，從 [我的訂閱]  頁面或個別訂用帳戶的 [訂用帳戶]  頁面瀏覽至訂用帳戶。 選取一或多個訂用帳戶，然後按一下功能區上的 [停用] 按鈕或 [啟用] 按鈕 (請參閱上面的影像)。 [狀態] 欄會分別變更為 [已停用] 或 [已啟用]。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會在訂用帳戶啟用或停用時，在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 記錄檔中寫入資料列。 例如，在報表伺服器記錄檔中：  
  
 `C:\Program Files\Microsoft SQL Server Reporting Services\SSRS\LogFiles\RSPortal_2019_06_20_00_49_22.log`  
  
 您會看到類似下列的資料列：  
  
 `RSPortal!subscription!RSPortal.exe!93!06/20/2019-01:16:47:: i INFO: Subscription 2b409d66-d4ea-408a-918c-0f9e41ce49ca disabled at 06/20/2019 01:16:47`  
  
 `RSPortal!subscription!RSPortal.exe!93!06/20/2019-01:16:51:: i INFO: Subscription 2b409d66-d4ea-408a-918c-0f9e41ce49ca enabled at 06/20/2019 01:16:51`  
  
![PowerShell 相關內容](/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 相關內容")：**使用 Windows PowerShell 停用單一訂用帳戶：** 使用下列 PowerShell 指令碼停用特定的訂用帳戶。 更新指令碼中的伺服器名稱和訂用帳戶識別碼。  
  
```PS  
#disable specific subscription  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptionID = "subscription guid";  
$rs2010.DisableSubscription($subscriptionID);  
  
```  
  
 您可以使用下列指令碼列出所有訂閱與其識別碼。 更新伺服器名稱。  
  
```  
#list all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME /ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
$subscriptions | select subscriptionid, report, status, path  
  
```  
  
 ![PowerShell 相關內容](/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 相關內容") **使用 Windows PowerShell 列出所有停用的訂用帳戶：** 使用下列 PowerShell 指令碼列出目前原生模式報表伺服器上所有已停用的訂用帳戶。 更新伺服器名稱。  
  
```  
#list all disabled subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://uetestb03/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
Write-Host "--- Disabled Subscriptions ---";  
Write-Host "----------------------------------- ";  
$subscriptions | Where-Object {$_.Active.DisabledByUserSpecified -and $_.Active.DisabledByUser } | select subscriptionid, report, status, lastexecuted,path | format-table -auto  
```  
  
 ![PowerShell 相關內容](/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 相關內容") **使用 Windows PowerShell 啟用所有停用的訂用帳戶：** 使用下列 PowerShell 指令碼啟用所有目前已停用的訂用帳戶。 更新伺服器名稱。  
  
```  
#enable all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/") | Where-Object {$_.status -eq "disabled" } ;  
ForEach ($subscription in $subscriptions)  
{  
    $rs2010.EnableSubscription($subscription.SubscriptionID);  
    $subscription | select subscriptionid, report, path  
}  
  
```  
  
 ![PowerShell 相關內容](/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 相關內容") **使用 Windows PowerShell「停用」所有訂用帳戶：** 使用下列 PowerShell 指令碼列出要停用的「所有」  訂用帳戶。  
  
```  
#DISABLE all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/") ;  
ForEach ($subscription in $subscriptions)  
{  
    $rs2010.DisableSubscription($subscription.SubscriptionID);  
    $subscription | select subscriptionid, report, path  
}  
```  
  
##  <a name="pause-a-shared-schedule"></a><a name="bkmk_pause_schedule"></a> 暫停共用排程  
 如果報表或訂閱從共用排程執行，您可以暫停排程來禁止處理。 由排程驅動的所有報表與訂閱處理，會被延遲至排程繼續為止。  
  
-   **SharePoint 模式：** ![SharePoint 設定](/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 設定")：在 [網站設定]  中，選取 [管理共用排程]  。 選取排程，然後按一下 [暫停選取的排程]  。  
  
-   **原生模式：** 在入口網站中，從入口網站畫面頂端的功能表列中，選取 [設定]  按鈕 ![[設定] 按鈕](media/ssrs-portal-settings-gear.png)，然後從下拉式功能表中選取 [網站設定]  。 選取 [排程]  索引標籤，以顯示 [排程] 頁面。 選取您想要啟用或停用的排程旁核取方塊，然後分別選取 [啟用]  或 [停用]  按鈕來執行所需的動作。 [狀態] 欄會據此更新為「已停用」或「已啟用」。  
  
##  <a name="disable-a-shared-data-source"></a><a name="bkmk_disable_shared_datasource"></a> 停用共用資料來源  
 使用共用資料來源的優點之一是您可以停用它，禁止執行報表或資料驅動訂閱。 停用共用資料來源會中斷報表與其外部來源的連接。 停用時，資料來源無法供所有使用它的報表與訂閱使用。  
  
 請注意，即使資料來源無法使用，報表仍然會載入。 報表不包含資料，但具備適當權限的使用者可以存取與報表相關聯的屬性頁面、安全性設定、報表記錄，以及訂閱資訊。  
  
-   **SharePoint 模式：** 若要停用 SharePoint 模式報表伺服器中的共用資料來源，請瀏覽至包含資料來源的文件庫。 ![共用資料來源圖示](../../reporting-services/report-data/media/hlp-16datasource.png "共用資料來源圖示") 按一下資料來源，然後清除 [啟用此資料來源]  核取方塊。  
  
-   **原生模式：** 若要停用原生模式報表伺服器上的共用資料來源，請在入口網站中開啟資料來源，並清除 [啟用此資料來源]  核取方塊。  
  
##  <a name="modify-role-assignments-to-prevent-access-to-a-report-native-mode"></a><a name="bkmk_modify_role_assignment"></a> 修改角色指派來禁止存取報表 (原生模式)  
讓報表無法使用的一個方法，是暫時移除可以提供存取報表的角色指派。 無論建立資料來源連接的方式為何，此方法可以用於所有報表。 此方法僅會以報表為目標，不會影響其他報表或項目的作業。  
  
 若要移除角色指派，請在入口網站中，開啟報表的 [安全性]  頁面。 如果報表從父系繼承安全性，您可以選取 [自訂安全性]  並選取 [項目安全性]  對話方塊中的 [確認]  來建立嚴格的安全性原則，省略提供普遍存取權的角色指派 (例如，您可以移除提供 Everyone 存取權的角色指派，保留提供一小組使用者存取權的角色指派，例如系統管理員)。  
  
##  <a name="remove-manage-subscription-permissions-from-role-native-mode"></a><a name="bkmk_remove_manage_subscriptions_permission"></a> 移除角色的管理訂閱權限 (原生模式)  
 若要讓使用者無法建立訂閱，請從角色中清除「管理個別訂閱」  工作。 當您移除這個工作後，[訂閱] 頁面就無法使用。 在入口網站中，即使 [我的訂閱] 頁面原先含有訂閱，此時也會顯示空白 (無法刪除這個頁面)。 移除訂閱相關的工作會讓使用者無法建立與修改訂閱，但是不會刪除現有的訂閱。 現有的訂閱會繼續執行，直到刪除為止。 若要移除權限：  
  
1.  開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 
  
2.  連接至 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器。  
  
3.  展開 [安全性]  節點。  
  
4.  展開 [角色]  節點，然後選取所需的角色。  
  
5.  以滑鼠右鍵按一下此角色，然後選取 [屬性]  。  
  
6.  清除**管理個別訂閱**和**管理所有訂用帳戶**工作。  
  
7.  選取 [確定]  以套用變更。

  
##  <a name="disable-delivery-extensions"></a><a name="bkmk_disable_extensions"></a> 停用傳遞延伸模組  
 在報表伺服器上安裝的所有傳遞延伸模組都會提供給有權建立給定報表之訂閱的任何使用者。 系統會自動提供和設定下列傳遞延伸模組：  
  
-   Windows 檔案共用  
  
-   SharePoint 文件庫 (只能從與 SharePoint 整合模式報表伺服器整合的 SharePoint 網站使用)  
  
 您必須先設定電子郵件傳遞，然後才能使用它。 如果您沒有設定它，便無法使用它。 如需詳細資訊，請參閱[電子郵件設定 - Reporting Services 原生模式 (組態管理員)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)。  
  
 如果您想要關閉特定延伸模組，可以在 **RSReportServer.config** 檔中移除延伸模組項目。 如需詳細資訊，請參閱 [Reporting Services 組態檔](../../reporting-services/report-server/reporting-services-configuration-files.md)和[電子郵件設定 - Reporting Services 原生模式 (組態管理員)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)。  
  
 在您移除傳遞延伸模組之後，就無法再於入口網站或 SharePoint 網站中使用它。 移除傳遞延伸模組可能會產生非使用中訂閱。 移除延伸模組之前，請務必刪除訂閱，或將它們設定為使用不同的傳遞延伸模組。  
  
## <a name="see-also"></a>另請參閱  
 [訂閱與傳遞 &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Reporting Services 組態檔](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [設定入口網站](../../reporting-services/report-server/configure-web-portal.md)   
 [Reporting Services 報表伺服器 &#40;原生模式&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [報表伺服器的入口網站 (SSRS 原生模式)](../../reporting-services/web-portal-ssrs-native-mode.md)   
 [安全性實體項目](../../reporting-services/security/securable-items.md) 
