---
title: 隱含資料指標轉換 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 300ce02538a59ef043424d866ad4ce49267fcfa4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62711566"
---
# <a name="implicit-cursor-conversions-odbc"></a>隱含資料指標轉換 (ODBC)
  應用程式可以要求透過資料指標類型[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)然後執行伺服端資料指標要求的類型不支援的 SQL 陳述式。 呼叫**SQLExecute**或是**SQLExecDirect**會傳回 SQL_SUCCESS_WITH_INFO 和**SQLGetDiagRec**傳回：  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 應用程式可以判斷何種資料指標現在正在使用藉由呼叫**SQLGetStmtOption**設定為 SQL_CURSOR_TYPE。 資料指標類型轉換只適用於一個陳述式。 下一步**SQLExecDirect**或是**SQLExecute**時，必須使用原始的陳述式資料指標設定。  
  
## <a name="see-also"></a>另請參閱  
 [資料指標程式設計詳細資料&#40;ODBC&#41;](cursor-programming-details-odbc.md)  
  
  
