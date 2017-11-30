---
title: "實作傳遞延伸模組 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- delivery [Reporting Services]
- custom delivery extensions [Reporting Services]
- extensions [Reporting Services], delivery
- delivery extensions [Reporting Services]
ms.assetid: 600cd229-efcd-480e-8c95-3c3c39ff4e7a
caps.latest.revision: "32"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: e84b9e82afa18a9fabefeafdaa931719cf8344d0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="implementing-a-delivery-extension"></a>實作傳遞延伸模組
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 可讓使用者建立和發行報表，一旦建立和發行，就可以傳遞給各個位置。 除此之外，[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 包括數個傳遞延伸模組以及一個傳遞 API，可讓開發人員建立其他的傳遞延伸模組，以進一步擴充在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的傳遞功能。  
  
 如需傳遞延伸模組的範例實作，請參閱 [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889) (SQL Server Reporting Services 產品範例)。  
  
## <a name="in-this-section"></a>本節內容  
 [傳遞延伸模組概觀](../../../reporting-services/extensions/delivery-extension/delivery-extensions-overview.md)  
 介紹如何為 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 撰寫自訂傳遞延伸模組。  
  
 [準備實作傳遞延伸模組](../../../reporting-services/extensions/delivery-extension/preparing-to-implement-a-delivery-extension.md)  
 描述實作 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 傳遞延伸模組時可用的介面與類別，以及在實作之前要考慮的問題。  
  
 [建立傳遞延伸模組程式庫](../../../reporting-services/extensions/delivery-extension/creating-a-delivery-extension-library.md)  
 描述為 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 傳遞延伸模組指派命名空間，以及將傳遞延伸模組編譯成為程式庫 DLL。  
  
 [實作傳遞延伸模組的 IDeliveryExtension 介面](../../../reporting-services/extensions/delivery-extension/implementing-the-ideliveryextension-interface-for-a-delivery-extension.md)  
 描述傳遞延伸模組的屬性，以及如何實作自己的傳遞延伸模組類別。  
  
 [使用傳遞延伸模組的通知類別](../../../reporting-services/extensions/delivery-extension/using-a-notification-class-for-a-delivery-extension.md)  
 描述 **Notification** 類別的屬性，以及如何在傳遞延伸模組實作中使用它。  
  
 [使用傳遞延伸模組的設定類別](../../../reporting-services/extensions/delivery-extension/using-the-setting-class-for-a-delivery-extension.md)  
 描述 **Setting** 類別的屬性，以及如何在傳遞延伸模組實作中使用它。  
  
 [使用傳遞延伸模組的 IDeliveryReportServerInformation 介面](../../../reporting-services/extensions/delivery-extension/using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension.md)  
 描述 **IDeliveryReportServerInformation** 介面的屬性，以及如何在傳遞延伸模組實作中使用它。  
  
 [使用傳遞延伸模組的報表類別](../../../reporting-services/extensions/delivery-extension/using-the-report-class-for-a-delivery-extension.md)  
 描述 **Report** 類別的屬性，以及如何在傳遞延伸模組實作中使用它。  
  
 [使用傳遞延伸模組的 RenderedOutputFile 類別](../../../reporting-services/extensions/delivery-extension/using-the-renderedoutputfile-class-for-a-delivery-extension.md)  
 描述 **RenderedOutputFile** 類別的屬性，以及如何在傳遞延伸模組實作中使用它。  
  
 [實作傳遞延伸模組的 ISubscriptionBaseUIUserControl 介面](../../../reporting-services/extensions/delivery-extension/implementing-the-isubscriptionbaseuiusercontrol-interface.md)  
 描述傳遞延伸模組使用者控制項的屬性，以及如何為訂閱實作自己的使用者介面。  
  
 [部署傳遞延伸模組](../../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)  
 描述如何部署您的傳遞延伸模組。  
  
 [對傳遞延伸模組程式碼進行偵錯](../../../reporting-services/extensions/delivery-extension/debugging-delivery-extension-code.md)  
 描述如何偵錯您的傳遞延伸模組中的程式碼。  
  
 [移除傳遞延伸模組](../../../reporting-services/extensions/delivery-extension/removing-a-delivery-extension.md)  
 描述如何從報表伺服器移除傳遞延伸模組。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
