---
title: 使用 SQLGetDiagRec 和 SQLGetDiagField |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 4f486bb1-fad8-4064-ac9d-61f2de85b68b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69a17086253b40469b0ed98cb6f870f319f03f52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306749"
---
# <a name="using-sqlgetdiagrec-and-sqlgetdiagfield"></a>使用 SQLGetDiagRec 和 SQLGetDiagField
應用程式呼叫**SQLGetDiagRec**或**SQLGetDiagField**來檢索診斷資訊。 這些函數接受環境、連接、語句或描述符句柄,並從上次使用該句柄的函數返回診斷。 當使用該句柄調用新功能時,在特定句柄上記錄的診斷將被丟棄。 如果函數返回多個診斷記錄,應用程式會多次調用這些函數;如果函數返回多個診斷記錄,則調用這些函數。通過使用SQL_DIAG_NUMBER選項調用**SQLGetDiagField**獲取標頭記錄(記錄 0)來檢索狀態記錄的總數。  
  
 應用程式通過調用**SQLGetDiagField**並指定要檢索的欄位來檢索各個診斷欄位。 某些診斷欄位對某些類型的句柄沒有任何意義。 有關診斷欄位及其含義的清單,請參閱[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)函數說明。  
  
 應用程式通過調用**SQLGetDiagRec**在單個調用中檢索 SQLSTATE、本機錯誤代碼和診斷消息。**SQLGetDiagRec**不能用於從標頭記錄中檢索資訊。  
  
 例如,以下代碼提示使用者執行 SQL 語句。 如果返回任何診斷資訊,它將調用**SQLGetDiagField**獲取狀態記錄的數量,並從這些記錄獲取**SQLSTATE、** 本機錯誤代碼和診斷消息。  
  
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
