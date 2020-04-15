---
title: 傳回代碼 ODBC |微軟文件
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
ms.openlocfilehash: 15e434025ed1201ca61371c2fb88e70143e131a5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304309"
---
# <a name="return-codes-odbc"></a>傳回碼 ODBC
ODBC 中的每個函數傳回一個代碼,稱為*返回代碼,* 它指示函數的總體成功或失敗。 程式邏輯通常會以傳回碼為基礎。  
  
 例如,以下代碼調用**SQLFetch**來檢索結果集中的行。 它檢查函數的返回代碼,以確定是否到達了結果集的末尾(SQL_NO_DATA)、是否返回了任何警告資訊(SQL_SUCCESS_WITH_INFO),或者是否發生了錯誤(SQL_ERROR)。  
  
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
  
 下表定義了返回代碼。  
  
|傳回碼|描述|  
|-----------------|-----------------|  
|SQL_SUCCESS|功能已成功完成。 應用程式調用**SQLGetDiagField**從標頭記錄檢索其他資訊。|  
|SQL_SUCCESS_WITH_INFO|功能成功完成,可能帶有非致命錯誤(警告)。 該應用程式調用**SQLGetDiagRec**或**SQLGetDiagField**來檢索其他資訊。|  
|SQL_ERROR|功能失敗。 該應用程式調用**SQLGetDiagRec**或**SQLGetDiagField**來檢索其他資訊。 函數的任何輸出參數的內容都是未定義的。|  
|SQL_INVALID_HANDLE|由於環境、連接、語句或描述符句柄無效,功能失敗。 這表示程式設計錯誤。 **SQLGetDiagRec**或**SQLGetDiagField**沒有其他資訊。 僅當句柄為空指標或類型錯誤(例如為需要連接句柄的參數傳遞語句句柄時)才返回此代碼。|  
|SQL_NO_DATA|沒有更多的數據可用。 該應用程式調用**SQLGetDiagRec**或**SQLGetDiagField**來檢索其他資訊。 可以返回 02xxx 類中的一個或多個驅動程式定義的狀態記錄。 **註:** 在 ODBC 2 中。*x*,此返回碼SQL_NO_DATA_FOUND。|  
|SQL_NEED_DATA|需要更多的數據,例如何時在執行時發送參數資料或需要額外的連接資訊。 該應用程式調用**SQLGetDiagRec**或**SQLGetDiagField**來檢索其他資訊(如果有)。|  
|SQL_STILL_EXECUTING|以非同步方式啟動的函數仍在執行中。 該應用程式調用**SQLGetDiagRec**或**SQLGetDiagField**來檢索其他資訊(如果有)。|
