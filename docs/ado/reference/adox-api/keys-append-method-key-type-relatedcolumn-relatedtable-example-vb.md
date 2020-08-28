---
description: Keys Append 方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例 (VB)
title: 在資料表之間建立新的外鍵關聯性範例 (VB) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Key Type property [ADOX], Visual Basic example
- RelatedTable property [ADOX], Visual Basic example
- Keys Append method [ADOX], Visual Basic example
- UpdateRule property [ADOX], Visual Basic example
- RelatedColumn property [ADOX], Visual Basic example
ms.assetid: 13b5b1c3-6af6-439e-bb65-976578ba6bc2
author: rothja
ms.author: jroth
ms.openlocfilehash: edc38c1506e472eddb6640c9d7ca121154dcc4cb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984059"
---
# <a name="keys-append-method-key-type-relatedcolumn-relatedtable-and-updaterule-properties-example-vb"></a>Keys Append 方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例 (VB)
下列程式碼示範如何建立兩個現有資料表（名為 **Customers** 和 **Orders**）之間的新外鍵關聯性。  
  
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
 [將方法附加至 ADOX 資料行 () ](./append-method-adox-columns.md)   
 [附加方法 (ADOX 索引鍵) ](./append-method-adox-keys.md)   
 [ (ADOX) 的目錄物件 ](./catalog-object-adox.md)   
 [資料行物件 (ADOX) ](./column-object-adox.md)   
 [資料行集合 (ADOX) ](./columns-collection-adox.md)   
 [ (ADOX) 的索引鍵物件 ](./key-object-adox.md)   
 [ (ADOX) 的索引鍵集合 ](./keys-collection-adox.md)   
 [名稱屬性 (ADOX) ](./name-property-adox.md)   
 [RelatedColumn 屬性 (ADOX) ](./relatedcolumn-property-adox.md)   
 [RelatedTable 屬性 (ADOX) ](./relatedtable-property-adox.md)   
 [資料表物件 (ADOX) ](./table-object-adox.md)   
 [資料表集合 (ADOX) ](./tables-collection-adox.md)   
 [類型屬性 (索引鍵)  (ADOX) ](./type-property-key-adox.md)   
 [UpdateRule 屬性 (ADOX)](./updaterule-property-adox.md)