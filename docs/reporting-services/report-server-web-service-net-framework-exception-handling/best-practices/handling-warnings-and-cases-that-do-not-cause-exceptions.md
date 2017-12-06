---
title: "處理未造成例外狀況的警告與案例 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service-net-framework-exception-handling
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- exceptions [Reporting Services], warnings that don't cause
- warnings [Reporting Services]
ms.assetid: 475c0713-6265-44e7-9ebc-ebdd1b89e0af
caps.latest.revision: "30"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: bb6c8290bd942d3f031afc819aa48832948dab81
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="handling-warnings-and-cases-that-do-not-cause-exceptions"></a>處理未造成例外狀況的警告與案例
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 不會擲回警告與某些錯誤的例外狀況。 例如，當您使用 <xref:ReportService2010.ReportingService2010.CreateCatalogItem%2A> 方法來將新報表發行到報表伺服器時，會以 <xref:ReportService2010.Warning> 物件的陣列傳回發生的任何警告。 應該處理和顯示這些警告，才能採取適當的動作。  
  
```vb  
Try  
   rs.CreateCatalogItem(name, parentFolder, False, definition, Nothing, warnings)  
  
   If Not (warnings.Length = 0) Then  
      Dim warning As Warning  
      For Each warning In warnings  
         Console.WriteLine(warning.Message)  
      Next warning  
   Else  
      Console.WriteLine("Report {0} created successfully with no warnings", name)  
   End If  
  
Catch ex As SoapException  
   Console.WriteLine(ex.Detail("Message").InnerXml)  
End Try  
```  
  
```csharp  
try  
{  
   rs.CreateCatalogItem("Report", name, parentFolder, false, definition, null, out warnings);  
  
   if (warnings.Length != 0)  
   {  
      foreach (Warning warning in warnings)  
      {  
         Console.WriteLine(warning.Message);  
      }  
   }  
   else  
      Console.WriteLine("Report {0} created successfully with no warnings", name);  
}  
  
catch (SoapException ex)  
{  
   Console.WriteLine(ex.Detail["Message"].InnerXml);  
}  
```  
  
 處理錯誤的另一項方法是評估某些方法的傳回值。 例如，<xref:ReportService2010.ReportingService2010.FindItems%2A> 方法可用以搜尋報表伺服器資料庫中的特定項目。 如果找不到符合搜尋準則的項目，則會傳回 <xref:ReportService2010.CatalogItem> 物件的 Null 陣列。 您應該評估陣列、檢查 **null**，而且如果找不到項目應該讓使用者知道。  
  
## <a name="see-also"></a>另請參閱  
 <xref:ReportService2010.CatalogItem>   
 [Reporting Services 中的例外狀況處理簡介](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 類別](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
