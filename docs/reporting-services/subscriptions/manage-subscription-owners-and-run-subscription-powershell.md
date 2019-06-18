---
title: 管理訂閱擁有者及執行訂閱 - PowerShell | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 04/26/2019
ms.openlocfilehash: 4beecb52ef0f65b29f3508d8123480e219d30abd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580603"
---
# <a name="manage-subscription-owners-and-run-subscription---powershell"></a>管理訂閱擁有者及執行訂閱

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

從 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 開始，您可以用程式設計方式，將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱的擁有權，從某位使用者轉移到另一位使用者。 本主題提供數個 Windows PowerShell 指令碼，供您可變更或單純列出訂閱擁有權時使用。 每項範例均包含原生模式和 SharePoint 模式的範例語法。 當您變更訂閱擁有者之後，便會在新擁有者的安全性內容中執行訂閱，且報表中的 [User!UserID] 欄位會顯示新擁有者的值。 如需 PowerShell 範例呼叫的物件模型詳細資訊，請參閱 <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>  

![PowerShell 相關內容](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 相關內容")

##  <a name="bkmk_top"></a> 本主題內容：
  
- [如何使用指令碼](#bkmk_how_to)  
  
- [指令碼：列出所有訂閱的擁有權](#bkmk_list_ownership_all)  
  
- [指令碼：列出特定使用者擁有的所有訂閱](#bkmk_list_all_one_user)  
  
- [指令碼：針對特定使用者擁有的所有訂閱變更擁有權](#bkmk_change_all)  
  
- [指令碼：列出與特定報表相關聯的所有訂閱](#bkmk_list_for_1_report)  
  
- [指令碼：變更特定訂閱的擁有權](#bkmk_change_all_1_subscription)  
  
- [指令碼：執行 (觸發) 單一訂閱](#bkmk_run_1_subscription)  
  
## <a name="bkmk_how_to"></a> 如何使用指令碼
  
### <a name="permissions"></a>權限

本節針對原生及 SharePoint 模式 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，摘要說明使用每個方法所需的權限等級。 本主題中的指令碼使用下列 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 方法：  
  
- [ReportingService2010.ListSubscriptions 方法](https://msdn.microsoft.com/library/reportservice2010.reportingservice2010.listsubscriptions.aspx)  
  
- [ReportingService2010.ChangeSubscriptionOwner 方法](https://msdn.microsoft.com/library/reportservice2010.reportingservice2010.changesubscriptionowner.aspx)  
  
- [ReportingService2010.ListChildren](https://msdn.microsoft.com/library/reportservice2010.reportingservice2010.listchildren.aspx)  
  
- 觸發要執行的特訂訂閱時，才需要在最後一個指令碼中使用 [ReportingService2010.FireEvent](https://msdn.microsoft.com/library/reportservice2010.reportingservice2010.fireevent.aspx) (機器翻譯) 方法。 若您不打算使用該指令碼，可以跳過 FireEvent 方法所需的權限需求。  
  
**原生模式：**
  
- 列出訂閱：(報表的 [ReportOperation Enumeration](https://msdn.microsoft.com/library/microsoft.reportingservices.interfaces.reportoperation.aspx) ，且使用者是訂閱擁有者)，或是 ReadAnySubscription。  
  
- 變更訂閱：使用者必須是 BUILTIN\Administrators 群組的成員  
  
- 列出子系：項目的 ReadProperties  
  
- 觸發事件：GenerateEvents (系統)  
  
 **SharePoint 模式：**
  
- 列出訂閱：ManageAlerts 或 (報表的 [CreateAlerts](https://msdn.microsoft.com/library/microsoft.sharepoint.spbasepermissions.aspx) ，且使用者是訂閱擁有者，同時訂閱為定時的訂閱)。  
  
- 變更訂閱：ManageWeb  
  
- 列出子系：ViewListItems  
  
- 觸發事件：ManageWeb  
  
 如需詳細資訊，請參閱 [將 Reporting Services 中的角色和工作與 SharePoint 群組和權限做比較](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)。  
  
### <a name="script-usage"></a>指令碼使用方式

**建立指令碼檔案 (.ps1)**
  
1. 建立名為 **c:\scripts**的資料夾。 若您選擇其他資料夾，則請修改範例命令列陳述式語法中使用的資料夾名稱。  
  
2. 為每個指令碼建立文字檔，然後將檔案儲存至 c:\scripts 資料夾。 當您建立 .ps1 檔案時，請使用每個範例命令列語法中的名稱。  
  
3. 以系統管理權限開啟命令提示字元。  
  
4. 執行每個指令碼檔案時，請使用每個範例所提供的範例命令列語法。  
  
**測試的環境**
  
 本主題中的指令碼測試於 PowerShell 第 3 版，並使用下列版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]：  
  
- [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
- [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
- [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
## <a name="bkmk_list_ownership_all"></a> 指令碼：列出所有訂閱的擁有權

此指令碼會列出網站的所有訂閱。 您可以使用此指令碼測試您的連線，或是確認其他指令碼中使用的報表路徑及訂閱識別碼。 若要單純稽核有哪些訂閱以及誰擁有這些訂閱，這會是很實用的指令碼。  
  
 **原生模式語法：**
  
```powershell
powershell c:\scripts\ListAll_SSRS_Subscriptions.ps1 "[server]/reportserver" "/"  
```  
  
 **SharePoint 模式語法：**
  
```powershell
powershell c:\scripts\ListAll_SSRS_Subscriptions.ps1 "[server]/_vti_bin/reportserver" "https://[server]"  
```  
  
 **指令碼：**
  
```
# Parameters  
#    server   - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
  
Param(  
    [string]$server,  
    [string]$site  
   )  
  
$rs2010 += New-WebServiceProxy -Uri "https://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
$subscriptions += $rs2010.ListSubscriptions($site); # use "/" for default native mode site  
  
Write-Host " "  
Write-Host "----- $server's Subscriptions: "  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted, Status  
```  
  
> [!TIP]  
> 若要以 SharePoint 模式確認網站 URL，請使用 SharePoint Cmdlet **Get-SPSite**。 如需詳細資訊，請參閱 [Get-SPSite](https://msdn.microsoft.com/library/ff607950\(v=office.15\).aspx)。  
  
##  <a name="bkmk_list_all_one_user"></a> 指令碼：列出特定使用者擁有的所有訂閱

此指令碼會列出特定使用者所擁有的所有訂閱。 您可以使用此指令碼測試您的連線，或是確認其他指令碼中使用的報表路徑及訂閱識別碼。 當您組織中有人離開而您想要確認該人員擁有那些訂閱，好讓您變更擁有者或刪除訂閱時，此指令碼相當實用。  
  
 **原生模式語法：**
  
```powershell
powershell c:\scripts\ListAll_SSRS_Subscriptions4User.ps1 "[Domain]\[user]" "[server]/reportserver" "/"  
```  
  
**SharePoint 模式語法：**
  
```powershell
powershell c:\scripts\ListAll_SSRS_Subscriptions4User.ps1 "[Domain]\[user]"  "[server]/_vti_bin/reportserver" "https://[server]"  
```  
  
**指令碼：**
  
```
# Parameters:  
#    currentOwner - DOMAIN\USER that owns the subscriptions you wish to change  
#    server        - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
#    site        - use "/" for default native mode site  
Param(  
    [string]$currentOwner,  
    [string]$server,  
    [string]$site  
)  
  
$rs2010 = New-WebServiceProxy -Uri "https://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
$subscriptions += $rs2010.ListSubscriptions($site);  
  
Write-Host " "  
Write-Host " "  
Write-Host "----- $currentOwner's Subscriptions: "  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status | where {$_.owner -eq $currentOwner}  
```  
  
## <a name="bkmk_change_all"></a> 指令碼：針對特定使用者擁有的所有訂閱變更擁有權

此指令碼會將特定使用者擁有的所有訂閱擁有權變更至新擁有者參數。  
  
**原生模式語法：**  
  
```powershell
powershell c:\scripts\ChangeALL_SSRS_SubscriptionOwner.ps1 "[Domain]\current owner]" "[Domain]\[new owner]" "[server]/reportserver"  
```  
  
**SharePoint 模式語法：**  
  
```powershell
powershell c:\scripts\ChangeALL_SSRS_SubscriptionOwner.ps1 "[Domain]\{current owner]" "[Domain]\[new owner]" "[server]/_vti_bin/reportserver"  
```  
  
**指令碼：**  
  
```
# Parameters:  
#    currentOwner - DOMAIN\USER that owns the subscriptions you wish to change  
#    newOwner      - DOMAIN\USER that will own the subscriptions you wish to change  
#    server        - server and instance name (e.g. myserver/reportserver, myserver/reportserver_db2, myserver/_vti_bin/reportserver)
  
Param(  
    [string]$currentOwner,  
    [string]$newOwner,  
    [string]$server  
)  
  
$rs2010 = New-WebServiceProxy -Uri "https://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
$items = $rs2010.ListChildren("/", $true);  
  
$subscriptions = @();  
  
ForEach ($item in $items)  
{  
    if ($item.TypeName -eq "Report")  
    {  
        $curRepSubs = $rs2010.ListSubscriptions($item.Path);  
        ForEach ($curRepSub in $curRepSubs)  
        {  
            if ($curRepSub.Owner -eq $previousOwner)  
            {  
                $subscriptions += $curRepSub;  
            }  
        }  
    }  
}  
  
Write-Host " "  
Write-Host " "  
Write-Host -foregroundcolor "green" "-----  $currentOwner's Subscriptions changing ownership to $newOwner : "  
$subscriptions | select SubscriptionID, Owner, Path, Description,  Status  | format-table -AutoSize  
  
ForEach ($sub in $subscriptions)  
{  
    $rs2010.ChangeSubscriptionOwner($sub.SubscriptionID, $newOwner);  
}  
  
$subs2 = @();  
  
ForEach ($item in $items)  
{  
    if ($item.TypeName -eq "Report")  
    {  
        $subs2 += $rs2010.ListSubscriptions($item.Path);  
    }  
}  
```  
  
## <a name="bkmk_list_for_1_report"></a> 指令碼：列出與特定報表相關聯的所有訂閱  

此指令碼會列出與特定報表相關聯的所有訂閱。 不同之處在於 SharePoint 模式的報表路徑語法，需要完整的 URL。 在語法範例中，使用的報表名稱是 "title only"，其中包含空格，因此需要以單引號將報表名稱括住。  
  
**原生模式語法：**  
  
```powershell
powershell c:\scripts\List_SSRS_One_Reports_Subscriptions.ps1 "[server]/reportserver" "'/reports/title only'" "/"  
```  
  
**SharePoint 模式語法：**  
  
```powershell
powershell c:\scripts\List_SSRS_One_Reports_Subscriptions.ps1 "[server]/_vti_bin/reportserver"  "'https://[server]/shared documents/title only.rdl'" "https://[server]"  
```  
  
**指令碼：**  
  
```
# Parameters:  
#    server      - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
#    reportpath  - path to report in the report server, including report name e.g. /reports/test report >> pass in  "'/reports/title only'"  
#    site        - use "/" for default native mode site  
Param  
(  
      [string]$server,  
      [string]$reportpath,  
      [string]$site  
)  
  
$rs2010 = New-WebServiceProxy -Uri "https://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
$subscriptions += $rs2010.ListSubscriptions($site);  
  
Write-Host " "  
Write-Host " "  
Write-Host "----- $reportpath 's Subscriptions: "  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status | where {$_.path -eq $reportpath}  
```  
  
## <a name="bkmk_change_all_1_subscription"></a> 指令碼：變更特定訂閱的擁有權  
 此指令碼會變更特定訂閱的擁有權。 訂閱由您傳遞至指令碼中的 SubscriptionID 所識別。 您可以使用其中一個列出訂閱的指令碼，以判斷正確的 SubscriptionID。  
  
 **原生模式語法：**  
  
```powershell
powershell c:\scripts\Change_SSRS_Owner_One_Subscription.ps1 "[Domain]\[new owner]" "[server]/reportserver" "/" "ac5637a1-9982-4d89-9d69-a72a9c3b3150"  
```  
  
 **SharePoint 模式語法：**  
  
```powershell
powershell c:\scripts\Change_SSRS_Owner_One_Subscription.ps1 "[Domain]\[new owner]" "[server]/_vti_bin/reportserver" "https://[server]" "9660674b-f020-453f-b1e3-d9ba37624519"  
```  
  
 **指令碼：**  
  
```
# Parameters:  
#    newOwner       - DOMAIN\USER that will own the subscriptions you wish to change  
#    server         - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
#    site        - use "/" for default native mode site  
#    subscriptionID - guid for the single subscription to change  
  
Param(  
    [string]$newOwner,  
    [string]$server,  
    [string]$site,  
    [string]$subscriptionid  
   )  
$rs2010 = New-WebServiceProxy -Uri "https://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
  
$subscription += $rs2010.ListSubscriptions($site) | where {$_.SubscriptionID -eq $subscriptionid};  
  
Write-Host " "  
Write-Host "----- $subscriptionid's Subscription properties: "  
$subscription | select Path, report, Description, SubscriptionID, Owner, Status  
  
$rs2010.ChangeSubscriptionOwner($subscription.SubscriptionID, $newOwner)  
  
#refresh the list  
$subscription = $rs2010.ListSubscriptions($site) | where {$_.SubscriptionID -eq $subscriptionid}; # use "/" for default native mode site  
Write-Host "----- $subscriptionid's Subscription properties: "  
$subscription | select Path, report, Description, SubscriptionID, Owner, Status  
```  
  
## <a name="bkmk_run_1_subscription"></a> 指令碼：執行 (觸發) 單一訂閱  

此指令碼會使用 FireEvent 方法執行特定訂閱。 無論為訂閱的設定排程為何，指令碼都會立即執行該訂閱。 EventType 會根據定義在報表伺服器組態檔 **rsreportserver.config** 中已知的事件集合進行比對。此指令碼會為標準訂閱使用下列事件類型：  
  
 `<Event>`  
  
 `<Type>TimedSubscription</Type>`  
  
 `</Event>`  
  
 如需組態檔的詳細資訊，請參閱 [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)。  
  
 指令碼包含延遲邏輯 "`Start-Sleep -s 6`"，所以在觸發事件之後會有時間，以透過 ListSubscription 方法取得更新的狀態。  
  
 **原生模式語法：**  
  
```powershell
powershell c:\scripts\FireSubscription.ps1 "[server]/reportserver" $null "70366e82-2d3c-4edd-a216-b97e51e26de9"  
```  
  
 **SharePoint 模式語法：**  
  
```powershell
powershell c:\scripts\FireSubscription.ps1 "[server]/_vti_bin/reportserver" "https://[server]" "c3425c72-580d-423e-805a-41cf9799fd25"  
```  
  
 **指令碼：**  
  
```
  
# Parameters  
#    server         - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
#    site           - use $null for a native mode server  
#    subscriptionid - subscription guid  
  
Param(  
  [string]$server,  
  [string]$site,  
  [string]$subscriptionid  
  )  
  
$rs2010 = New-WebServiceProxy -Uri "https://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
#event type is case sensative to what is in the rsreportserver.config  
$rs2010.FireEvent("TimedSubscription",$subscriptionid,$site)  
  
Write-Host " "  
Write-Host "----- Subscription ($subscriptionid) status: "  
#get list of subscriptions and filter to the specific ID to see the Status and LastExecuted  
Start-Sleep -s 6 # slight delay in processing so ListSubscription returns the updated Status and LastExecuted  
$subscriptions = $rs2010.ListSubscriptions($site);   
$subscriptions | select Status, Path, report, Description, Owner, SubscriptionID, EventType, lastexecuted | where {$_.SubscriptionID -eq $subscriptionid}  
  
```  

## <a name="see-also"></a>另請參閱  

- [ReportingService2010.ListSubscriptions 方法](https://msdn.microsoft.com/library/reportservice2010.reportingservice2010.listsubscriptions.aspx)  

- [ReportingService2010.ChangeSubscriptionOwner 方法](https://msdn.microsoft.com/library/reportservice2010.reportingservice2010.changesubscriptionowner.aspx)   

- [ReportingService2010.ListChildren](https://msdn.microsoft.com/library/reportservice2010.reportingservice2010.listchildren.aspx)  

- [ReportingService2010.FireEvent](https://msdn.microsoft.com/library/reportservice2010.reportingservice2010.fireevent.aspx)