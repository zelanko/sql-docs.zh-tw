---
description: GetString 方法範例 (VB)
title: " (VB) 的 GetString 方法範例 |Microsoft Docs"
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
- GetString method [ADO], Visual Basic example
ms.assetid: 14c96d71-46a8-4782-b474-80ce348e8bff
author: rothja
ms.author: jroth
ms.openlocfilehash: 8d5baaab530a1d693a5f31f998e6aa6893b6cdfa
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774897"
---
# <a name="getstring-method-example-vb"></a>GetString 方法範例 (VB)
此範例示範 [GetString](./getstring-method-ado.md) 方法。  
  
 假設您正在偵測資料存取問題，並想要快速且簡單的方式來列印小型 [記錄集](./recordset-object-ado.md)的目前內容。  
  
```  
'BeginGetStringVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
     ' connection variables  
    Dim Cnxn As ADODB.Connection  
    Dim rstAuthors As ADODB.Recordset  
    Dim strCnxn As String  
    Dim strSQLAuthors As String  
    Dim varOutput As Variant  
  
     ' specific variables  
    Dim strPrompt As String  
    Dim strState As String  
  
     ' open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
     ' get user input  
    strPrompt = "Enter a state (CA, IN, KS, MD, MI, OR, TN, UT): "  
    strState = Trim(InputBox(strPrompt, "GetString Example"))  
  
     ' open recordset  
    Set rstAuthors = New ADODB.Recordset  
    strSQLAuthors = "SELECT au_fname, au_lname, address, city FROM Authors " & _  
                "WHERE state = '" & strState & "'"  
    rstAuthors.Open strSQLAuthors, Cnxn, adOpenStatic, adLockReadOnly, adCmdText  
  
    If Not rstAuthors.EOF Then  
    ' Use all defaults: get all rows, TAB as column delimiter,  
    ' CARRIAGE RETURN as row delimiter, EMPTY-string as null delimiter  
       varOutput = rstAuthors.GetString(adClipString)  
        ' print output  
       Debug.Print "State = '" & strState & "'"  
       Debug.Print "Name             Address             City" & vbCr  
       Debug.Print varOutput  
    Else  
       Debug.Print "No rows found for state = '" & strState & "'" & vbCr  
    End If  
  
    ' clean up  
    rstAuthors.Close  
    Cnxn.Close  
    Set rstAuthors = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstAuthors Is Nothing Then  
        If rstAuthors.State = adStateOpen Then rstAuthors.Close  
    End If  
    Set rstAuthors = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndGetStringVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的 GetString 方法 ](./getstring-method-ado.md)   
 [Recordset 物件 (ADO)](./recordset-object-ado.md)