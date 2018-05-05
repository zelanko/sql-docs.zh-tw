---
title: 傳回碼 ODBC |Microsoft 文件
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
- return codes [ODBC]
- diagnostic information [ODBC], return codes
ms.assetid: e893b719-4392-476f-911a-5ed6da6f7e94
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 12751f87c9f9832567dc04ba7df7659e80e66897
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="return-codes-odbc"></a>ODBC 的傳回碼
在 ODBC 中的每個函式會傳回程式碼，稱為其*傳回碼，*指出整體成功或失敗函式。 程式邏輯通常會以傳回碼為基礎。  
  
 例如，下列程式碼呼叫**SQLFetch**擷取結果集的資料列。 它會檢查以判斷結果集已到達結尾 (SQL_NO_DATA)，如果傳回任何警告資訊 (SQL_SUCCESS_WITH_INFO)，或發生錯誤 (SQL_ERROR) 函式的傳回碼。  
  
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
  
|傳回碼|Description|  
|-----------------|-----------------|  
|SQL_SUCCESS|函式已順利完成。 應用程式會呼叫**SQLGetDiagField**擷取標頭記錄中的其他資訊。|  
|SQL_SUCCESS_WITH_INFO|已順利完成，可能發生非嚴重錯誤 （警告） 的函式。 應用程式會呼叫**SQLGetDiagRec**或**SQLGetDiagField**來擷取其他資訊。|  
|SQL_ERROR|函式失敗。 應用程式會呼叫**SQLGetDiagRec**或**SQLGetDiagField**來擷取其他資訊。 不會定義任何輸出引數，函式的內容。|  
|SQL_INVALID_HANDLE|函式失敗，因為無效的環境、 連接、 陳述式或描述項控制代碼。 這會指出程式設計錯誤。 沒有其他資訊可從**SQLGetDiagRec**或**SQLGetDiagField**。 只有在控制代碼為 null 指標，或類型錯誤，例如當陳述式控制代碼傳遞給需要連接控制代碼的引數時，會傳回這段程式碼。|  
|SQL_NO_DATA|無更多可用的資料。 應用程式會呼叫**SQLGetDiagRec**或**SQLGetDiagField**來擷取其他資訊。 可能會傳回類別 02xxx 中的一個或多個驅動程式定義的狀態記錄。 **注意：** ODBC 2 中。*x*，這會傳回 SQL_NO_DATA_FOUND 名為程式碼。|  
|SQL_NEED_DATA|需要更多資料，例如在執行階段則傳送參數資料，或需要其他連接資訊。 應用程式會呼叫**SQLGetDiagRec**或**SQLGetDiagField**擷取其他資訊，如果有的話。|  
|SQL_STILL_EXECUTING|以非同步方式啟動的函式仍在執行中。 應用程式會呼叫**SQLGetDiagRec**或**SQLGetDiagField**擷取其他資訊，如果有的話。|
