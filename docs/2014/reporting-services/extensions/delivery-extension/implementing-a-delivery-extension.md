---
title: 實作傳遞延伸模組 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- delivery [Reporting Services]
- custom delivery extensions [Reporting Services]
- extensions [Reporting Services], delivery
- delivery extensions [Reporting Services]
ms.assetid: 600cd229-efcd-480e-8c95-3c3c39ff4e7a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cae33496e4dddcaf2d14ba2d87f0d4013795e58f
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "60158524"
---
# <a name="implementing-a-delivery-extension"></a>實作傳遞延伸模組
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 可讓使用者建立和發行報表，一旦建立和發行，就可以傳遞給各個位置。 除此之外，[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 包括數個傳遞延伸模組以及一個傳遞 API，可讓開發人員建立其他的傳遞延伸模組，以進一步擴充在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的傳遞功能。  
  
 如需傳遞延伸模組的範例實作，請參閱 [SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889) (SQL Server Reporting Services 產品範例)。  
  
## <a name="in-this-section"></a>本節內容  
 [傳遞延伸模組概觀] 傳遞-擴充功能-overview.md)  
 介紹如何為 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 撰寫自訂傳遞延伸模組。  
  
 [準備實作傳遞延伸模組](preparing-to-implement-a-delivery-extension.md)  
 描述實作 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 傳遞延伸模組時可用的介面與類別，以及在實作之前要考慮的問題。  
  
 [建立傳遞延伸模組程式庫](creating-a-delivery-extension-library.md)  
 描述為 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 傳遞延伸模組指派命名空間，以及將傳遞延伸模組編譯成為程式庫 DLL。  
  
 [實作傳遞延伸模組的 IDeliveryExtension 介面](implementing-the-ideliveryextension-interface-for-a-delivery-extension.md)  
 描述傳遞延伸模組的屬性，以及如何實作自己的傳遞延伸模組類別。  
  
 [使用傳遞延伸模組的通知類別](using-a-notification-class-for-a-delivery-extension.md)  
 描述 **Notification** 類別的屬性，以及如何在傳遞延伸模組實作中使用它。  
  
 [使用傳遞延伸模組的設定類別](using-the-setting-class-for-a-delivery-extension.md)  
 描述 **Setting** 類別的屬性，以及如何在傳遞延伸模組實作中使用它。  
  
 [使用傳遞延伸模組的 IDeliveryReportServerInformation 介面](using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension.md)  
 描述 **IDeliveryReportServerInformation** 介面的屬性，以及如何在傳遞延伸模組實作中使用它。  
  
 [使用傳遞延伸模組的報表類別](using-the-report-class-for-a-delivery-extension.md)  
 描述 **Report** 類別的屬性，以及如何在傳遞延伸模組實作中使用它。  
  
 [使用傳遞延伸模組的 RenderedOutputFile 類別](using-the-renderedoutputfile-class-for-a-delivery-extension.md)  
 描述 **RenderedOutputFile** 類別的屬性，以及如何在傳遞延伸模組實作中使用它。  
  
 [實作傳遞延伸模組的 ISubscriptionBaseUIUserControl 介面](implementing-the-isubscriptionbaseuiusercontrol-interface.md)  
 描述傳遞延伸模組使用者控制項的屬性，以及如何為訂閱實作自己的使用者介面。  
  
 [部署傳遞延伸模組](deploying-a-delivery-extension.md)  
 描述如何部署您的傳遞延伸模組。  
  
 [對傳遞延伸模組程式碼進行偵錯](debugging-delivery-extension-code.md)  
 描述如何偵錯您的傳遞延伸模組中的程式碼。  
  
 [移除傳遞延伸模組](removing-a-delivery-extension.md)  
 描述如何從報表伺服器移除傳遞延伸模組。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../reporting-services-extensions.md)   
 [Reporting Services 延伸模組程式庫](../reporting-services-extension-library.md)  
  
  
