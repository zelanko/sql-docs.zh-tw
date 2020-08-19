---
description: 可傳回資料錄集的 JScript 程式碼範例
title: 傳回記錄集的 JScript 程式碼範例 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- JScript
helpviewer_keywords:
- Recordset [ADO]
ms.assetid: 74aad8a6-06cc-4a2c-811a-d78f9b741d84
author: rothja
ms.author: jroth
ms.openlocfilehash: e6aea6b2e423dab4fb58b3e683081f7d3fdb6850
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453200"
---
# <a name="jscript-code-example-to-return-a-recordset"></a>可傳回資料錄集的 JScript 程式碼範例
## <a name="jscript-code-rsjs"></a>JScript 程式碼 ( # A0)   
  
```  
main();  
  
function main()  
{  
  DP = "SQLOLEDB";  
  DS = "MySQLServer";  
  DB = "NORTHWIND";  
  
  adOpenForwardOnly = 0;  
  adLockReadOnly = 1;  
  adCmdText = 1;  
  try   
  {  
    var objRs = new ActiveXObject("ADODB.Recordset");  
  }  
  catch (e)  
  {  
    alert("ADODB namespace not found.");  
    exit(0);  
  }  
  
  strConn =  "Provider="         +DP+  
            ";Initial Catalog="  +DB+  
            ";Data Source="      +DS+  
            ";Integrated Security=SSPI;"  
  strComm = "SELECT ProductID,ProductName,UnitPrice "+  
            "FROM Products " +   
            "WHERE CategoryID = 7"  // select Produce  
  
  objRs.open(strComm,   
             strConn,   
             adOpenForwardOnly,  
             adLockReadOnly,  
             adCmdText);  
  
  objRs.MoveFirst();  
  while (objRs.EOF != true)   
  {  
    alert(objRs("ProductID")+"\t"  
         +objRs("ProductName")+"\t"  
         +objRs("UnitPrice"));  
    objRs.MoveNext();  
  }  
  
  objRs.Close  
  objRs = null;  
}  
  
function alert(str)  
{  
  WScript.Echo(str);  
}  
```  
  
#### <a name="try-it"></a>請嘗試  
  
1.  將上述程式碼儲存到文字檔中。 將檔案儲存為 rs.js。  
  
2.  開啟命令提示字元，並將您已儲存 JScript 檔案 ( # A0) 的目錄。  
  
3.  `CScript rs.js`從命令提示字元輸入。
