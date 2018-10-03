---
title: 使用傳遞延伸模組的 IDeliveryReportServerInformation 介面 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- IDeliveryReportServerInformation interface
- delivery extensions [Reporting Services], retrieving report server information
ms.assetid: adbce647-18f3-470c-8114-42f8bcc95dc2
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d5198b839c0d11821f586f8f3c403c0bcdf96367
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48222830"
---
# <a name="using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension"></a>使用傳遞延伸模組的 IDeliveryReportServerInformation 介面
  <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation> 介面會公開您可用以擷取有關報表伺服器資訊的一些屬性。 您可以使用此資訊來傳遞通知和報表。 當實作傳遞延伸模組類別時，會實作 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ReportServerInformation%2A> 介面所需的 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 屬性。 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ReportServerInformation%2A> 屬性會傳回實作 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation> 介面的物件。 從這個物件，您可以取得報表伺服器目前支援的轉譯延伸模組清單。  
  
 下列`for`迴圈可用來在報表伺服器上儲存一份目前可用的轉譯延伸模組**ArrayList**物件。  
  
```vb  
Dim renderFormats As New ArrayList()  
Dim e As Microsoft.ReportingServices.Interfaces.Extension  
For Each e In  ReportServerInformation.RenderingExtension  
   If e.Visible Then  
      renderFormats.Add(e.Name)  
   End If  
Next e  
```  
  
```csharp  
ArrayList renderFormats = new ArrayList();  
foreach (Microsoft.ReportingServices.Interfaces.Extension e in ReportServerInformation.RenderingExtension)  
{   
   if (e.Visible)  
   {  
      renderFormats.Add(e.Name);  
   }  
}  
```  
  
 如需 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation> 介面的詳細資訊，請參閱[使用傳遞延伸模組的 IDeliveryReportServerInformation 介面](using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension.md)。  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.ReportingServices.Interfaces>   
 [實作傳遞延伸模組](implementing-a-delivery-extension.md)   
 [Reporting Services 延伸模組程式庫](../reporting-services-extension-library.md)  
  
  
