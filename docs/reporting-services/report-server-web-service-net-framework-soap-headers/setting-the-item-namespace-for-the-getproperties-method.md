---
title: 設定 GetProperties 方法的項目命名空間 | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-soap-headers
ms.topic: reference
helpviewer_keywords:
- item properties [Reporting Services]
- ItemNamespaceHeader SOAP header
- GetProperties method
ms.assetid: b0a08639-3101-40a2-abe2-3a41753826d1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5d415d1f8b8dc25143fc704c19b3d1d0c755aa02
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "63026160"
---
# <a name="setting-the-item-namespace-for-the-getproperties-method"></a>設定 GetProperties 方法的項目命名空間
  您可以使用 <xref:ReportService2010.ItemNamespaceHeader> 中的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SOAP 標頭，根據兩個不同的項目識別碼來擷取項目屬性：項目的完整路徑或是項目的識別碼。  
  
 當您呼叫 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 方法時，通常會以引數傳遞您要擷取屬性的項目之完整路徑。 您可以透過使用 <xref:ReportService2010.ItemNamespaceHeader>，傳遞項目的識別碼做為識別碼，為方法呼叫設定 SOAP 標頭，以便使用 <xref:ReportService2010.ReportingService2010.GetProperties%2A>。  
  
 下列程式碼範例會根據項目的識別碼來擷取項目屬性值。  
  
> [!NOTE]  
>  依預設，如果您以項目識別碼傳遞完整路徑名稱給 <xref:ReportService2010.ItemNamespaceHeader> 方法，則不需要為 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 設定值。  
  
```vb  
Imports System  
Imports System.Collections  
  
Class Sample  
   Sub Main()  
      Dim rs As New ReportingService2010()  
      rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
      rs.Url = "https://<Server Name>/reportserver/ReportService2010.asmx"  
  
      Dim items() As CatalogItem  
  
      Try  
         ' Need the ID property of items. Normally, you would already have   
         ' this stored somewhere.  
         items = rs.ListChildren("/AdventureWorks Sample Reports", False)  
  
         ' Set the item namespace header to be GUID-based  
         rs.ItemNamespaceHeaderValue = New ItemNamespaceHeader()  
         rs.ItemNamespaceHeaderValue.ItemNamespace = ItemNamespaceEnum.GUIDBased  
  
         ' Call GetProperties with item ID.  
         If Not (items Is Nothing) Then  
            Dim item As CatalogItem  
            For Each item In  items  
               Dim properties As [Property]() = rs.GetProperties(item.ID, Nothing)  
               Dim property As [Property]  
               For Each property In  properties  
                  Console.WriteLine(([property].Name + ": " + [property].Value))  
               Next property  
               Console.WriteLine()  
            Next item  
         End If  
  
      Catch e As Exception  
         Console.WriteLine((e.Message + ": " + e.StackTrace))  
      End Try  
   End Sub 'Main  
End Class 'Sample  
```  
  
```csharp  
using System;  
using System.Collections;  
  
class Sample  
{  
   static void Main()  
   {  
   ReportingService2010 rs = new ReportingService2010();  
      rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
      rs.Url = "https://<Server Name>/reportserver/ReportService2010.asmx";  
  
      CatalogItem[] items;  
  
      try  
      {  
         // Need the ID property of items. Normally, you would already have   
         // this stored somewhere.  
         items = rs.ListChildren("/AdventureWorks Sample Reports", false);  
  
         // Set the item namespace header to be GUID-based  
         rs.ItemNamespaceHeaderValue = new ItemNamespaceHeader();  
         rs.ItemNamespaceHeaderValue.ItemNamespace = ItemNamespaceEnum.GUIDBased;  
  
         // Call GetProperties with item ID.  
         if (items != null)  
         {  
            foreach( CatalogItem item in items)  
            {  
               Property[] properties = rs.GetProperties(item.ID, null);  
               foreach (Property property in properties)  
               {  
                  Console.WriteLine(property.Name + ": " + property.Value);  
               }  
               Console.WriteLine();  
            }  
         }  
      }  
  
      catch (Exception e)  
      {  
         Console.WriteLine(e.Message);  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [技術參考 &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)   
 [使用 Reporting Services SOAP 標頭](../../reporting-services/report-server-web-service-net-framework-soap-headers/using-reporting-services-soap-headers.md)  
  
  
