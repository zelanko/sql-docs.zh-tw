---
title: 實作傳遞延伸模組的 ISubscriptionBaseUIUserControl 介面 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- user controls [Reporting Services]
- ISubscriptionBaseUIUserControl interface
- delivery extensions [Reporting Services], user controls
ms.assetid: a1e9122c-aa0b-45de-b536-4f1202875ab1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2664d71243d98e9b8152c5c5c7ce241a4f3669f8
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "60156622"
---
# <a name="implementing-the-isubscriptionbaseuiusercontrol-interface-for-a-delivery-extension"></a>實作傳遞延伸模組的 ISubscriptionBaseUIUserControl 介面
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 傳遞延伸模組可以包含訂閱使用者介面 (UI) 的實作，以收集報表管理員中延伸模組的特定資訊。 當使用者建立新訂閱或是修改現有的訂閱時，會叫用 UI。 當建立新訂閱時，UI 會顯示適當的預設值，並允許使用者與傳遞提供者互動。 當修改訂閱時，會使用目前訂閱中的資訊來預先擴展 UI。  
  
 傳遞延伸模組以 ASP.NET 使用者控制項的方式提供訂閱 UI。 報表伺服器在顯示訂閱 UI 時，會合併傳遞延伸模組所定義的使用者控制項。 提供抽象方法以啟用此功能的基底介面是 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 介面。 這個介面可確保會正確執行一般作業，例如輸出值的驗證。 此外，基底使用者控制項提供一組報表伺服器所使用的預設屬性，以便在訂閱之間取得一致性。 與報表管理員整合在一起的傳遞延伸模組需要這些屬性。  
  
 您可以在傳遞提供者中實作 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 介面，才能建立報表管理員的訂閱 UI。 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 介面提供的基礎結構可讓使用者輸入訂閱設定值，以處理傳遞延伸模組以及驗證設定所需的設定。  
  
> [!NOTE]  
>  您需要將 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 介面實作為傳遞延伸模組的一部分。 使用傳遞延伸模組的訂閱永遠都可以改透過 SOAP API 方法 <xref:ReportService2010.ReportingService2010.CreateSubscription%2A> 與 <xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A> 來建立。 如需 SOAP API 功能以管理訂閱和傳遞的詳細資訊，請參閱[訂閱與傳遞方法](../../report-server-web-service/methods/subscription-and-delivery-methods.md)。  
  
 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 介面會擴充 <xref:Microsoft.ReportingServices.Interfaces.IExtension>。 實作 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 的使用者控制項，也必須繼承自 **System.Web.UI.WebControls.WebControl**。 如需 **WebControl** 類別的詳細資訊，請參閱《[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 開發人員指南》。  
  
 如需如何使用 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 介面的範例，請參閱 [SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889) (SQL Server Reporting Services 產品範例)。  
  
## <a name="see-also"></a>另請參閱  
 [實作傳遞延伸模組](implementing-a-delivery-extension.md)   
 [Reporting Services 延伸模組程式庫](../reporting-services-extension-library.md)  
  
  
