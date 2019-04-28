---
title: ParentCatalog 屬性範例 (VB) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: a98d750a42692c10a083a1a953e81f274fca7dd1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62710396"
---
# <a name="parentcatalog-property-example-vb"></a>ParentCatalog 屬性範例 (VB)
下列程式碼示範如何使用[ParentCatalog](../../../ado/reference/adox-api/parentcatalog-property-adox.md)屬性來存取提供者特有的屬性，再附加到類別目錄的資料表。 屬性是**AutoIncrement**，Microsoft Jet 資料庫中建立自動遞增欄位。  
  
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
 [Append 方法 (ADOX Columns)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 (ADOX Tables)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Catalog 物件 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [資料行物件 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)   
 [資料行集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Name 屬性 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)   
 [ParentCatalog 屬性 (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md)   
 [Table 物件 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)   
 [Type 屬性 (Column) (ADOX)](../../../ado/reference/adox-api/type-property-column-adox.md)
