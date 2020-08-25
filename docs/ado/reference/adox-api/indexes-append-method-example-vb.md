---
description: Indexes Append 方法範例 (VB)
title: " (VB) 的索引附加方法範例 |Microsoft Docs"
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
- Append method [ADOX]
ms.assetid: 50f87e27-1bf9-427c-9b1d-704a672434d2
author: rothja
ms.author: jroth
ms.openlocfilehash: 8a08cabb34fed31ffd8b843fcbb9f76a29b6016b
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770277"
---
# <a name="indexes-append-method-example-vb"></a>Indexes Append 方法範例 (VB)
下列程式碼示範如何建立新的索引。 索引位於資料表中的兩個數據行上。  
  
```  
Attribute VB_Name = "IndexesAppend"  
Option Explicit  
  
' BeginCreateIndexVB  
Sub Main()  
    On Error GoTo CreateIndexError  
  
    Dim tbl As New Table  
    Dim idx As New ADOX.Index  
    Dim cat As New ADOX.Catalog  
  
    'Open the catalog.  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Define the table and append it to the catalog.  
    tbl.Name = "MyTable"  
    tbl.Columns.Append "Column1", adInteger  
    tbl.Columns.Append "Column2", adInteger  
    tbl.Columns.Append "Column3", adVarWChar, 50  
    cat.Tables.Append tbl  
    Debug.Print "Table 'MyTable' is added."  
  
    ' Define a multi-column index.  
    idx.Name = "multicolidx"  
    idx.Columns.Append "Column1"  
    idx.Columns.Append "Column2"  
  
    ' Append the index to the table.  
    tbl.Indexes.Append idx  
    Debug.Print "The index is appended to table 'MyTable'."  
  
    'Delete the table as this is a demonstration.  
    cat.Tables.Delete tbl.Name  
    Debug.Print "Table 'MyTable' is deleted."  
  
    'Clean up.  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set tbl = Nothing  
    Set idx = Nothing  
    Exit Sub  
  
CreateIndexError:  
    Set cat = Nothing  
    Set tbl = Nothing  
    Set idx = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndCreateIndexVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [附加方法 (ADOX 索引) ](./append-method-adox-indexes.md)   
 [ (ADOX) 的索引物件 ](./index-object-adox.md)   
 [Indexes 集合 (ADOX)](./indexes-collection-adox.md)