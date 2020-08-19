---
description: PrimaryKey 和 Unique 屬性範例 (VB)
title: PrimaryKey 和 Unique 屬性範例 (VB) |Microsoft Docs
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
- Unique property [ADOX], Visual Basic example
- PrimaryKey property [ADOX], Visual Basic example
ms.assetid: f536acac-06ea-4b39-bfba-ee9902b01615
author: rothja
ms.author: jroth
ms.openlocfilehash: 1be519ab53b346eee06c45664c512677f5d8628c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439680"
---
# <a name="primarykey-and-unique-properties-example-vb"></a>PrimaryKey 和 Unique 屬性範例 (VB)
此範例示範[索引](../../../ado/reference/adox-api/index-object-adox.md)的[PrimaryKey](../../../ado/reference/adox-api/primarykey-property-adox.md)和[唯一](../../../ado/reference/adox-api/unique-property-adox.md)屬性。 程式碼會建立具有兩個數據行的新資料表。 **PrimaryKey**和**Unique**屬性是用來讓一個資料行成為不允許重複值的主鍵。  
  
```  
' BeginPrimaryKeyVB  
Sub Main()  
    On Error GoTo PrimaryKeyXError  
  
    Dim catNorthwind As New ADOX.Catalog  
    Dim tblNew As New ADOX.Table  
    Dim idxNew As New ADOX.Index  
    Dim idxLoop As New ADOX.Index  
    Dim colLoop As New ADOX.Column  
  
    ' Connect the catalog  
    catNorthwind.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Name new table  
    tblNew.Name = "NewTable"  
  
    ' Append a numeric and a text field to new table.  
    tblNew.Columns.Append "NumField", adInteger, 20  
    tblNew.Columns.Append "TextField", adVarWChar, 20  
  
    ' Append new Primary Key index on NumField column  
    ' to new table  
    idxNew.Name = "NumIndex"  
    idxNew.Columns.Append "NumField"  
    idxNew.PrimaryKey = True  
    idxNew.Unique = True  
    tblNew.Indexes.Append idxNew  
  
    ' Append an index on Textfield to new table.  
    ' Note the different technique: Specifying index and  
    ' column name as parameters of the Append method  
    tblNew.Indexes.Append "TextIndex", "TextField"  
  
    ' Append the new table  
    catNorthwind.Tables.Append tblNew  
  
    With tblNew  
        Debug.Print tblNew.Indexes.Count & " Indexes in " & _  
            tblNew.Name & " Table"  
  
        ' Enumerate Indexes collection.  
        For Each idxLoop In .Indexes  
            With idxLoop  
                Debug.Print "Index " & .Name  
                Debug.Print "   Primary key = " & .PrimaryKey  
                Debug.Print "   Unique = " & .Unique  
  
                ' Enumerate Columns collection of each Index  
                ' object.  
                Debug.Print "    Columns"  
                For Each colLoop In .Columns  
                    Debug.Print "       " & colLoop.Name  
                Next colLoop  
            End With  
        Next idxLoop  
  
    End With  
  
    ' Delete new table as this is a demonstration.  
    catNorthwind.Tables.Delete tblNew.Name  
  
    'Clean up  
    Set catNorthwind.ActiveConnection = Nothing  
    Set catNorthwind = Nothing  
    Set tblNew = Nothing  
    Set idxNew = Nothing  
    Set idxLoop = Nothing  
    Set colLoop = Nothing  
    Exit Sub  
  
PrimaryKeyXError:  
  
    Set catNorthwind = Nothing  
    Set tblNew = Nothing  
    Set idxNew = Nothing  
    Set idxLoop = Nothing  
    Set colLoop = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndPrimaryKeyVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [ (ADOX) 的索引物件 ](../../../ado/reference/adox-api/index-object-adox.md)   
 [PrimaryKey 屬性 (ADOX) ](../../../ado/reference/adox-api/primarykey-property-adox.md)   
 [Unique 屬性 (ADOX)](../../../ado/reference/adox-api/unique-property-adox.md)
