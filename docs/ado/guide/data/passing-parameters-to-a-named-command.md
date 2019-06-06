---
title: 將參數傳遞給具名命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6863a14a467e1d884d43b982451ec5807820486b
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701845"
---
# <a name="passing-parameters-to-a-named-command"></a>傳遞參數給具名命令
就如同命令的結果會當做傳遞*出*具名命令，也就是參數的變數參數化的命令可以針對已傳入作為*中*具名命令的變數。  
  
 下列程式碼範例會嘗試擷取的所有訂單客戶所下的**CustomerID**取自 Northwind 資料庫中的"ALKFI 」。 值**CustomerID**會在呼叫具名的命令時的時間提供。  
  
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
  
 請注意，所有輸入的參數必須在前面的任何輸出變數和參數資料類型必須符合或可以轉換為所對應的欄位。 下列陳述式：  
  
```  
objConn.GetOrdersOf 12345, objRs  
```  
  
 -因為必要的輸入的參數是的會導致不相符的資料類型的錯誤**字串**型別，而非**整數**型別。  
  
 下列呼叫：  
  
```  
objConn.GetOrdersOf "12345", objRs  
```  
  
 -有效，但會產生空的結果集，因為沒有這類記錄存在於資料庫中。  
  
## <a name="see-also"></a>另請參閱  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
