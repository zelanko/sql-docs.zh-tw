---
title: 在資料表之間建立新的外鍵關聯性範例（VB） |Microsoft Docs
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
- Key Type property [ADOX], Visual Basic example
- RelatedTable property [ADOX], Visual Basic example
- Keys Append method [ADOX], Visual Basic example
- UpdateRule property [ADOX], Visual Basic example
- RelatedColumn property [ADOX], Visual Basic example
ms.assetid: 13b5b1c3-6af6-439e-bb65-976578ba6bc2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6873b964adfcfc5bffed5d093bed48f4fbd29a20
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67965866"
---
# <a name="keys-append-method-key-type-relatedcolumn-relatedtable-and-updaterule-properties-example-vb"></a>Keys Append 方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例 (VB)
下列程式碼示範如何在兩個現有的資料表（名為**Customers**和**Orders**）之間建立新的外鍵關聯性。  
  
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
 [Append 方法（ADOX Columns）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法（ADOX Keys）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Catalog 物件（ADOX）](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Column 物件（ADOX）](../../../ado/reference/adox-api/column-object-adox.md)   
 [Columns 集合（ADOX）](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Key 物件（ADOX）](../../../ado/reference/adox-api/key-object-adox.md)   
 [Keys 集合（ADOX）](../../../ado/reference/adox-api/keys-collection-adox.md)   
 [Name 屬性（ADOX）](../../../ado/reference/adox-api/name-property-adox.md)   
 [RelatedColumn 屬性（ADOX）](../../../ado/reference/adox-api/relatedcolumn-property-adox.md)   
 [RelatedTable 屬性（ADOX）](../../../ado/reference/adox-api/relatedtable-property-adox.md)   
 [Table 物件（ADOX）](../../../ado/reference/adox-api/table-object-adox.md)   
 [Tables 集合（ADOX）](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [Type 屬性（Key）（ADOX）](../../../ado/reference/adox-api/type-property-key-adox.md)   
 [UpdateRule 屬性 (ADOX)](../../../ado/reference/adox-api/updaterule-property-adox.md)
