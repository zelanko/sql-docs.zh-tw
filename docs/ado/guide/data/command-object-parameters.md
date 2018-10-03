---
title: 命令物件參數 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Command object [ADO], parameters
ms.assetid: 10e7ef4a-78bf-4e91-931e-cbc6c065dd4c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f4fb4128333f1fdc5865186a202188fc64b6109f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47701736"
---
# <a name="command-object-parameters"></a>Command 物件參數
先前所討論的主題[建立和執行簡單的命令](../../../ado/guide/data/creating-and-executing-a-simple-command.md)。 針對使用更有趣[命令](../../../ado/reference/ado-api/command-object-ado.md)物件會顯示在下一個範例中，在其中具有已參數化 SQL 命令。 這項修改讓您能夠重複使用的命令，在不同的值中的參數每次的傳遞。 因為[備妥屬性](../../../ado/reference/ado-api/prepared-property-ado.md)屬性上的**命令**物件設定為**true**，ADO 需要編譯命令中指定的提供者[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)再執行第一次。 它也會保留在記憶體中已編譯的命令。 這會執行的命令稍微因為準備，但每次之後呼叫此命令時獲得效能的結果所需的額外負荷而執行的第一次。 因此，將會用一次以上時，才應該準備命令。  
  
```  
'BeginManualParamCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objParm1 As New ADODB.Parameter  
    Dim objRs As New ADODB.Recordset  
  
    ' Set the CommandText as a parameterized SQL query.  
    objCmd.CommandText = "SELECT OrderID, OrderDate, " & _  
                         "RequiredDate, ShippedDate " & _  
                         "FROM Orders " & _  
                         "WHERE CustomerID = ? " & _  
                         "ORDER BY OrderID"  
    objCmd.CommandType = adCmdText  
  
    ' Prepare command because we will be executing it more than once.  
    objCmd.Prepared = True  
  
    ' Create new parameter for CustomerID. Initial value is ALFKI.  
    Set objParm1 = objCmd.CreateParameter("CustId", adChar, _  
                    adParamInput, 5, "ALFKI")  
    objCmd.Parameters.Append objParm1  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
    objCmd.ActiveConnection = objConn  
  
    ' Execute once and display.  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    ' .Set new param value, re-execute command, and display.  
    objCmd("CustId") = "CACTU"  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    'clean up  
    objRs.Close  
    objConn.Close  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Set objParm1 = Nothing  
    Exit Sub  
  
ErrHandler:  
    'clean up  
    If objRs.State = adStateOpen Then  
        objRs.Close  
    End If  
  
    If objConn.State = adStateOpen Then  
        objConn.Close  
    End If  
  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Set objParm1 = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
'EndManualParamCmd  
  
'BeginNewConnection  
Private Function GetNewConnection() As ADODB.Connection  
    Dim oCn As New ADODB.Connection  
    Dim sCnStr As String  
  
    sCnStr = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    oCn.Open sCnStr  
  
    If oCn.State = adStateOpen Then  
        Set GetNewConnection = oCn  
    End If  
  
End Function  
'EndNewConnection  
```  
  
 並非所有提供者支援準備的命令。 如果提供者不支援命令準備，它就可能會傳回錯誤，因為這個屬性設定為 **，則為 True**。 如果它不會傳回錯誤，它會略過準備的命令並將設定要求**已準備**屬性設**false**。
