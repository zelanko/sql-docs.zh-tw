---
description: GetRows 方法範例 (VB)
title: " (VB) 的 GetRows 方法範例 |Microsoft Docs"
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
- Getrows method [ADO], Visual Basic example
ms.assetid: 9f7c78bb-7bb8-4c4f-8e5a-4d3bfc8a208f
author: rothja
ms.author: jroth
ms.openlocfilehash: a4f57460813cc72e4d513b9954739bcc02a5e4b8
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775017"
---
# <a name="getrows-method-example-vb"></a>GetRows 方法範例 (VB)
這個範例會使用 [GetRows](./getrows-method-ado.md) 方法，從 [記錄集](./recordset-object-ado.md) 取出指定的資料列數目，並將產生的資料填入陣列。 在兩種情況下， **getrows** 方法會傳回小於所需的資料列數目：若已達到 [EOF](./bof-eof-properties-ado.md) ，或如果 **GetRows** 嘗試抓取其他使用者刪除的記錄，則為。 只有在第二個案例發生時，函式才會傳回 **False** 。 此程式必須有 GetRowsOK 函數才能執行。  
  
```  
'BeginGetRowsVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
     ' connection and recordset variables  
    Dim rstEmployees As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strSQLEmployees As String  
    Dim strCnxn As String  
    ' array variable  
    Dim arrEmployees As Variant  
    ' detail variables  
    Dim strMessage As String  
    Dim intRows As Integer  
    Dim intRecord As Integer  
  
    ' open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' open recordset client-side to enable RecordCount  
    Set rstEmployees = New ADODB.Recordset  
    strSQLEmployees = "SELECT fName, lName, hire_date FROM Employee ORDER BY lName"  
    rstEmployees.Open strSQLEmployees, Cnxn, adOpenStatic, adLockReadOnly, adCmdText  
  
    ' get user input for number of rows  
    Do  
        strMessage = "Enter number of rows to retrieve:"  
        intRows = Val(InputBox(strMessage))  
  
          ' if bad user input exit the loop  
        If intRows <= 0 Then  
            MsgBox "Please enter a positive number", vbOKOnly, "Not less than zero!"  
        ' if number of requested records is over the total  
        ElseIf intRows > rstEmployees.RecordCount Then  
            MsgBox "Not enough records in Recordset to retrieve " & intRows & " rows.", _  
            vbOKOnly, "Over the available total"  
        Else  
            Exit Do  
        End If  
    Loop  
  
      ' else put the data in an array and print  
    arrEmployees = rstEmployees.GetRows(intRows)  
  
    Dim x As Integer, y As Integer  
  
    For x = 0 To intRows - 1  
        For y = 0 To 2  
            Debug.Print arrEmployees(y, x) & " ";  
        Next y  
        Debug.Print vbCrLf  
    Next x  
  
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
'EndGetRowsVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的 GetRows 方法 ](./getrows-method-ado.md)   
 [Recordset 物件 (ADO)](./recordset-object-ado.md)