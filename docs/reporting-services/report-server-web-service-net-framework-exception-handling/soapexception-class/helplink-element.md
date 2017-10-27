---
title: "HelpLink 元素 |Microsoft 文件"
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
- HelpLink element
- SoapException class
ms.assetid: a4489103-a874-44c2-8f75-95cb238928ed
caps.latest.revision: 30
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 683da36a3015ee177935823d234968c8486eb51c
ms.contentlocale: zh-tw
ms.lasthandoff: 08/12/2017

---
# <a name="helplink-element"></a>HelpLink 元素
  **HelpLink**元素**詳細**屬性就是報表伺服器所產生的 URL 字串。 URL 會以 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 說明及支援所管理的網頁為目標，並提供有關 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中發生的特定錯誤之其他說明與知識庫文章。 URL 具有下列語法：  
  
 **http://**www.microsoft.com**/**產品**/**ee**/**transform.aspx**嗎？Server&evtsrc**= v*alue***& Mssqlserver&evtid**=*值***& ProdName**=*值***（& s) ProdVer**=*值*  
  
 下表列出的引數**HelpLink** URL。  
  
|引數|Value|  
|--------------|-----------|  
|**Server&evtsrc**|"Microsoft.ReportingServices.Diagnostics.ErrorStrings.resources.Strings"|  
|**Mssqlserver&evtid**|例如，報表伺服器錯誤碼，rsReservedItem。|  
|**ProdName**|"Microsoft SQL%20Server%20Reporting%20Services"。 產品名稱值是編碼的 URL。|  
|**ProdVer**|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 的版本號碼。 "8.00"的值表示[!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]。|  
  
 下列範例說明**HelpLink** URL 傳回的錯誤碼**rsReservedItem**。 當使用者嘗試修改或刪除在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的保留項目時，就會發生這個錯誤。  
  
```  
http://www.microsoft.com/products/ee/transform.aspx?  
EvtSrc=Microsoft.ReportingServices.Diagnostics.ErrorStrings.resources.Strings  
&EvtID=rsReservedItem&ProdName=Microsoft%20SQL%20Server%20Reporting%20Services&ProdVer=8.00  
```  
  
 您可以存取**HelpLink**程式碼中的項目**SoapException**類別。  
  
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
 [例外狀況處理中的 Reporting Services 簡介](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 類別](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)   
 [使用詳細資料屬性來處理特定的錯誤](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  

