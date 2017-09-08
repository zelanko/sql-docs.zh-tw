---
title: "實作傳遞延伸模組的 IDeliveryExtension 介面 |Microsoft 文件"
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
- delivery extensions [Reporting Services], attributes
- delivery extensions [Reporting Services], class creation
- IDeliveryExtension interface
ms.assetid: ab0344db-510b-403f-8dbf-b9831553765d
caps.latest.revision: 37
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: ac54345b14ba3ff84a755e0ce4e8b1c4e9acab13
ms.contentlocale: zh-tw
ms.lasthandoff: 08/12/2017

---
# <a name="implementing-the-ideliveryextension-interface-for-a-delivery-extension"></a>實作傳遞延伸模組的 IDeliveryExtension 介面
  您的傳遞延伸模組類別是用以根據通知的內容，將報告通知傳遞給使用者。 傳遞延伸模組類別也提供基礎結構，以驗證傳遞給傳遞延伸模組的使用者設定。 此外，您的傳遞延伸模組類別應該包含特定的屬性，讓用戶端可用以取得有關延伸模組的名稱、延伸模組支援的設定，以及可供傳遞延伸模組使用的轉譯格式。  
  
 ![IDeliveryExtension 介面處理](../../../reporting-services/extensions/delivery-extension/media/bk-ext-02.gif "IDeliveryExtension 介面處理程序")  
IDeliveryExtension 介面允許使用者資料的驗證以及供用戶端了解必要的傳遞設定  
  
 若要建立傳遞延伸模組類別，請實作 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 與 <xref:Microsoft.ReportingServices.Interfaces.IExtension>。 **IDeliveryExtension**介面可讓您的傳遞延伸模組，以傳遞報表通知使用<xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A>方法以及驗證內送延伸模組的設定，使用<xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ValidateUserData%2A>方法。 **IExtension**介面可讓您傳遞延伸模組實作當地語系化延伸模組名稱，並處理延伸模組特定組態資訊儲存在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]組態檔。 藉由實作**IExtension**，傳遞延伸模組包含<xref:Microsoft.ReportingServices.Interfaces.Extension.LocalizedName%2A>屬性。 強烈建議，[!INCLUDE[ssRS](../../../includes/ssrs-md.md)]傳遞延伸模組支援**LocalizedName**屬性，以便使用者遇到使用者介面，例如報表管理員中的延伸模組的熟悉名稱。  
  
 傳遞延伸模組也必須實作**ExtensionSettings**屬性**IDeliveryExtension**介面。 報表伺服器會使用 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ExtensionSettings%2A> 屬性傳回的值，來評估傳遞延伸模組所需的設定。 與傳遞延伸模組互動的用戶端，會使用報表伺服器 Web 服務的 <xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A> 方法，來為傳遞延伸模組傳回設定清單。  
  
 您也可以使用傳遞延伸模組類別，來擷取和處理儲存在 RSReportServer.config 檔案中的自訂組態資料。 如需有關處理自訂組態資料的詳細資訊，請參閱＜<xref:Microsoft.ReportingServices.Interfaces.IExtension.SetConfiguration%2A>＞方法。  
  
 如需範例**IDeliveryExtension**類別的實作，請參閱[SQL Server Reporting Services 產品範例](http://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="see-also"></a>另請參閱  
 [實作傳遞延伸模組](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
