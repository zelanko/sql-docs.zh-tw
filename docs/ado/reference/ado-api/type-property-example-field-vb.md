---
title: 輸入屬性的範例 （欄位） (VB) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Type property [field] [ADO], Visual Basic example
ms.assetid: accb72f5-a3bd-4a7e-92b6-6da0783b4b75
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c6f897f6db8f361d865d356a92d21eb217114eb6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="type-property-example-field-vb"></a>型別屬性範例 （欄位） (VB)
這個範例會示範[類型](../../../ado/reference/ado-api/type-property-ado.md)屬性所顯示的值之常數的對應名稱[類型](../../../ado/reference/ado-api/type-property-ado.md)屬性的所有[欄位](../../../ado/reference/ado-api/field-object.md)中的物件***員工***資料表。 FieldType 函式，才能執行這個程序。  
  
```  
'BeginTypeFieldVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
    Dim Cnxn As ADODB.Connection  
    Dim rstEmployees As ADODB.Recordset  
    Dim fld As ADODB.Field  
    Dim strCnxn As String  
    Dim strSQLEmployee As String  
    Dim FieldType As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open recordset with data from Employees table  
    Set rstEmployees = New ADODB.Recordset  
    strSQLEmployee = "employee"  
    rstEmployees.Open strSQLEmployee, Cnxn, , , adCmdTable  
    'rstEmployees.Open strSQLEmployee, Cnxn, adOpenStatic, adLockReadOnly, adCmdTable  
     ' the above two lines of code are identical  
  
    Debug.Print "Fields in Employees Table:" & vbCr  
  
    ' Enumerate Fields collection of Employees table  
    For Each fld In rstEmployees.Fields  
        ' translate field-type code to text  
        Select Case fld.Type  
            Case adChar  
               FieldType = "adChar"  
            Case adVarChar  
               FieldType = "adVarChar"  
            Case adSmallInt  
               FieldType = "adSmallInt"  
            Case adUnsignedTinyInt  
               FieldType = "adUnsignedTinyInt"  
            Case adDBTimeStamp  
               FieldType = "adDBTimeStamp"  
        End Select  
        ' show results  
        Debug.Print "  Name: " & fld.Name & vbCr & _  
          "  Type: " & FieldType & vbCr  
    Next fld  
  
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
  
    Set fld = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndTypeFieldVB  
  
Attribute VB_Name = "TypeField"  
```  
  
## <a name="see-also"></a>另請參閱  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)   
 [Type 屬性 (ADO)](../../../ado/reference/ado-api/type-property-ado.md)
