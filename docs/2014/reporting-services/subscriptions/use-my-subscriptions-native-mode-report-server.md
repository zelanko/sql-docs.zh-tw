---
title: 使用我的訂閱 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- subscriptions [Reporting Services], My Subscriptions page
- My Subscriptions page [Reporting Services]
ms.assetid: e96623ba-677e-4748-8787-f32bed3b5c12
caps.latest.revision: 36
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: c1125792543e3a926ddb98e3d33e0f600328d232
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146869"
---
# <a name="use-my-subscriptions"></a>使用我的訂閱
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 報表管理員包括**我的訂閱**頁面，將組織的所有訂閱到一個地方。 您可以使用 [我的訂閱] 來檢視、修改和刪除現有的訂閱。 然而，無法用它來建立訂閱。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 原生模式|  
  
 在 [我的訂閱] 中，您可以依資料夾、報表、描述、觸發程序、上次執行或狀態來排序訂閱。 除了 [上次執行] 依時間順序以外，所有值都依字母順序排序。  
  
 [我的訂閱] 僅顯示您所建立的訂閱。 即使您已經加入成為其他使用者擁有之訂閱的訂閱者，它一樣不會列出其他使用者擁有的訂閱，也不會顯示資料驅動訂閱。  
  
 您無法依名稱搜尋訂閱，也無法根據觸發程序資訊、狀態資訊等等來搜尋訂閱。 如需詳細資訊，請參閱[Create，Modify，and 刪除標準訂閱&#40;原生模式的 Reporting Services&#41;](create-and-manage-subscriptions-for-native-mode-report-servers.md)。  
  
## <a name="how-to-use-my-subscriptions"></a>如何使用我的訂閱  
 我的訂閱可以透過報表管理員使用。 若要存取 我的訂閱，請按一下**我的訂閱**報表管理員通用工具列上。  
  
## <a name="use-windows-powershell-to-list-mysubscriptions"></a>使用 Windows PowerShell 來列出 MySubscriptions  
 ![PowerShell 相關內容](../media/rs-powershellicon.jpg "PowerShell 相關內容")  
  
 下列 PowerShell 指令碼將會傳回目前使用者的訂閱和訂閱屬性清單。 如需詳細資訊，請參閱 [ReportingService2010.ListMySubscriptions 方法](http://technet.microsoft.com/library/reportservice2010.reportingservice2010.listmysubscriptions.aspx)。  
  
```  
#server -  all subscriptions of the current user at the given server or site  
$server="[server name]/reportserver"  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
  
$subscriptions=ListMySubscriptions(ItemPathOrSiteURL)  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status  
#uncomment the following to list all the subscription properties  
#$subscriptions  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料驅動訂閱](data-driven-subscriptions.md)   
 [訂閱與傳遞&#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [建立及管理原生模式報表伺服器的訂閱](../create-manage-subscriptions-native-mode-report-servers.md)  
  
  