---
description: State 屬性範例 (VB)
title: State 屬性範例 (VB) |Microsoft Docs
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
- State property [ADO], Visual Basic example
ms.assetid: 9da6db50-d9bb-47e1-ae8b-be3c9b88cf9a
author: rothja
ms.author: jroth
ms.openlocfilehash: 1927de05ec73d58474460d5b90773289cc149865
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777337"
---
# <a name="state-property-example-vb"></a>State 屬性範例 (VB)
這個範例會使用 [State](./state-property-ado.md) 屬性來顯示非同步連接開啟和執行非同步命令時的訊息。  
  
```  
'BeginStateVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim Cnxn1 As ADODB.Connection  
    Dim Cnxn2 As ADODB.Connection  
    Dim cmdChange As ADODB.Command  
    Dim cmdRestore As ADODB.Command  
    Dim strCnxn As String  
    Dim strSQL As String  
  
    ' Open two asynchronous connections, displaying  
    ' a message while connecting  
    Set Cnxn1 = New ADODB.Connection  
    Set Cnxn2 = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
  
    Cnxn1.Open strCnxn, , , adAsyncConnect  
    Do Until Cnxn1.State <> adStateConnecting  
       Debug.Print "Opening first connection...."  
    Loop  
  
    Cnxn2.Open strCnxn, , , adAsyncConnect  
    Do Until Cnxn2.State <> adStateConnecting  
       Debug.Print "Opening second connection...."  
    Loop  
  
    ' Create two command objects  
    Set cmdChange = New ADODB.Command  
    cmdChange.ActiveConnection = Cnxn1  
    strSQL = "UPDATE Titles SET type = 'self_help' WHERE type = 'psychology'"  
    cmdChange.CommandText = strSQL  
  
    Set cmdRestore = New ADODB.Command  
    cmdRestore.ActiveConnection = Cnxn2  
    strSQL = "UPDATE Titles SET type = 'psychology' WHERE type = 'self_help'"  
    cmdRestore.CommandText = strSQL  
  
    ' Executing the commands, displaying a message  
    ' while they are executing  
    cmdChange.Execute , , adAsyncExecute  
    Do Until cmdChange.State <> adStateExecuting  
       Debug.Print "Change command executing...."  
    Loop  
  
    cmdRestore.Execute , , adAsyncExecute  
    Do Until cmdRestore.State <> adStateExecuting  
       Debug.Print "Restore command executing...."  
    Loop  
  
    ' clean up  
    Cnxn1.Close  
    Cnxn2.Close  
    Set Cnxn1 = Nothing  
    Set Cnxn2 = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not Cnxn1 Is Nothing Then  
        If Cnxn1.State = adStateOpen Then Cnxn1.Close  
    End If  
    Set Cnxn1 = Nothing  
  
    If Not Cnxn2 Is Nothing Then  
        If Cnxn2.State = adStateOpen Then Cnxn2.Close  
    End If  
    Set Cnxn2 = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndStateVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的記錄集物件 ](./recordset-object-ado.md)   
 [State 屬性 (ADO)](./state-property-ado.md)