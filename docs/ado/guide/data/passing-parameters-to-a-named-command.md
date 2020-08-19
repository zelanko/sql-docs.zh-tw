---
description: 傳遞參數給具名命令
title: 將參數傳遞至命名的命令 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- named commands [ADO]
- commands [ADO], passing parameters to a named command
ms.assetid: 36e0cdbe-7f50-40f5-af0d-700f5d8dc75a
author: rothja
ms.author: jroth
ms.openlocfilehash: fa6ac56c3bb3e632ace019a2c8b2a97c96262421
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453070"
---
# <a name="passing-parameters-to-a-named-command"></a>傳遞參數給具名命令
就像命令的結果是以指名的命令的 *out* 變數形式傳遞時，參數化命令的參數 *可以做為變數傳入* 命名的命令。  
  
 下列程式碼範例會嘗試從 Northwind 資料庫中取得 **CustomerID** 為 "ALKFI" 之客戶所放置的所有訂單。 當呼叫指名的命令時，會提供 **CustomerID** 的值。  
  
```  
Const DS = "MySqlServer"  
Const DB = "Northwind"  
Const DP = "SQLOLEDB"  
  
Dim objConn As New ADODB.Connection  
Dim objRs As New ADODB.Recordset  
Dim objComm As New ADODB.Command  
  
CommandText = "SELECT OrderID, OrderDate, " & _  
                     "RequiredDate, ShippedDate " & _  
                     "FROM Orders " & _  
                     "WHERE CustomerID = ? " & _  
                     "ORDER BY OrderID"  
  
ConnectionString = "Provider=" & DP & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;"  
  
' Connect to the data source.  
objConn.Open ConnectionString  
  
' Set a named command.  
objComm.CommandText = CommandText  
objComm.CommandType = adCmdText  
objComm.Name = "GetOrdersOf"  
Set objComm.ActiveConnection = objConn  
  
' Call the named command, passing a CustomerID value  
' as the input parameter.   
'    "ALFKI" is the required input parameter,  
'    objRs is the resultant output variable.  
objConn.GetOrdersOf "ALKFI", objRs  
  
' Display the result.  
Debug.Print "All orders by ALFKI:"  
Do While Not objRs.EOF  
    Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                objRs(2) & vbTab & objRs(3)  
    objRs.MoveNext  
Loop  
  
' Clean up.  
objRs.Close  
objConn.Close  
Set objRs = Nothing  
Set objConn = Nothing  
Set objComm = Nothing  
```  
  
 請注意，所有輸入參數必須在任何輸出變數之前，而且參數的資料類型必須相符，或是可以轉換成對應欄位的資料類型。 下列語句-  
  
```  
objConn.GetOrdersOf 12345, objRs  
```  
  
 -會產生不相符資料類型的錯誤，因為必要的輸入參數是 **字串** 類型，而不是 **整數** 類型。  
  
 下列呼叫：  
  
```  
objConn.GetOrdersOf "12345", objRs  
```  
  
 -有效，但會產生空的結果集，因為資料庫中不存在這類記錄。  
  
## <a name="see-also"></a>另請參閱  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
