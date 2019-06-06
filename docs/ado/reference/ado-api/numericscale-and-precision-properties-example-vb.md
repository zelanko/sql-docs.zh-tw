---
title: NumericScale 和 Precision 屬性範例 (VB) |Microsoft Docs
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
- NumericScale property [ADO], Visual Basic example
- Precision property [ADO], Visual Basic example
ms.assetid: 9c1e2322-c225-49d1-a120-a343f23cea73
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c2251d9e51a6c483d07408e141a27657125a9187
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707229"
---
# <a name="numericscale-and-precision-properties-example-vb"></a>NumericScale 和 Precision 屬性範例 (VB)
這個範例會使用[NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)並[有效位數](../../../ado/reference/ado-api/precision-property-ado.md)要顯示的數值小數位數與有效位數中的欄位屬性***折扣***資料表***Pubs***資料庫。  
  
```  
'BeginNumericScaleVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub NumericScaleX()  
  
    ' connection and recordset variables  
   Dim rstDiscounts As ADODB.Recordset  
   Dim Cnxn As ADODB.Connection  
   Dim fldTemp As ADODB.Field  
   Dim strCnxn As String  
   Dim strSQLDiscounts As String  
  
   ' Open connection  
   Set Cnxn = New ADODB.Connection  
   strCnxn = "Provider='sqloledb';Data Source='MySqlServer';Initial Catalog='Pubs';Integrated Security='SSPI';"  
  
   Cnxn.Open strCnxn  
  
   ' Open recordset  
   Set rstDiscounts = New ADODB.Recordset  
   strSQLDiscounts = "Discounts"  
   rstDiscounts.Open strSQLDiscounts, Cnxn, adOpenStatic, adLockReadOnly, adCmdTable  
  
   ' Display numeric scale and precision of  
   ' numeric and small integer fields  
   For Each fldTemp In rstDiscounts.Fields  
      If fldTemp.Type = adNumeric Or fldTemp.Type = adSmallInt Then  
         MsgBox "Field: " & fldTemp.Name & vbCr & _  
            "Numeric scale: " & _  
               fldTemp.NumericScale & vbCr & _  
            "Precision: " & fldTemp.Precision  
      End If  
   Next fldTemp  
  
    ' clean up  
   rstDiscounts.Close  
   Cnxn.Close  
   Set rstDiscounts = Nothing  
   Set Cnxn = Nothing  
  
End Sub  
'EndNumericScaleVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)   
 [NumericScale 屬性 (ADO)](../../../ado/reference/ado-api/numericscale-property-ado.md)   
 [參數物件](../../../ado/reference/ado-api/parameter-object.md)   
 [Precision 屬性 (ADO)](../../../ado/reference/ado-api/precision-property-ado.md)
