---
description: 使用 Recordset 物件
title: 使用記錄集物件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 01c630d8-eb35-4bd0-a99f-7c0f85316cc1
author: rothja
ms.author: jroth
ms.openlocfilehash: fef7e779c11dac06b2cda5401250577e9bb7162e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452610"
---
# <a name="using-a-recordset-object"></a>使用 Recordset 物件
或者，您也可以使用 **記錄集。開啟** 以隱含方式建立連線，並在單一作業中透過該連接發出命令。 例如，在 Visual Basic：  
  
```  
Dim oRs As ADODB.Recordset  
Dim sConn As String  
Dim sSQL as String  
  
sConn = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _             "Initial Catalog='Northwind';Integrated Security='SSPI';"  
  
sSQL = "SELECT ProductID, ProductName, CategoryID, UnitPrice " & _  
             "FROM Products"  
  
' Create and Open the Recordset object.  
Set oRs = New ADODB.Recordset  
oRs.CursorLocation = adUseClient  
oRs.Open sSQL, sConn, adOpenStatic, _  
               adLockBatchOptimistic, adCmdText  
  
MsgBox oRs.RecordCount  
  
oRs.MarshalOptions = adMarshalModifiedOnly  
' Disconnect the Recordset.  
Set oRs.ActiveConnection = Nothing  
oRs.Close          
Set oRs = Nothing  
```  
  
 請注意， **or** 會採用連接字串 (*sConn*) ，取代 **連接** 物件 (*oConn*) ，作為其 **ActiveConnection** 參數的值。 此外，也會藉由設定**記錄集**物件上的**CursorLocation**屬性來強制執行用戶端資料指標類型。 同樣地，請與 **HelloData** 範例對比。
