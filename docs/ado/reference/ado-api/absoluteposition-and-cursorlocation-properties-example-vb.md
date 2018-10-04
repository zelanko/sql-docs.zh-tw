---
title: AbsolutePosition 和 CursorLocation 屬性範例 (VB) |Microsoft Docs
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
- AbsolutePosition property [ADO], Visual Basic example
- CursorLocation property [ADO], Visual Basic example
ms.assetid: c4755799-c60a-4b5e-a01f-b85dd0e0a7f9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a22afb8e59d692ae4fae010adc819cd930b8ab46
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47770838"
---
# <a name="absoluteposition-and-cursorlocation-properties-example-vb"></a>AbsolutePosition 和 CursorLocation 屬性範例 (VB)
此範例示範如何[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)屬性可以追蹤列舉的所有記錄迴圈的進度[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。 它會使用[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性，來啟用**AbsolutePosition**藉由設定資料指標，用戶端資料指標的屬性。  
  
```  
'BeginAbsolutePositionVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim rstEmployees As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQL As String  
        'record variables  
    Dim strMessage As String  
  
    'Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open Employee recordset with  
    ' Client-side cursor to enable AbsolutePosition property  
    Set rstEmployees = New ADODB.Recordset  
    strSQL = "employee"  
    rstEmployees.Open strSQL, strCnxn, adUseClient, adLockReadOnly, adCmdTable  
  
    ' Enumerate Recordset  
    Do While Not rstEmployees.EOF  
        ' Display current record information  
        strMessage = "Employee: " & rstEmployees!lname & vbCr & _  
            "(record " & rstEmployees.AbsolutePosition & _  
            " of " & rstEmployees.RecordCount & ")"  
        If MsgBox(strMessage, vbOKCancel) = vbCancel Then Exit Do  
        rstEmployees.MoveNext  
    Loop  
  
    ' clean up  
    rstEmployees.Close  
    Cnxn.Close  
    Set rstEmployees = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
   ' clean up  
    If Not rstEmployees Is Nothing Then  
        If rstEmployees.State = adStateOpen Then rstEmployees.Close  
    End If  
    Set rstEmployees = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndAbsolutePositionVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [AbsolutePosition 屬性 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [CursorLocation 屬性 (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
