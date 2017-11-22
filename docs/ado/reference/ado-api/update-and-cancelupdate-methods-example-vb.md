---
title: "更新和 CancelUpdate 方法範例 (VB) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: VB
helpviewer_keywords:
- CancelUpdate method [ADO]
- Update method [ADO], Visual Basic example
ms.assetid: 55bedd08-7440-4da4-b854-4ac9ef2fdedb
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7233b7b8832ff0f8b479b2e57e1a1387ec6de581
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="update-and-cancelupdate-methods-example-vb"></a>更新和 CancelUpdate 方法範例 (VB)
這個範例會示範[更新](../../../ado/reference/ado-api/update-method.md)方法搭配[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法。  
  
```  
'BeginUpdateVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
    ' recordset and connection variables  
    Dim rstEmployees As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQLEmployees As String  
     ' buffer variables  
    Dim strOldFirst As String  
    Dim strOldLast As String  
    Dim strMessage As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open recordset to enable changes  
    Set rstEmployees = New ADODB.Recordset  
    strSQLEmployees = "SELECT fname, lname FROM Employee ORDER BY lname"  
    rstEmployees.Open strSQLEmployees, Cnxn, adOpenKeyset, adLockOptimistic, adCmdText  
  
    ' Store original data  
    strOldFirst = rstEmployees!fname  
    strOldLast = rstEmployees!lname  
    ' Change data in edit buffer  
    rstEmployees!fname = "Linda"  
    rstEmployees!lname = "Kobara"  
  
    ' Show contents of buffer and get user input  
    strMessage = "Edit in progress:" & vbCr & _  
        "  Original data = " & strOldFirst & " " & _  
        strOldLast & vbCr & "  Data in buffer = " & _  
        rstEmployees!fname & " " & rstEmployees!lname & vbCr & vbCr & _  
        "Use Update to replace the original data with " & _  
        "the buffered data in the Recordset?"  
  
    If MsgBox(strMessage, vbYesNo) = vbYes Then  
        rstEmployees.Update  
    Else  
        rstEmployees.CancelUpdate  
    End If  
  
    ' show the resulting data  
    MsgBox "Data in recordset = " & rstEmployees!fname & " " & _  
       rstEmployees!lname  
  
    ' restore original data because this is a demonstration  
    If Not (strOldFirst = rstEmployees!fname And _  
           strOldLast = rstEmployees!lname) Then  
        rstEmployees!fname = strOldFirst  
        rstEmployees!lname = strOldLast  
        rstEmployees.Update  
    End If  
  
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
' EndUpdateVB  
```  
  
 這個範例會示範**更新**方法搭配[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)方法。  
  
```  
Attribute VB_Name = "Update"  
```  
  
## <a name="see-also"></a>請參閱＜  
 [CancelUpdate 方法 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)
