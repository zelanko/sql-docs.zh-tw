---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e5f780f9abc47a367a1825d51b12159292ace5da
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020417"
---
# <a name="return-codes-odbc"></a>傳回碼 ODBC
ODBC 中的每個函式都會傳回稱為其傳回碼的程式碼 *，* 以指出函數的整體成功或失敗。 程式邏輯通常會以傳回碼為基礎。  
  
 例如，下列程式碼會呼叫**SQLFetch**來取出結果集中的資料列。 它會檢查函式的傳回碼，以判斷是否已達到結果集的結尾（SQL_NO_DATA）、是否已傳回任何警告資訊（SQL_SUCCESS_WITH_INFO），或者是否發生錯誤（SQL_ERROR）。  
  
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
|SQL_SUCCESS|函數已順利完成。 應用程式會呼叫**SQLGetDiagField** ，以從標頭記錄中取得其他資訊。|  
|SQL_SUCCESS_WITH_INFO|函數已順利完成，可能發生非嚴重錯誤（警告）。 應用程式會呼叫**SQLGetDiagRec**或**SQLGetDiagField** ，以取得其他資訊。|  
|SQL_ERROR|函數失敗。 應用程式會呼叫**SQLGetDiagRec**或**SQLGetDiagField** ，以取得其他資訊。 函式的任何輸出引數內容都未定義。|  
|SQL_INVALID_HANDLE|因為環境、連接、語句或描述項控制碼無效，所以函數失敗。 這表示程式設計錯誤。 **SQLGetDiagRec**或**SQLGetDiagField**中不提供任何其他資訊。 只有當控制碼為 null 指標或類型錯誤時（例如，針對需要連接控制碼的引數傳遞語句控制碼時），才會傳回此程式碼。|  
|SQL_NO_DATA|沒有其他可用的資料。 應用程式會呼叫**SQLGetDiagRec**或**SQLGetDiagField** ，以取得其他資訊。 可能會傳回類別02xxx 中的一或多個驅動程式定義狀態記錄。 **注意：** 在 ODBC 2 中。*x*，此傳回碼的名稱為 SQL_NO_DATA_FOUND。|  
|SQL_NEED_DATA|需要更多資料，例如在執行時間傳送參數資料，或需要其他連接資訊。 應用程式會呼叫**SQLGetDiagRec**或**SQLGetDiagField**來取得其他資訊（如果有的話）。|  
|SQL_STILL_EXECUTING|以非同步方式啟動的函式仍在執行中。 應用程式會呼叫**SQLGetDiagRec**或**SQLGetDiagField**來取得其他資訊（如果有的話）。|
