---
title: 語句的批次 |Microsoft Docs
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 013a8e8ab09b192a2ff7a04a9d7ddc5be1395636
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82710742"
---
# <a name="batches-of-statements"></a>陳述式的批次
  語句的批次 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 包含兩個或多個語句，以分號（;)，並內建于傳遞至**SQLExecDirect**或[SQLPrepare 函數](https://go.microsoft.com/fwlink/?LinkId=59360)的單一字串。 例如：  
  
```  
SQLExecDirect(hstmt,   
    "SELECT * FROM Authors; SELECT * FROM Titles",  
    SQL_NTS);  
```  
  
 批次可能會比個別提交陳述式更有效率，因為其網路傳輸量通常較低。 當使用目前的結果集完成時，請使用[SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md)來取得下一個結果集的位置。  
  
 當 ODBC 資料指標屬性設定為預設值 (資料列集大小為 1 的順向唯讀資料指標) 時，就一定可以使用批次。  
  
 如果針對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用伺服器資料指標時執行了批次，伺服器資料指標就會隱含地轉換成預設的結果集。 **SQLExecDirect**或**SQLExecute**會傳回 SQL_SUCCESS_WITH_INFO，而對**SQLGetDiagRec**的呼叫會傳回：  
  
```  
szSqlState = "01S02", pfNativeError = 0  
szErrorMsg = "[Microsoft][SQL Server Native Server Native Client]Cursor type changed."  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;執行語句](executing-statements-odbc.md)  
  
  
