---
title: 傳遞參數至具名命令 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- named commands [ADO]
- commands [ADO], passing parameters to a named command
ms.assetid: 36e0cdbe-7f50-40f5-af0d-700f5d8dc75a
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 94f5d5fb25406b581ccd1bdadbaef5934360c7de
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="passing-parameters-to-a-named-command"></a>將參數傳遞至具名的命令
就像命令的結果會當做傳遞*出*具名命令參數的變數參數化的命令可以針對已做為傳入的*中*具名命令的變數。  
  
 下列程式碼範例會嘗試擷取的所有訂單放置客戶其**CustomerID** "ALKFI"是從 Northwind 資料庫。 值**CustomerID**提供在具名的命令呼叫時的時間。  
  
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
  
 請注意，所有輸入的參數必須在前面的任何輸出變數的資料類型的參數必須符合或可以轉換成對應的欄位的。 下列陳述式：  
  
```  
objConn.GetOrdersOf 12345, objRs  
```  
  
 -因為必要的輸入的參數，會導致錯誤的資料類型不符，**字串**類型，不是**整數**型別。  
  
 下列呼叫：  
  
```  
objConn.GetOrdersOf "12345", objRs  
```  
  
 — 有效，但會產生空的結果集，因為沒有這類記錄存在於資料庫中。  
  
## <a name="see-also"></a>另請參閱  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
