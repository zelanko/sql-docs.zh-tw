---
title: 隱含資料指標轉換 (ODBC) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b1f1880ea464949bd962bab002d1f1129261463c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034352"
---
# <a name="implicit-cursor-conversions-odbc"></a>隱含資料指標轉換 (ODBC)
  應用程式可以要求透過資料指標類型[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) ，然後執行伺服端資料指標要求的型別不支援的 SQL 陳述式。 呼叫**SQLExecute**或**SQLExecDirect**傳回 SQL_SUCCESS_WITH_INFO 和**SQLGetDiagRec**傳回：  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 應用程式可以判斷哪些類型的資料指標正在使用藉由呼叫**SQLGetStmtOption**設定為 SQL_CURSOR_TYPE。 資料指標類型轉換只適用於一個陳述式。 下一步 **SQLExecDirect**或**SQLExecute**都是使用原始陳述式資料指標設定。  
  
## <a name="see-also"></a>另請參閱  
 [資料指標程式設計詳細&#40;ODBC&#41;](cursor-programming-details-odbc.md)  
  
  