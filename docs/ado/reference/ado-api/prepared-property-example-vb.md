---
title: 備妥的屬性範例（VB） |Microsoft Docs
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
- Prepared property [ADO], Visual Basic example
ms.assetid: e3a3db2d-7f73-4288-ad08-5468f251d610
author: rothja
ms.author: jroth
ms.openlocfilehash: 7d5cb8a583e5434e81922f556ae62e3d0f4f312f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761946"
---
# <a name="prepared-property-example-vb"></a>Prepared 屬性範例 (VB)
這個範例會藉由開啟兩個[命令](../../../ado/reference/ado-api/command-object-ado.md)物件（一個已備妥，一個尚未備妥）來示範[備](../../../ado/reference/ado-api/prepared-property-ado.md)妥的屬性。  
  
```  
'BeginPreparedVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim Cnxn As ADODB.Connection  
    Dim cmd1 As ADODB.Command  
    Dim cmd2 As ADODB.Command  
  
    Dim strCnxn As String  
    Dim strCmd As String  
    Dim sngStart As Single  
    Dim sngEnd As Single  
    Dim sngNotPrepared As Single  
    Dim sngPrepared As Single  
    Dim intLoop As Integer  
  
    ' Open a connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Set Cnxn = New ADODB.Connection  
    Cnxn.Open strCnxn  
  
    ' Create two command objects for the same  
    ' command - one prepared and one not prepared  
    strCmd = "SELECT title, type FROM Titles ORDER BY type"  
  
    Set cmd1 = New ADODB.Command  
    Set cmd1.ActiveConnection = Cnxn  
    cmd1.CommandText = strCmd  
  
    Set cmd2 = New ADODB.Command  
    Set cmd2.ActiveConnection = Cnxn  
    cmd2.CommandText = strCmd  
    cmd2.Prepared = True  
  
    ' Set a timer, then execute the unprepared  
    ' command 20 times  
    sngStart = Timer  
    For intLoop = 1 To 20  
        cmd1.Execute  
    Next intLoop  
    sngEnd = Timer  
    sngNotPrepared = sngEnd - sngStart  
  
    ' Reset the timer, then execute the prepared  
    ' command 20 times  
    sngStart = Timer  
    For intLoop = 1 To 20  
        cmd2.Execute  
    Next intLoop  
    sngEnd = Timer  
    sngPrepared = sngEnd - sngStart  
  
    ' Display performance results  
    MsgBox "Performance Results:" & vbCr & _  
        "   Not Prepared: " & Format(sngNotPrepared, _  
        "##0.000") & " seconds" & vbCr & _  
        "   Prepared: " & Format(sngPrepared, _  
        "##0.000") & " seconds"  
  
    ' clean up  
    Cnxn.Close  
    Set Cnxn = Nothing  
    Set cmd1 = Nothing  
    Set cmd2 = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    Set cmd1 = Nothing  
    Set cmd2 = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndPreparedVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [Command 物件（ADO）](../../../ado/reference/ado-api/command-object-ado.md)   
 [Prepared 屬性 (ADO)](../../../ado/reference/ado-api/prepared-property-ado.md)
