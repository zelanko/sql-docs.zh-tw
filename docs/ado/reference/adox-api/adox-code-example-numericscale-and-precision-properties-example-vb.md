---
description: ADOX 程式碼範例：NumericScale 和 Precision 屬性範例 (VB)
title: NumericScale 和 Precision 屬性 ADOX 程式碼範例 (VB) |Microsoft Docs
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
- Precision property [ADOX], Visual Basic example
- NumericScale property [ADOX], Visual Basic example
ms.assetid: ea2ec614-34c8-41b7-8ebd-063798bd56b4
author: rothja
ms.author: jroth
ms.openlocfilehash: 919ad2763a711382cc9f472f34c791807cdd29e2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440641"
---
# <a name="adox-code-example-numericscale-and-precision-properties-example-vb"></a>ADOX 程式碼範例：NumericScale 和 Precision 屬性範例 (VB)
此範例示範資料[行](../../../ado/reference/adox-api/column-object-adox.md)物件的[NumericScale](../../../ado/reference/adox-api/numericscale-property-adox.md)和[Precision](../../../ado/reference/adox-api/precision-property-adox.md)屬性。 此程式碼會顯示*Northwind*資料庫之 [**訂單詳細資料**] 資料表的值。  
  
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
 [資料行物件 (ADOX) ](../../../ado/reference/adox-api/column-object-adox.md)   
 [NumericScale 屬性 (ADOX) ](../../../ado/reference/adox-api/numericscale-property-adox.md)   
 [Precision 屬性 (ADOX)](../../../ado/reference/adox-api/precision-property-adox.md)
