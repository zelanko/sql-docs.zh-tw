---
title: "NumericScale 和有效位數屬性範例 (VB) |Microsoft 文件"
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
- Precision property [ADOX], Visual Basic example
- NumericScale property [ADOX], Visual Basic example
ms.assetid: ea2ec614-34c8-41b7-8ebd-063798bd56b4
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 41bacabc5cfcaff1ef48e03e5db00f3acd58da7a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="adox-code-example-numericscale-and-precision-properties-example-vb"></a>ADOX 程式碼範例： NumericScale 和有效位數屬性範例 (VB)
這個範例會示範[NumericScale](../../../ado/reference/adox-api/numericscale-property-adox.md)和[精確度](../../../ado/reference/adox-api/precision-property-adox.md)屬性[資料行](../../../ado/reference/adox-api/column-object-adox.md)物件。 此程式碼會顯示其值**Order Details**資料表*Northwind*資料庫。  
  
```  
' BeginNumericScalePrecVB  
Sub Main()  
    On Error GoTo NumericScalePrecXError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim tblOD As ADOX.Table  
    Dim colLoop As ADOX.Column  
  
    ' Connect the catalog.  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "data source='Northwind.mdb';"  
    Set cat.ActiveConnection = cnn  
  
    ' Retrieve the Order Details table  
    Set tblOD = cat.Tables("Order Details")  
  
    ' Display numeric scale and precision of  
    ' small integer fields.  
    For Each colLoop In tblOD.Columns  
        If colLoop.Type = adSmallInt Then  
            MsgBox "Column: " & colLoop.Name & vbCr & _  
                "Numeric scale: " & _  
                colLoop.NumericScale & vbCr & _  
                "Precision: " & colLoop.Precision  
        End If  
    Next colLoop  
  
    'Clean up  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
NumericScalePrecXError:  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndNumericScalePrecVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料行物件 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)   
 [NumericScale 屬性 (ADOX)](../../../ado/reference/adox-api/numericscale-property-adox.md)   
 [有效位數屬性 (ADOX)](../../../ado/reference/adox-api/precision-property-adox.md)

