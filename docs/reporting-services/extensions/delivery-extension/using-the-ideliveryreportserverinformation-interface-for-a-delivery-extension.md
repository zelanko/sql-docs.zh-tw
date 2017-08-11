---
title: "使用傳遞延伸模組的 IDeliveryReportServerInformation 介面 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
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
- IDeliveryReportServerInformation interface
- delivery extensions [Reporting Services], retrieving report server information
ms.assetid: adbce647-18f3-470c-8114-42f8bcc95dc2
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: caebc70ede4475cef103d0d76598ea3125231252
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension"></a>使用傳遞延伸模組的 IDeliveryReportServerInformation 介面
  <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation> 介面會公開您可用以擷取有關報表伺服器資訊的一些屬性。 您可以使用此資訊來傳遞通知和報表。 當實作傳遞延伸模組類別時，會實作 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ReportServerInformation%2A> 介面所需的 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 屬性。 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ReportServerInformation%2A> 屬性會傳回實作 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation> 介面的物件。 從這個物件，您可以取得報表伺服器目前支援的轉譯延伸模組清單。  
  
 下列**如**迴圈可用來儲存在報表伺服器上的目前可用的轉譯延伸模組清單**ArrayList**物件。  
  
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
  
 如需有關<xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation>介面，請參閱[使用傳遞延伸模組的 IDeliveryReportServerInformation 介面](../../../reporting-services/extensions/delivery-extension/using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension.md)。  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.ReportingServices.Interfaces>   
 [實作傳遞延伸模組](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
