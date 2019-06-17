---
title: 建立和執行簡單的命令 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Command object [ADO], creating and executing
- commands [ADO], creating and executing
ms.assetid: 0b81af6f-b9ae-4f7c-b59b-b5bdd775036f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6d0bba47aeb801688a1d9d55ee8f667153728162
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702131"
---
# <a name="creating-and-executing-a-simple-command"></a>建立和執行簡單的命令
簡單的命令是指未參數化，而且需要沒有持續性。 有三種方式，來建立和執行簡單的命令。  
  
-   使用**命令**物件  
  
-   使用**連線**物件  
  
-   使用**資料錄集**物件  
  
## <a name="using-a-command-object"></a>使用命令物件  
 若要建立簡單的命令，使用**命令**物件，您必須將指派的指示**CommandText**屬性**命令**物件，並設定適當的值**CommandType**屬性。 執行此命令需要開啟連接會指派給**ActiveConnection**屬性**命令**物件，然後呼叫**Execute**方法在 **命令**物件。  
  
 下列程式碼片段顯示使用的基本方法**命令**對資料來源執行命令的物件。 此範例會使用傳回的資料列的命令，並傳回命令執行的結果**資料錄集**物件。  
  
```  
    'BeginBasicCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objRs As New ADODB.Recordset  
  
    objCmd.CommandText = "SELECT OrderID, OrderDate, " & _  
                         "RequiredDate, ShippedDate " & _  
                         "FROM Orders " & _  
                         "WHERE CustomerID = 'ALFKI' " & _  
                         "ORDER BY OrderID"  
    objCmd.CommandType = adCmdText  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
    objCmd.ActiveConnection = objConn  
  
    ' Execute once and display...  
    Set objRs = objCmd.Execute  
  
    Debug.Print "ALFKI"  
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
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
'EndBasicCmd  
  
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
  
## <a name="using-a-recordset-object"></a>使用資料錄集物件  
 您也可以建立命令做為文字字串和 pa 才**開放**方法**資料錄集**物件時，命令類型 (adCmdText)，以及執行。 下列程式碼片段示範這種情況。  
  
```  
  
Const DS = "MySqlServer"  
Const DB = "Northwind"  
Const DP = "SQLOLEDB"  
  
Dim objRs As New ADODB.Recordset  
Dim CommandText As String  
Dim ConnctionString As String  
  
CommandText = "SELECT OrderID, OrderDate, " & _  
                     "RequiredDate, ShippedDate " & _  
                     "FROM Orders " & _  
                     "WHERE CustomerID = 'ALFKI' " & _  
                     "ORDER BY OrderID"  
ConnectionString = "Provider=" & DP & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;"  
  
' Connect to data source and execute the SQL command.  
objRs.Open CommandText, ConnectionString, _  
            adOpenStatic, adLockReadOnly, adCmdText  
  
Debug.Print "ALFKI"  
Do While Not objRs.EOF  
    Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                objRs(2) & vbTab & objRs(3)  
    objRs.MoveNext  
Loop  
  
'Clean up.  
objRs.Close  
Set objRs = Nothing  
```  
  
## <a name="using-a-connection-object"></a>使用連接物件  
 您也可以開啟的連線物件上執行命令。 上述程式碼範例現在會變成這樣：  
  
```  
Const DS = "MySqlServer"  
Const DB = "Northwind"  
Const DP = "SQLOLEDB"  
  
Dim objConn As New ADODB.Connection  
Dim objRs As New ADODB.Recordset  
  
CommandText = "SELECT OrderID, OrderDate, " & _  
                     "RequiredDate, ShippedDate " & _  
                     "FROM Orders " & _  
                     "WHERE CustomerID = 'ALFKI' " & _  
                     "ORDER BY OrderID"  
  
ConnectionString = "Provider=" & DP & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;"  
  
' Connect to the data source.  
objConn.Open ConnectionString  
  
' Execute command through the connection and display...  
Set objRs = objConn.Execute(CommandText)  
  
Debug.Print "ALFKI"  
Do While Not objRs.EOF  
    Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                objRs(2) & vbTab & objRs(3)  
    objRs.MoveNext  
Loop  
  
'Clean up.  
objRs.Close  
objConn.Close  
Set objRs = Nothing  
Set objConn = Nothing  
```
