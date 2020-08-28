---
description: 以 Connection 物件方法的形式來呼叫預存程序
title: 在連線物件上呼叫預存程式做為方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- calling stored procedures [ADO]
- stored procedures [ADO]
- commands [ADO]
ms.assetid: 35ffdb79-a931-4271-a3bb-0cd804cf173e
author: rothja
ms.author: jroth
ms.openlocfilehash: 6194c9374258e23e7c5a388df9424f986fc899b0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991569"
---
# <a name="calling-a-stored-procedure-as-a-method-on-a-connection-object"></a>以 Connection 物件方法的形式來呼叫預存程序
您可以呼叫預存程式，就像是相關聯開啟 **連接** 物件上的原生方法一樣。 這類似于在 **連接** 物件上呼叫指名的命令。  
  
 下列 Visual Basic 程式碼範例會呼叫 Northwind 範例資料庫中的預存程式（稱為 CustOrdersOrders），這會在這裡再次列出以方便您使用。  
  
```  
CREATE PROCEDURE CustOrdersOrders @CustomerID nchar(5) AS  
SELECT OrderID, OrderDate, RequiredDate, ShippedDate  
FROM Orders  
WHERE CustomerID = @CustomerID  
ORDER BY OrderID  
```  
  
 下列程式碼範例示範如何呼叫預存程式，就像是相關聯開啟 **連接** 物件上的原生方法一樣。  
  
```  
Const DS = "MySQLServer"  
Const DB = "Northwind"  
Const DP = "SQLOLEDB"  
  
Dim objConn As New ADODB.Connection  
Dim objRs As New ADODB.Recordset  
Dim objComm As New ADODB.Command  
  
ConnectionString = "Provider=" & DP & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;"  
  
' Connect to the data source.  
objConn.Open ConnectionString  
  
' Set a stored procedure  
  
Set objComm.ActiveConnection = objConn  
  
' Execute the stored procedure on  
' the active connection object...  
'    "ALFKI" is the required input parameter,  
'    objRs is the resultant output variable.  
  
' Display the result.  
Debug.Print "Results returned from sp_CustOrdersOrders for ALFKI: "  
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
Set objComm = Nothing  
```  
  
## <a name="see-also"></a>另請參閱  
 [Connection 物件 (ADO)](../../reference/ado-api/connection-object-ado.md)