---
title: 陳述式的批次 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 651ff25ac3331820f93fae7cdd5fc85567738107
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47851968"
---
# <a name="batches-of-statements"></a>陳述式的批次
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  批次[!INCLUDE[tsql](../../../includes/tsql-md.md)]陳述式包含兩個或多個陳述式，並以分號 （;），單一字串傳遞至內建**SQLExecDirect**或是[SQLPrepare 函數](http://go.microsoft.com/fwlink/?LinkId=59360)。 例如：  
  
```  
SQLExecDirect(hstmt,   
    "SELECT * FROM Authors; SELECT * FROM Titles",  
    SQL_NTS);  
```  
  
 批次可能會比個別提交陳述式更有效率，因為其網路傳輸量通常較低。 使用[SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md)來定位下一步 時，結果集已完成，但目前的結果集。  
  
 當 ODBC 資料指標屬性設定為預設值 (資料列集大小為 1 的順向唯讀資料指標) 時，就一定可以使用批次。  
  
 如果針對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用伺服器資料指標時執行了批次，伺服器資料指標就會隱含地轉換成預設的結果集。 **SQLExecDirect**或是**SQLExecute**傳回 SQL_SUCCESS_WITH_INFO，而且呼叫**SQLGetDiagRec**傳回：  
  
```  
szSqlState = "01S02", pfNativeError = 0  
szErrorMsg = "[Microsoft][SQL Server Native Server Native Client]Cursor type changed."  
```  
  
## <a name="see-also"></a>另請參閱  
 [執行陳述式&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
