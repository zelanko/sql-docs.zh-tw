---
title: 實作傳遞延伸模組的 IDeliveryExtension 介面 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], attributes
- delivery extensions [Reporting Services], class creation
- IDeliveryExtension interface
ms.assetid: ab0344db-510b-403f-8dbf-b9831553765d
caps.latest.revision: 36
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 1f00fb1249254cf0adbcba84babe94e967b281b9
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2018
ms.locfileid: "40393999"
---
# <a name="implementing-the-ideliveryextension-interface-for-a-delivery-extension"></a>實作傳遞延伸模組的 IDeliveryExtension 介面
  您的傳遞延伸模組類別是用以根據通知的內容，將報告通知傳遞給使用者。 傳遞延伸模組類別也提供基礎結構，以驗證傳遞給傳遞延伸模組的使用者設定。 此外，您的傳遞延伸模組類別應該包含特定的屬性，讓用戶端可用以取得有關延伸模組的名稱、延伸模組支援的設定，以及可供傳遞延伸模組使用的轉譯格式。  
  
 ![IDeliveryExtension 介面處理](../../media/bk-ext-02.gif "IDeliveryExtension 介面處理")  
IDeliveryExtension 介面允許使用者資料的驗證以及供用戶端了解必要的傳遞設定  
  
 若要建立傳遞延伸模組類別，請實作 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 與 <xref:Microsoft.ReportingServices.Interfaces.IExtension>。 **IDeliveryExtension** 介面允許傳遞延伸模組使用 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> 方法來傳遞報表通知，並使用 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ValidateUserData%2A> 方法來驗證內送延伸模組設定。 **IExtension** 介面允許您的傳遞延伸模組實作當地語系化延伸模組名稱，並處理儲存在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 設定檔中的延伸模組特定設定資訊。 透過實作 **IExtension**，您的傳遞延伸模組包含 <xref:Microsoft.ReportingServices.Interfaces.Extension.LocalizedName%2A> 屬性。 強烈建議 [!INCLUDE[ssRS](../../../includes/ssrs.md)] 傳遞延伸模組支援 **LocalizedName** 屬性，這樣使用者就會在使用者介面中遇到延伸模組的熟悉名稱，例如報表管理員。  
  
 您的傳遞延伸模組也必須實作 **IDeliveryExtension** 介面的 **ExtensionSettings** 屬性。 報表伺服器會使用 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ExtensionSettings%2A> 屬性傳回的值，來評估傳遞延伸模組所需的設定。 與傳遞延伸模組互動的用戶端，會使用報表伺服器 Web 服務的 <xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A> 方法，來為傳遞延伸模組傳回設定清單。  
  
 您也可以使用傳遞延伸模組類別，來擷取和處理儲存在 RSReportServer.config 檔案中的自訂組態資料。 如需有關處理自訂組態資料的詳細資訊，請參閱＜<xref:Microsoft.ReportingServices.Interfaces.IExtension.SetConfiguration%2A>＞方法。  
  
 如需範例 **IDeliveryExtension** 類別實作，請參閱 [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889) (SQL Server Reporting Services 產品範例)。  
  
## <a name="see-also"></a>另請參閱  
 [實作傳遞延伸模組](../delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 延伸模組程式庫](../reporting-services-extension-library.md)  
  
  
