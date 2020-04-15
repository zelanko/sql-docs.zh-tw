---
title: 使用者輸入的 SQL 語句 |微軟文件
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
ms.openlocfilehash: bf2f8cf36be392cb42a970fa2fb0b19c35daeb39
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301959"
---
# <a name="sql-statements-entered-by-the-user"></a>使用者所輸入的 SQL 陳述式
執行暫時分析的應用程式通常還允許使用者直接輸入 SQL 語句。 例如：  
  
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
  
 此方法簡化了應用程式編碼;應用程式依賴於使用者生成 SQL 語句和數據源來檢查該語句的有效性。 由於很難編寫能夠充分暴露 SQL 的複雜性的圖形使用者介面,因此只需要求使用者輸入 SQL 語句文本可能是一種更可取的選擇。 但是,這要求用戶不僅瞭解 SQL,還知道要查詢的數據源的架構。 某些應用程式提供圖形使用者介面,使用者可以通過該介面創建基本的 SQL 語句,並提供文本介面,使用者可以使用該介面對其進行修改。
