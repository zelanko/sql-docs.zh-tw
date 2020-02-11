---
title: AddNew 方法範例（VB） |Microsoft Docs
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
- AddNew method [ADO], Visual Basic example
ms.assetid: d439e097-65f3-471d-8799-5a1263beb3c1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 043855dc4f2af915b7e1f61bffe99ae89956c3be
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67921309"
---
# <a name="addnew-method-example-vb"></a>AddNew 方法範例 (VB)
這個範例會使用[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)方法，以指定的名稱建立新的記錄。  
  
```  
'BeginAddNewVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim Cnxn As ADODB.Connection  
    Dim rstEmployees As ADODB.Recordset  
    Dim strCnxn As String  
    Dim strSQL As String  
     'record variables  
    Dim strID As String  
    Dim strFirstName As String  
    Dim strLastName As String  
    Dim blnRecordAdded As Boolean  
  
    ' Open a connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Northwind';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open Employees Table with a cursor that allows updates  
    Set rstEmployees = New ADODB.Recordset  
    strSQL = "Employees"  
    rstEmployees.Open strSQL, strCnxn, adOpenKeyset, adLockOptimistic, adCmdTable  
  
    ' Get data from the user  
    strFirstName = Trim(InputBox("Enter first name:"))  
    strLastName = Trim(InputBox("Enter last name:"))  
  
    ' Proceed only if the user actually entered something  
    ' for both the first and last names  
    If strFirstName <> "" And strLastName <> "" Then  
  
        rstEmployees.AddNew  
        rstEmployees!firstname = strFirstName  
        rstEmployees!LastName = strLastName  
        rstEmployees.Update  
        blnRecordAdded = True  
  
        ' Show the newly added data  
        MsgBox "New record: " & rstEmployees!EmployeeId & " " & _  
        rstEmployees!firstname & " " & rstEmployees!LastName  
  
    Else  
        MsgBox "Please enter a first name and last name."  
    End If  
  
    ' Delete the new record because this is a demonstration  
    Cnxn.Execute "DELETE FROM Employees WHERE EmployeeID = '" & strID & "'"  
  
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
'EndAddNewVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [AddNew 方法（ADO）](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
