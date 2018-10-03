---
title: 資料行和資料表 Append 方法、 Name 屬性範例 (VB) |Microsoft Docs
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
- Name property [ADOX], Visual Basic example
- Append method [ADOX], Visual Basic example
ms.assetid: 678e5546-df5d-4cd0-bfe9-6cf13cb385c0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2bdd2643fdeb0f317e47c4d54b8b1ca62dec4109
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47681519"
---
# <a name="columns-and-tables-append-methods-name-property-example-vb"></a>Columns 和 Tables Append 方法、Name 屬性範例 (VB)
下列程式碼示範如何建立新的資料表。  
  
```  
' BeginCreateTableVB  
Sub Main()  
    On Error GoTo CreateTableError  
  
    Dim tbl As New Table  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Catalog.  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    tbl.Name = "MyTable"  
    tbl.Columns.Append "Column1", adInteger  
    tbl.Columns.Append "Column2", adInteger  
    tbl.Columns.Append "Column3", adVarWChar, 50  
    cat.Tables.Append tbl  
    Debug.Print "Table 'MyTable' is added."  
  
    'Delete the table as this is a demonstration.  
    cat.Tables.Delete tbl.Name  
    Debug.Print "Table 'MyTable' is deleted."  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set tbl = Nothing  
    Exit Sub  
  
CreateTableError:  
  
    Set cat = Nothing  
    Set tbl = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndCreateTableVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [Append 方法 (ADOX Columns)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 (ADOX Tables)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [資料行物件 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)   
 [資料行集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Name 屬性 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)   
 [Table 物件 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)   
 [Tables 集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)
