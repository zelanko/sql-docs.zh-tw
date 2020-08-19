---
description: 使用 SQLGetDiagRec 和 SQLGetDiagField
title: 使用 SQLGetDiagRec 和 SQLGetDiagField |Microsoft Docs
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
ms.openlocfilehash: 402cb326ac91e13db0d3ab5421bd5ddb097fb3db
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421432"
---
# <a name="using-sqlgetdiagrec-and-sqlgetdiagfield"></a>使用 SQLGetDiagRec 和 SQLGetDiagField
應用程式會呼叫 **SQLGetDiagRec** 或 **SQLGetDiagField** 來取得診斷資訊。 這些函數會接受環境、連接、語句或描述項控制碼，並從上次使用該處理的函式傳回診斷。 當使用該控制碼呼叫新的函式時，會捨棄記錄在特定控制碼上的診斷。 如果函式傳回多個診斷記錄，則應用程式會多次呼叫這些函數;藉由呼叫 **SQLGetDiagField** 的標頭記錄來抓取狀態記錄的總數， (記錄 0) 搭配 SQL_DIAG_NUMBER 選項。  
  
 應用程式會藉由呼叫 **SQLGetDiagField** 並指定要取出的欄位，以抓取個別的診斷欄位。 某些診斷欄位對於特定類型的控制碼沒有任何意義。 如需診斷欄位及其意義的清單，請參閱 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) 函數描述。  
  
 應用程式會藉由呼叫 **SQLGetDiagRec**，在單一呼叫中取出 SQLSTATE、原生錯誤碼和診斷訊息; **SQLGetDiagRec** 無法用來從標頭記錄中取出資訊。  
  
 例如，下列程式碼會提示使用者輸入 SQL 語句，然後執行它。 如果傳回任何診斷資訊，則會呼叫 **SQLGetDiagField** 以取得狀態記錄的數目和 **SQLGetDiagRec** ，以從這些記錄取得 SQLSTATE、原生錯誤碼和診斷訊息。  
  
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
