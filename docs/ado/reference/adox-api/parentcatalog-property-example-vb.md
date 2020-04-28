---
title: ParentCatalog 屬性範例（VB） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ParentCatalog property [ADOX], Visual Basic example
ms.assetid: 448bc850-7584-4c5f-89f3-5f4fee88b259
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f87a092d20fb15a23e21a7ef9f0094e40eedeb57
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67965598"
---
# <a name="parentcatalog-property-example-vb"></a>ParentCatalog 屬性範例 (VB)
下列程式碼示範如何在將資料表附加至目錄之前，使用[ParentCatalog](../../../ado/reference/adox-api/parentcatalog-property-adox.md)屬性來存取提供者特定的屬性。 屬性為**自動遞增**，這會在 Microsoft Jet 資料庫中建立自動遞增欄位。  
  
```  
' BeginCreateAutoIncrColumnVB  
Sub Main()  
    On Error GoTo CreateAutoIncrColumnError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim tbl As New ADOX.Table  
  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
    Set cat.ActiveConnection = cnn  
  
    With tbl  
        .Name = "MyContacts"  
        Set .ParentCatalog = cat  
        ' Create fields and append them to the new Table object.  
        .Columns.Append "ContactId", adInteger  
        ' Make the ContactId column and auto incrementing column  
        .Columns("ContactId").Properties("AutoIncrement") = True  
        .Columns.Append "CustomerID", adVarWChar  
        .Columns.Append "FirstName", adVarWChar  
        .Columns.Append "LastName", adVarWChar  
        .Columns.Append "Phone", adVarWChar, 20  
        .Columns.Append "Notes", adLongVarWChar  
    End With  
  
    cat.Tables.Append tbl  
    Debug.Print "Table 'MyContacts' is added."  
  
    ' Delete the table as this is a demonstration.  
    cat.Tables.Delete tbl.Name  
    Debug.Print "Table 'MyContacts' is delete."  
  
    'Clean up  
    cnn.Close  
    Set cat = Nothing  
    Set tbl = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
CreateAutoIncrColumnError:  
  
    Set cat = Nothing  
    Set tbl = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
' EndCreateAutoIncrColumnVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [Append 方法（ADOX Columns）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法（ADOX Tables）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Catalog 物件（ADOX）](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Column 物件（ADOX）](../../../ado/reference/adox-api/column-object-adox.md)   
 [Columns 集合（ADOX）](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Name 屬性（ADOX）](../../../ado/reference/adox-api/name-property-adox.md)   
 [ParentCatalog 屬性（ADOX）](../../../ado/reference/adox-api/parentcatalog-property-adox.md)   
 [Table 物件（ADOX）](../../../ado/reference/adox-api/table-object-adox.md)   
 [Type 屬性 (Column) (ADOX)](../../../ado/reference/adox-api/type-property-column-adox.md)
