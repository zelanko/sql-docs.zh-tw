---
title: 陳述式的批次 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- statements [ODBC], batches
- batches [ODBC]
- ODBC applications, statements
- multiple statements, batches
- SQLMoreResults function
- SQLExecDirect function
ms.assetid: 057d7c1c-1428-4780-9447-a002ea741188
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8951469279e5c3577aef355e339397b329bb5d63
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206768"
---
# <a name="batches-of-statements"></a>陳述式的批次
  批次[!INCLUDE[tsql](../../../includes/tsql-md.md)]陳述式包含兩個或多個陳述式，並以分號 （;），單一字串傳遞至內建**SQLExecDirect**或是[SQLPrepare 函數](https://go.microsoft.com/fwlink/?LinkId=59360)。 例如:  
  
```  
SQLExecDirect(hstmt,   
    "SELECT * FROM Authors; SELECT * FROM Titles",  
    SQL_NTS);  
```  
  
 批次可能會比個別提交陳述式更有效率，因為其網路傳輸量通常較低。 使用[SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md)來定位下一步 時，結果集已完成，但目前的結果集。  
  
 當 ODBC 資料指標屬性設定為預設值 (資料列集大小為 1 的順向唯讀資料指標) 時，就一定可以使用批次。  
  
 如果針對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用伺服器資料指標時執行了批次，伺服器資料指標就會隱含地轉換成預設的結果集。 **SQLExecDirect**或是**SQLExecute**傳回 SQL_SUCCESS_WITH_INFO，而且呼叫**SQLGetDiagRec**傳回：  
  
```  
szSqlState = "01S02", pfNativeError = 0  
szErrorMsg = "[Microsoft][SQL Server Native Server Native Client]Cursor type changed."  
```  
  
## <a name="see-also"></a>另請參閱  
 [執行陳述式&#40;ODBC&#41;](executing-statements-odbc.md)  
  
  
