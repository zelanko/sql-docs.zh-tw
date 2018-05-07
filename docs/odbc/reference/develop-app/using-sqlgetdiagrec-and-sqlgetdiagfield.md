---
title: 使用 SQLGetDiagRec 和 SQLGetDiagField |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 4f486bb1-fad8-4064-ac9d-61f2de85b68b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 555bc3ba25ba895b54384acb8772a4b4293e61c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="using-sqlgetdiagrec-and-sqlgetdiagfield"></a>使用 SQLGetDiagRec 和 SQLGetDiagField
應用程式呼叫**SQLGetDiagRec**或**SQLGetDiagField**擷取診斷資訊。 這些函式接受環境、 連接、 陳述式或描述元的控制代碼，並從上一次使用該控制代碼的函式傳回診斷。 新的函式呼叫使用該控制代碼時，會捨棄登入特定的控制代碼的診斷。 如果函式傳回多個診斷記錄，應用程式呼叫這些函式多次。狀態記錄的總數藉由呼叫擷取**SQLGetDiagField** SQL_DIAG_NUMBER 選項使用的標頭記錄 （記錄 0）。  
  
 應用程式來擷取個別的診斷欄位呼叫**SQLGetDiagField**並指定要擷取的欄位。 特定的診斷欄位並沒有任何意義，特定類型的控制代碼。 如需診斷欄位，其意義的清單，請參閱[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)函式描述。  
  
 藉由呼叫應用程式擷取 SQLSTATE、 原生錯誤碼和單一呼叫中的診斷訊息**SQLGetDiagRec**;**SQLGetDiagRec**無法用來從標頭記錄中擷取資訊。  
  
 例如，下列程式碼會提示使用者輸入的 SQL 陳述式，並加以執行。 如果未傳回任何診斷資訊，它會呼叫**SQLGetDiagField**取得狀態記錄的數目和**SQLGetDiagRec**所取得的 SQLSTATE、 原生錯誤碼和診斷訊息記錄。  
  
```  
SQLCHAR       SqlState[6], SQLStmt[100], Msg[SQL_MAX_MESSAGE_LENGTH];  
SQLINTEGER    NativeError;  
SQLSMALLINT   i, MsgLen;  
SQLRETURN     rc1, rc2;  
SQLHSTMT      hstmt;  
  
// Prompt the user for an SQL statement.  
GetSQLStmt(SQLStmt);  
  
// Execute the SQL statement and return any errors or warnings.  
rc1 = SQLExecDirect(hstmt, SQLStmt, SQL_NTS);  
if ((rc1 == SQL_SUCCESS_WITH_INFO) || (rc1 == SQL_ERROR)) {
   SQLLEN numRecs = 0;
   SQLGetDiagField(SQL_HANDLE_STMT, hstmt, 0, SQL_DIAG_NUMBER, &numRecs, 0, 0);
   // Get the status records.
   i = 1;  
   while (i <= numRecs && (rc2 = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, SqlState, &NativeError,  
            Msg, sizeof(Msg), &MsgLen)) != SQL_NO_DATA) {  
      DisplayError(SqlState,NativeError,Msg,MsgLen);  
      i++;  
   }  
}  
  
if ((rc1 == SQL_SUCCESS) || (rc1 == SQL_SUCCESS_WITH_INFO)) {  
   // Process statement results, if any.  
}  
```
