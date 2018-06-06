---
title: 使用 Detail 屬性處理特定的錯誤 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: report-server-web-service-net-framework-exception-handling
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- exceptions [Reporting Services], Detail property
- Detail property
- InnerText property
ms.assetid: 4392633d-b46b-41e6-bc12-efb64e166704
caps.latest.revision: 30
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: df197d5746e4dcf925de630225304f0e3a42fa11
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="using-the-detail-property-to-handle-specific-errors"></a>使用詳細資料屬性來處理特定的錯誤
  若要進一步分類例外狀況，[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 會在 SOAP 例外狀況的 **Detail** 屬性中，於子項目的 **InnerText** 屬性中傳回其他錯誤資訊。 因為 **Detail** 屬性是一種 **XmlNode** 物件，所以您可以使用下列程式碼來存取 **Message** 子項目的內部文字。  
  
 如需包含在 **Detail** 屬性中所有可用的子項目清單，請參閱 [Detail 屬性](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)。 如需詳細資訊，請參閱 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK 文件中的＜Detail 屬性＞。  
  
```vb  
Try  
' Code for accessing the report server  
Catch ex As SoapException  
   ' The exception is a SOAP exception, so use  
   ' the Detail property's Message element.  
   Console.WriteLine(ex.Detail("Message").InnerXml)  
End Try  
```  
  
```csharp  
try  
{  
   // Code for accessing the report server  
}  
catch (SoapException ex)  
{  
   // The exception is a SOAP exception, so use  
   // the Detail property's Message element.  
   Console.WriteLine(ex.Detail["Message"].InnerXml);  
}  
```  
  
```vb  
Try  
' Code for accessing the report server  
Catch ex As SoapException  
   If ex.Detail("ErrorCode").InnerXml = "rsInvalidItemName" Then  
   End If ' Perform an action based on the specific error code  
End Try  
```  
  
```csharp  
try  
{  
   // Code for accessing the report server  
}  
catch (SoapException ex)  
{  
   if (ex.Detail["ErrorCode"].InnerXml == "rsInvalidItemName")  
   {  
      // Perform an action based on the specific error code  
   }  
}  
```  
  
 下列程式碼行會將在 SOAP 例外狀況中傳回的特定錯誤碼寫入主控台。 另外，您可以評估錯誤碼並執行特定的動作。  
  
```vb  
Console.WriteLine(ex.Detail("ErrorCode").InnerXml)  
```  
  
```csharp  
Console.WriteLine(ex.Detail["ErrorCode"].InnerXml);  
```  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 中的例外狀況處理簡介](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 類別](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)   
 [SoapException 錯誤資料表](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md)  
  
  
