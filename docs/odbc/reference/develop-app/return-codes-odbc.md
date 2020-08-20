---
description: 傳回碼 ODBC
title: 傳回碼 ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- return codes [ODBC]
- diagnostic information [ODBC], return codes
ms.assetid: e893b719-4392-476f-911a-5ed6da6f7e94
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 79a06ad170f747c3841c42eadef0288af6fef39a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494634"
---
# <a name="return-codes-odbc"></a>傳回碼 ODBC
ODBC 中的每個函式都會傳回稱為其傳回 *碼* 的程式碼，表示函式的整體成功或失敗。 程式邏輯通常會以傳回碼為基礎。  
  
 例如，下列程式碼會呼叫 **SQLFetch** 來取出結果集中的資料列。 它會檢查函數的傳回碼，以判斷是否已達到結果集的結尾 (SQL_NO_DATA) ，如果傳回任何警告資訊 (SQL_SUCCESS_WITH_INFO) ，或發生 (SQL_ERROR) 錯誤。  
  
```  
SQLRETURN   rc;  
SQLHSTMT    hstmt;  
  
while ((rc=SQLFetch(hstmt)) != SQL_NO_DATA) {  
   if (rc == SQL_SUCCESS_WITH_INFO) {  
      // Call function to display warning information.  
   } else if (rc == SQL_ERROR) {  
      // Call function to display error information.  
      break;  
   }  
   // Process row.  
}  
```  
  
 傳回碼 SQL_INVALID_HANDLE 永遠會指出程式設計錯誤，而且絕不會在執行階段發生。 雖然 SQL_ERROR 可能會指出程式設計錯誤，其他所有傳回碼還是會提供執行階段資訊。  
  
 下表定義傳回碼。  
  
|傳回碼|描述|  
|-----------------|-----------------|  
|SQL_SUCCESS|函數已順利完成。 應用程式會呼叫 **SQLGetDiagField** ，以從標頭記錄中取出其他資訊。|  
|SQL_SUCCESS_WITH_INFO|函數已順利完成，可能發生非嚴重錯誤 (警告) 。 應用程式會呼叫 **SQLGetDiagRec** 或 **SQLGetDiagField** 來取得其他資訊。|  
|SQL_ERROR|函數失敗。 應用程式會呼叫 **SQLGetDiagRec** 或 **SQLGetDiagField** 來取得其他資訊。 函數的任何輸出引數內容都未定義。|  
|SQL_INVALID_HANDLE|函數失敗，因為環境、連接、語句或描述項控制碼無效。 這表示程式設計錯誤。 **SQLGetDiagRec**或**SQLGetDiagField**不提供任何其他資訊。 只有當控制碼是 null 指標或錯誤的型別（例如針對需要連接控制碼的引數傳遞語句控制碼時），才會傳回此程式碼。|  
|SQL_NO_DATA|沒有其他可用的資料。 應用程式會呼叫 **SQLGetDiagRec** 或 **SQLGetDiagField** 來取得其他資訊。 可能會傳回類別02xxx 中的一或多個驅動程式定義狀態記錄。 **注意：**  在 ODBC 2 中。*x*，此傳回碼的名稱為 SQL_NO_DATA_FOUND。|  
|SQL_NEED_DATA|需要更多資料，例如在執行時間傳送參數資料時，或需要其他連接資訊。 應用程式會呼叫 **SQLGetDiagRec** 或 **SQLGetDiagField** 來取得其他資訊（如果有的話）。|  
|SQL_STILL_EXECUTING|以非同步方式啟動的函數仍在執行中。 應用程式會呼叫 **SQLGetDiagRec** 或 **SQLGetDiagField** 來取得其他資訊（如果有的話）。|
