---
title: HelpLink 項目 | Microsoft Docs
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
- HelpLink element
- SoapException class
ms.assetid: a4489103-a874-44c2-8f75-95cb238928ed
caps.latest.revision: 30
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: aec03e032cdd0af46666ca76f49bb2034c5312d8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030954"
---
# <a name="helplink-element"></a>HelpLink 元素
  **Detail** 屬性的 **HelpLink** 項目是報表伺服器所產生的 URL 字串。 URL 會以 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 說明及支援所管理的網頁為目標，並提供有關 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中發生的特定錯誤之其他說明與知識庫文章。 URL 具有下列語法：  
  
 **http://** www.microsoft.com**/** products**/** ee**/** transform.aspx **?EvtSrc**=v*alue***&EvtID**=* value ***&ProdName**=* value***&ProdVer**=* value*  
  
 下表列出 **HelpLink** URL 的引數。  
  
|引數|ReplTest1|  
|--------------|-----------|  
|**EvtSrc**|"Microsoft.ReportingServices.Diagnostics.ErrorStrings.resources.Strings"|  
|**EvtID**|例如，報表伺服器錯誤碼，rsReservedItem。|  
|**ProdName**|"Microsoft SQL%20Server%20Reporting%20Services"。 產品名稱值是編碼的 URL。|  
|**ProdVer**|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 的版本號碼。 "8.00" 的值表示 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]。|  
  
 下列範例說明**HelpLink** URL 傳回的錯誤碼`rsReservedItem`。 當使用者嘗試修改或刪除在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的保留項目時，就會發生這個錯誤。  
  
```  
http://www.microsoft.com/products/ee/transform.aspx?  
EvtSrc=Microsoft.ReportingServices.Diagnostics.ErrorStrings.resources.Strings  
&EvtID=rsReservedItem&ProdName=Microsoft%20SQL%20Server%20Reporting%20Services&ProdVer=8.00  
```  
  
 您可以使用 **SoapException** 類別來存取程式碼中的 **HelpLink** 項目。  
  
```vb  
Try  
   rs.DeleteItem("/Report1")  
  
Catch e As SoapException  
   Console.WriteLine(e.Detail("HelpLink").InnerXml)  
End Try  
```  
  
```csharp  
try  
{  
   rs.DeleteItem("/Report1");  
}  
  
catch (SoapException e)  
{  
   Console.WriteLine(e.Detail["HelpLink"].InnerXml);  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 中的例外狀況處理簡介](../introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 類別](reporting-services-soapexception-class.md)   
 [使用 Detail 屬性來處理特定的錯誤](../best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  