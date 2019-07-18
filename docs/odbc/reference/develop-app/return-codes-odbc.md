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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020417"
---
# <a name="return-codes-odbc"></a>傳回碼 ODBC
ODBC 中的每個函式傳回的程式碼中，然後再稱為其*傳回碼、* 指出整體成功或失敗函式。 程式邏輯通常會以傳回碼為基礎。  
  
 例如，下列程式碼會呼叫**SQLFetch**來擷取結果集的資料列。 它會檢查來判斷結果集已到達結尾 (SQL_NO_DATA)，如果傳回任何警告資訊 (SQL_SUCCESS_WITH_INFO)，或發生錯誤 (SQL_ERROR) 函式的傳回碼。  
  
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
|SQL_SUCCESS|已成功完成時，函式。 應用程式會呼叫**SQLGetDiagField**擷取標頭記錄中的其他資訊。|  
|SQL_SUCCESS_WITH_INFO|已順利完成，可能發生非嚴重錯誤 （警告） 的函式。 應用程式會呼叫**SQLGetDiagRec**或是**SQLGetDiagField**來擷取其他資訊。|  
|SQL_ERROR|失敗函式。 應用程式會呼叫**SQLGetDiagRec**或是**SQLGetDiagField**來擷取其他資訊。 此函式的任何輸出引數的內容為未定義。|  
|SQL_INVALID_HANDLE|函式失敗，因為無效的環境、 連接、 陳述式或描述元控制代碼。 這會指出程式設計錯誤。 會提供任何額外的資訊**SQLGetDiagRec**或是**SQLGetDiagField**。 控制代碼為 null 指標，或錯誤的型別，例如當陳述式控制代碼傳遞的引數，需要在連接控制代碼時，只傳回此程式碼。|  
|SQL_NO_DATA|可使用任何更多的資料不。 應用程式會呼叫**SQLGetDiagRec**或是**SQLGetDiagField**來擷取其他資訊。 可能會傳回類別 02xxx 中的一或多個驅動程式定義的狀態記錄。 **注意：** 在 ODBC 2。*x*，這會傳回 SQL_NO_DATA_FOUND 命名為程式碼。|  
|SQL_NEED_DATA|需要更多資料，例如在執行階段則傳送參數資料，或其他連接資訊是必要的。 應用程式會呼叫**SQLGetDiagRec**或是**SQLGetDiagField**擷取的詳細資訊，如果有的話。|  
|SQL_STILL_EXECUTING|以非同步方式啟動的函式仍在執行中。 應用程式會呼叫**SQLGetDiagRec**或是**SQLGetDiagField**擷取的詳細資訊，如果有的話。|
