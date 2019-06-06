---
title: ActiveCommand 屬性範例 (VB) |Microsoft Docs
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
- ActiveCommand property [ADO], Visual Basic example
ms.assetid: 23b06499-62df-4f46-88eb-6da392f9b456
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 75c75540433e077cc5d96bb9b2f0c88c05a62bd6
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704041"
---
# <a name="activecommand-property-example-vb"></a>ActiveCommand 屬性範例 (VB)
此範例示範[ActiveCommand](../../../ado/reference/ado-api/activecommand-property-ado.md)屬性。  
  
 有一個副程式[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)物件，其**ActiveCommand**屬性用來顯示命令文字和參數，建立**資料錄集**。  
  
```  
'BeginActiveCommandVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
        'recordset and connection variables  
    Dim cmd As ADODB.Command  
    Dim rst As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
        'record variables  
    Dim strPrompt As String  
    Dim strName As String  
  
    Set Cnxn = New ADODB.Connection  
    Set cmd = New ADODB.Command  
  
    strPrompt = "Enter an author's name (e.g., Ringer): "  
    strName = Trim(InputBox(strPrompt, "ActiveCommandX Example"))  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
  
        'create SQL command string  
    cmd.CommandText = "SELECT * FROM Authors WHERE au_lname = ?"  
    cmd.Parameters.Append cmd.CreateParameter("LastName", adChar, adParamInput, 20, strName)  
  
    Cnxn.Open strCnxn  
    cmd.ActiveConnection = Cnxn  
  
        'create the recordset by executing command string  
    Set rst = cmd.Execute(, , adCmdText)  
        'see the results  
    Call ActiveCommandXprint(rst)  
  
    ' clean up  
    Cnxn.Close  
    Set rst = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rst Is Nothing Then  
        If rst.State = adStateOpen Then rst.Close  
    End If  
    Set rst = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndActiveCommandVB  
```  
  
 **ActiveCommandXprint**常式提供只**資料錄集**物件，但它必須列印命令文字和參數，建立**資料錄集**。 因為可以完成這**Recordset**物件的**ActiveCommand**屬性會產生相關聯[命令](../../../ado/reference/ado-api/command-object-ado.md)物件。  
  
 **命令**物件的[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性會產生建立參數化的命令**資料錄集**。 **命令**物件的[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合產生的已取代為命令的參數預留位置的值 (" **？** ")。  
  
 最後，會列印錯誤訊息或作者的名稱和識別碼。  
  
```  
'BeginActiveCommandPrintVB  
Public Sub ActiveCommandXprint(rstp As ADODB.Recordset)  
  
    Dim strName As String  
  
    strName = rstp.ActiveCommand.Parameters.Item("LastName").Value  
  
    Debug.Print "Command text = '"; rstp.ActiveCommand.CommandText; "'"  
    Debug.Print "Parameter = '"; strName; "'"  
  
    If rstp.BOF = True Then  
       Debug.Print "Name = '"; strName; "', not found."  
    Else  
       Debug.Print "Name = '"; rstp!au_fname; " "; rstp!au_lname; _  
             "', author ID = '"; rstp!au_id; "'"  
    End If  
  
    rstp.Close  
    Set rstp = Nothing  
End Sub  
'EndActiveCommandPrintVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [ActiveCommand 屬性 (ADO)](../../../ado/reference/ado-api/activecommand-property-ado.md)   
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
