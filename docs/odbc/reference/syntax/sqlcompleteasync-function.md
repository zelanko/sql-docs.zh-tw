---
title: "SQLCompleteAsync 函式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQLCompleteAsync
helpviewer_keywords:
- SQLCompleteAsync function [ODBC]
ms.assetid: 1b97c46a-d2e5-4540-8239-9d975e5321c6
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 83f44395e0c7ed8d102bee046b19aefe96c156b5
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcompleteasync-function"></a>SQLCompleteAsync 函式
**一致性**  
 版本引進了： ODBC 3.8  
  
 標準相容性： 無  
  
 **摘要**  
 **SQLCompleteAsync**可用來判斷完成使用任一個通知或輪詢基礎處理的非同步函式時。 如需有關非同步作業的詳細資訊，請參閱[非同步執行](../../../odbc/reference/develop-app/asynchronous-execution.md)。  
  
 **SQLCompleteAsync**僅實作 ODBC 驅動程式管理員。  
  
 在通知基礎的非同步處理模式中， **SQLCompleteAsync**必須驅動程式管理員會引發事件物件，用於通知之後呼叫。 **SQLCompleteAsync**完成非同步處理和非同步函式會產生傳回碼。  
  
 在輪詢非同步處理模式中， **SQLCompleteAsync**呼叫原始的非同步函式，而不需要原始的非同步函式呼叫中指定的引數的替代方案。 **SQLCompleteAsync**可用無論是否已啟用 ODBC 資料指標程式庫。  
  
## <a name="syntax"></a>語法  
  
```vb  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 [輸入]完成非同步的控點的類型處理。 有效值為利用 SQL_HANDLE_DBC 或 SQL_HANDLE_STMT。  
  
 *Handle*  
 [輸入]完成非同步的控點處理。 如果*處理*不是有效的控制代碼所指定型別的*HandleType*， **SQLCompleteAsync**傳回 SQL_INVALID_HANDLE。  
  
 如果*處理*不是有效的控制代碼所指定型別的*HandleType*， **SQLCompleteAsync**傳回 SQL_INVALID_HANDLE。  
  
 *AsyncRetCodePtr*  
 [輸出]將包含了非同步 API 的傳回碼的緩衝區指標。 如果*AsyncRetCodePtr*是 NULL， **SQLCompleteAsync**會傳回 SQL_ERROR。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_ERROR、 sql_no_data 為止或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 如果**SQLCompleteAsync**傳回 SQL_SUCCESS，應用程式應該從所指向的緩衝區取得非同步函式的傳回碼*AsyncRetCodePtr*。 相關聯的 SQLSTATE，如果有的話，可透過呼叫**SQLGetDiagRec**與*HandleType* SQL_HANDLE_STMT 和陳述式控制代碼或*HandleType* SQL_ 的HANDLE_DBC 和連接控制代碼。 這些診斷記錄相關聯的非同步函式，這不**SQLCompleteAsync**函式。  
  
 **SQLCompleteAsync**傳回 SQL_SUCCESS，表示以外的程式碼**SQLCompleteAsync**呼叫不正確。 **SQLCompleteAsync**在此情況下將會公佈任何診斷記錄。 可能的傳回碼如下：  
  
-   SQL_INVALID_HANDLE： 所指定的控制代碼*HandleType*和*處理*不是有效的控制代碼。  
  
-   SQL_ERROR: *AsyncRetCodePtr*是 NULL，或控制代碼上未啟用非同步處理。  
  
-   SQL_NO_DATA： 以通知模式的非同步作業不在進行中或驅動程式管理員未收到通知的應用程式。 在輪詢模式中，非同步作業不在進行中。  
  
## <a name="comments"></a>註解  
 在輪詢非同步處理模式中， *AsyncRetCodePtr*可能 SQL_STILL_EXECUTING 時**SQLCompleteAsync**都會傳回 SQL_SUCCESS。 應用程式應該保留輪詢直到*AsyncRetCodePtr*不 SQL_STILL_EXECUTING。 在通知基礎的非同步處理模式中， *AsyncRetCodePtr*絕對不會 SQL_STILL_EXECUTING。  
  
## <a name="see-also"></a>另請參閱  
 [非同步執行 （輪詢方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)

