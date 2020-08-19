---
description: 使用者所輸入的 SQL 陳述式
title: 使用者輸入的 SQL 語句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- user-entered SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], entered by user
ms.assetid: 109af162-93ba-425a-8fe5-49c7dc7cc784
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6d7d7ee7ffc2a4c949173c3eee888e4c41b9e741
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424540"
---
# <a name="sql-statements-entered-by-the-user"></a>使用者所輸入的 SQL 陳述式
執行臨機操作分析的應用程式通常也會允許使用者直接輸入 SQL 語句。 例如：  
  
```  
SQLCHAR *     Statement, SqlState[6], Msg[SQL_MAX_MESSAGE_LENGTH];  
SQLSMALLINT   i, MsgLen;  
SQLINTEGER    NativeError;  
SQLRETURN     rc1, rc2;  
  
// Prompt user for SQL statement.  
GetSQLStatement(Statement);  
  
// Execute the statement directly. Because it will be executed only once,  
// do not prepare it.  
rc1 = SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Process any errors or returned information.  
if ((rc1 == SQL_ERROR) || rc1 == SQL_SUCCESS_WITH_INFO) {  
   i = 1;  
   while ((rc2 = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, SqlState, &NativeError,  
         Msg, sizeof(Msg), &MsgLen)) != SQL_NO_DATA) {  
      DisplayError(SqlState, NativeError, Msg, MsgLen);  
      i++;  
   }  
}  
```  
  
 這種方法可簡化應用程式撰寫程式碼;應用程式會依賴使用者建立 SQL 語句，並在資料來源上檢查語句的有效性。 因為很難撰寫圖形化使用者介面來適當地公開 SQL 的複雜，所以直接要求使用者輸入 SQL 語句文字可能是最好的替代方法。 不過，這需要使用者不僅知道 SQL，也需要知道所查詢資料來源的架構。 有些應用程式會提供圖形化使用者介面，讓使用者可以用它來建立基本的 SQL 語句，也可以提供文字介面讓使用者可以修改它。
