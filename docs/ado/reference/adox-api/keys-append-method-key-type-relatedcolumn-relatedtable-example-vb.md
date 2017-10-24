---
title: "建立新外部索引鍵之間的關聯性的資料表範例 (VB) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Key Type property [ADOX], Visual Basic example
- RelatedTable property [ADOX], Visual Basic example
- Keys Append method [ADOX], Visual Basic example
- UpdateRule property [ADOX], Visual Basic example
- RelatedColumn property [ADOX], Visual Basic example
ms.assetid: 13b5b1c3-6af6-439e-bb65-976578ba6bc2
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: baf04a542b1f488e8570713df938f3a03aa753f1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="keys-append-method-key-type-relatedcolumn-relatedtable-and-updaterule-properties-example-vb"></a>索引鍵附加方法、 金鑰類型、 RelatedColumn、 RelatedTable 和 UpdateRule 屬性範例 (VB)
下列程式碼示範如何建立兩個現有的資料表，名為新的外部索引鍵關係**客戶**和**訂單**。  
  
```  
' BeginCreateKeyVB  
Sub Main()  
    On Error GoTo CreateKeyError  
  
    Dim kyForeign As New ADOX.Key  
    Dim cat As New ADOX.Catalog  
  
    ' Connect to the catalog.  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Define the foreign key.  
    kyForeign.Name = "CustOrder"  
    kyForeign.Type = adKeyForeign  
    kyForeign.RelatedTable = "Customers"  
    kyForeign.Columns.Append "CustomerId"  
    kyForeign.Columns("CustomerId").RelatedColumn = "CustomerId"  
    kyForeign.UpdateRule = adRICascade  
  
    ' Append the foreign key to the keys collection.  
    cat.Tables("Orders").Keys.Append kyForeign  
  
    'Delete the key t demonstrate the Delete method.  
    cat.Tables("Orders").Keys.Delete kyForeign.Name  
  
    'Clean up.  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set kyForeign = Nothing  
    Exit Sub  
  
CreateKeyError:  
    Set cat = Nothing  
    Set kyForeign = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
' EndCreateKeyVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [Append 方法 （ADOX 資料行）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 （ADOX 索引鍵）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [目錄物件 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [資料行物件 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)   
 [資料行集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [索引鍵的物件 (ADOX)](../../../ado/reference/adox-api/key-object-adox.md)   
 [索引鍵集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)   
 [Name 屬性 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)   
 [RelatedColumn 屬性 (ADOX)](../../../ado/reference/adox-api/relatedcolumn-property-adox.md)   
 [RelatedTable 屬性 (ADOX)](../../../ado/reference/adox-api/relatedtable-property-adox.md)   
 [Table 物件 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)   
 [資料表集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [型別屬性 (Key) (ADOX)](../../../ado/reference/adox-api/type-property-key-adox.md)   
 [UpdateRule 屬性 (ADOX)](../../../ado/reference/adox-api/updaterule-property-adox.md)

