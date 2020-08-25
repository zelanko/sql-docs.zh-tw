---
description: 'AbsolutePage、PageCount 和 PageSize 屬性範例 (VB) '
title: AbsolutePage、PageCount 和 PageSize 屬性範例 (VB) |Microsoft Docs
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
- PageCount property [ADO], Visual Basic example
- AbsolutePage property [ADO], Visual Basic example
- PageSize property [ADO], Visual Basic example
ms.assetid: 5aaada64-5115-4adc-8668-827348f32566
author: rothja
ms.author: jroth
ms.openlocfilehash: 8adbe7524bbf7886744b9753eb8dfb5417a1898a
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88760008"
---
# <a name="absolutepage-pagecount-and-pagesize-properties-example-vb"></a>AbsolutePage、PageCount 和 PageSize 屬性範例 (VB) 
```  
'BeginAbsolutePageVB  
  
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
    Dim intPage As Integer  
    Dim intPageCount As Integer  
    Dim intRecord As Integer  
  
    'Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open employee recordset  
    ' Use client cursor to enable AbsolutePosition property  
    Set rstEmployees = New ADODB.Recordset  
    strSQL = "employee"  
    rstEmployees.Open strSQL, strCnxn, adUseClient, adLockReadOnly, adCmdTable  
  
    ' Display names and hire dates, five records at a time  
    rstEmployees.PageSize = 5  
    intPageCount = rstEmployees.PageCount  
    For intPage = 1 To intPageCount  
        rstEmployees.AbsolutePage = intPage  
        strMessage = ""  
        For intRecord = 1 To rstEmployees.PageSize  
            strMessage = strMessage & _  
                rstEmployees!fname & " " & _  
                rstEmployees!lname & " " & _  
                rstEmployees!hire_date & vbCr  
            rstEmployees.MoveNext  
            If rstEmployees.EOF Then Exit For  
        Next intRecord  
        MsgBox strMessage  
    Next intPage  
  
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
'EndAbsolutePageVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的 AbsolutePage 屬性 ](./absolutepage-property-ado.md)   
 [ (ADO) 的 PageCount 屬性 ](./pagecount-property-ado.md)   
 [ (ADO) 的 PageSize 屬性 ](./pagesize-property-ado.md)   
 [Recordset 物件 (ADO)](./recordset-object-ado.md)