---
title: NextRecordset 方法範例（VB） |Microsoft Docs
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
- NextRecordset method [ADO], Visual Basic example
ms.assetid: b14806da-80d9-4da4-bb87-f558b36a6ac0
author: rothja
ms.author: jroth
ms.openlocfilehash: 78480bd71a1d96f5c5447022e3c7748814003bea
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762379"
---
# <a name="nextrecordset-method-example-vb"></a>NextRecordset 方法範例 (VB)
這個範例會使用[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)方法來查看記錄集中的資料，其中使用由三個不同**SELECT**語句所組成的複合命令語句。  
  
```  
'BeginNextRecordsetVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    ' connection and recordset variables  
    Dim rstCompound As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim SQLCompound As String  
  
    Dim intCount As Integer  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open compound recordset  
    Set rstCompound = New ADODB.Recordset  
    SQLCompound = "SELECT * FROM Authors; " & _  
        "SELECT * FROM stores; " & _  
        "SELECT * FROM jobs"  
    rstCompound.Open SQLCompound, Cnxn, adOpenStatic, adLockReadOnly, adCmdText  
  
    ' Display results from each SELECT statement  
    intCount = 1  
    Do Until rstCompound Is Nothing  
        Debug.Print "Contents of recordset #" & intCount  
  
        Do Until rstCompound.EOF  
            Debug.Print , rstCompound.Fields(0), rstCompound.Fields(1)  
            rstCompound.MoveNext  
        Loop  
  
        Set rstCompound = rstCompound.NextRecordset  
        intCount = intCount + 1  
    Loop  
  
    ' clean up  
    Cnxn.Close  
    Set rstCompound = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstCompound Is Nothing Then  
        If rstCompound.State = adStateOpen Then rstCompound.Close  
    End If  
    Set rstCompound = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndNextRecordsetVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [NextRecordset 方法（ADO）](../../../ado/reference/ado-api/nextrecordset-method-ado.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
