---
title: "使用我的訂閱 （原生模式報表伺服器） |Microsoft 文件"
ms.custom: 
ms.date: 07/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subscriptions [Reporting Services], My Subscriptions page
- My Subscriptions page [Reporting Services]
ms.assetid: e96623ba-677e-4748-8787-f32bed3b5c12
caps.latest.revision: 40
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: bc870d25cc341f84909e595cde4a411fecbf6603
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="use-my-subscriptions-native-mode-report-server"></a>使用我的訂閱 (原生模式報表伺服器)
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]入口網站包含**我的訂閱**頁面，將組織的所有訂閱到一個地方。 您可以使用*我的訂閱*檢視、 修改、 啟用、 停用，以及刪除現有的訂閱。 然而，無法用它來建立訂閱。  [我的訂閱] 僅顯示您所建立的訂閱。 即使您已經加入成為其他使用者擁有之訂閱的訂閱者，它一樣不會列出其他使用者擁有的訂閱，也不會顯示資料驅動訂閱。
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式|  
  
因為您無法依名稱搜尋訂閱，所以搜尋欄位將動態篩選訂閱清單，也無法根據觸發程序資訊、狀態資訊等等來搜尋訂閱。 如需詳細資訊，請參閱 [建立和管理原生模式報表伺服器的訂閱](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)。
  
## <a name="to-open-the-my-subscriptions-page"></a>若要開啟我的訂閱頁面  
1. 開啟 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] Web 入口網站。
2. 按一下 [設定] ![ssrs_portal_settings_gear](../../reporting-services/subscriptions/media/ssrs-portal-settings-gear.png) (位於工具列中)。
3. 按一下 [我的訂閱]。

如需詳細資訊，請參閱 [Web portal (SSRS Native Mode)](../../reporting-services/web-portal-ssrs-native-mode.md)。

## <a name="use-windows-powershell-to-list-mysubscriptions"></a>使用 Windows PowerShell 來列出 MySubscriptions  
 ![PowerShell 相關內容](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 相關內容")  
  
 下列 PowerShell 指令碼將會傳回目前使用者的訂閱和訂閱屬性清單。 如需詳細資訊，請參閱 [ReportingService2010.ListMySubscriptions 方法](http://technet.microsoft.com/library/reportservice2010.reportingservice2010.listmysubscriptions.aspx)。  
  
```  
#server -  all subscriptions of the current user at the given server or site  
$server="[server name]/reportserver"  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
  
$subscriptions=ListMySubscriptions(ItemPathOrSiteURL)  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status  
#uncomment the following to list all the subscription properties  
#$subscriptions

```  
  
## <a name="see-also"></a>請參閱＜  
 [資料驅動訂閱](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [訂閱和傳遞 &#40;Reporting Services &#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [old_ 建立及管理原生模式報表伺服器的訂閱](http://msdn.microsoft.com/en-us/7f46cbdb-5102-4941-bca2-5e0ff9012c6b)  
  
  

