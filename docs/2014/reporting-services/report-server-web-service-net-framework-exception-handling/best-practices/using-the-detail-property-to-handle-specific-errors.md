---
title: 使用 Detail 屬性處理特定的錯誤 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- exceptions [Reporting Services], Detail property
- Detail property
- InnerText property
ms.assetid: 4392633d-b46b-41e6-bc12-efb64e166704
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f45118f75161fc8877edad53bce9abef4f5e00a8
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "60158404"
---
# <a name="using-the-detail-property-to-handle-specific-errors"></a>使用詳細資料屬性來處理特定的錯誤
  若要進一步分類例外狀況，[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 會在 SOAP 例外狀況的 **Detail** 屬性中，於子項目的 **InnerText** 屬性中傳回其他錯誤資訊。 因為 **Detail** 屬性是一種 **XmlNode** 物件，所以您可以使用下列程式碼來存取 **Message** 子項目的內部文字。  
  
 如需包含在 **Detail** 屬性中所有可用的子項目清單，請參閱 [Detail 屬性](../soapexception-class/detail-property.md)。 如需詳細資訊，請參閱 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK 文件中的＜Detail 屬性＞。  
  
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
 [Reporting Services 中的例外狀況處理簡介](../introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 類別](../soapexception-class/reporting-services-soapexception-class.md)   
 [SoapException 錯誤資料表](../soapexception-class/soapexception-errors-table.md)  
  
  
