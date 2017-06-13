---
title: "實作 ISubscriptionBaseUIUserControl 介面 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- user controls [Reporting Services]
- ISubscriptionBaseUIUserControl interface
- delivery extensions [Reporting Services], user controls
ms.assetid: a1e9122c-aa0b-45de-b536-4f1202875ab1
caps.latest.revision: 35
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 5b509345723b137941c2f00c054c77f076035dc2
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="implementing-the-isubscriptionbaseuiusercontrol-interface"></a>實作 ISubscriptionBaseUIUserControl 介面
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 傳遞延伸模組可以包含訂閱使用者介面 (UI) 的實作，以收集報表管理員中延伸模組的特定資訊。 當使用者建立新訂閱或是修改現有的訂閱時，會叫用 UI。 當建立新訂閱時，UI 會顯示適當的預設值，並允許使用者與傳遞提供者互動。 當修改訂閱時，會使用目前訂閱中的資訊來預先擴展 UI。  
  
 傳遞延伸模組以 ASP.NET 使用者控制項的方式提供訂閱 UI。 報表伺服器在顯示訂閱 UI 時，會合併傳遞延伸模組所定義的使用者控制項。 提供抽象方法以啟用此功能的基底介面是 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 介面。 這個介面可確保會正確執行一般作業，例如輸出值的驗證。 此外，基底使用者控制項提供一組報表伺服器所使用的預設屬性，以便在訂閱之間取得一致性。 與報表管理員整合在一起的傳遞延伸模組需要這些屬性。  
  
 您可以在傳遞提供者中實作 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 介面，才能建立報表管理員的訂閱 UI。 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 介面提供的基礎結構可讓使用者輸入訂閱設定值，以處理傳遞延伸模組以及驗證設定所需的設定。  
  
> [!NOTE]  
>  您需要將 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 介面實作為傳遞延伸模組的一部分。 使用傳遞延伸模組的訂閱永遠都可以改透過 SOAP API 方法 <xref:ReportService2010.ReportingService2010.CreateSubscription%2A> 與 <xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A> 來建立。 如需用於管理訂閱與傳遞的 SOAP API 功能的詳細資訊，請參閱[Subscription and Delivery Methods](../../../reporting-services/report-server-web-service/methods/subscription-and-delivery-methods.md)。  
  
 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 介面會擴充 <xref:Microsoft.ReportingServices.Interfaces.IExtension>。 使用者控制項實作<xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl>也必須繼承自**System.Web.UI.WebControls.WebControl**。 如需有關**WebControl**類別，請參閱您[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]開發人員手冊 》。  
  
 如需如何使用的範例<xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl>介面，請參閱[SQL Server Reporting Services 產品範例](http://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="see-also"></a>另請參閱  
 [實作傳遞延伸模組](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
