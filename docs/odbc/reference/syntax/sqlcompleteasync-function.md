---
title: SQLCompleteAsync 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
f1_keywords:
- SQLCompleteAsync
helpviewer_keywords:
- SQLCompleteAsync function [ODBC]
ms.assetid: 1b97c46a-d2e5-4540-8239-9d975e5321c6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 736867be33531a73c0ada66a3be0f1245f1c483a
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537602"
---
# <a name="sqlcompleteasync-function"></a>SQLCompleteAsync 函式
**合規性**  
 導入的版本：ODBC 3.8  
  
 標準的合規性：None  
  
 **摘要**  
 **SQLCompleteAsync**可用來判斷何時非同步函式已完成使用任一個通知或輪詢為基礎的處理。 如需有關非同步作業的詳細資訊，請參閱 <<c0> [ 非同步執行](../../../odbc/reference/develop-app/asynchronous-execution.md)。  
  
 **SQLCompleteAsync**僅實作在 ODBC 驅動程式管理員。  
  
 在通知基礎的非同步處理模式中， **SQLCompleteAsync**必須驅動程式管理員會產生將用於通知的事件物件之後呼叫。 **SQLCompleteAsync**完成非同步處理和非同步函式會產生傳回碼。  
  
 在輪詢基礎的非同步處理模式中， **SQLCompleteAsync**呼叫原始的非同步函式，而不需要原始的非同步函式呼叫中指定的引數的替代方案。 **SQLCompleteAsync**可用不論是否啟用 ODBC 資料指標程式庫。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 [輸入]正在處理的控制代碼上可用來完成非同步的型別。 有效值為利用 SQL_HANDLE_DBC 或 SQL_HANDLE_STMT。  
  
 *Handle*  
 [輸入]控制代碼可用來完成非同步處理。 如果*處理*不是有效的控制代碼所指定型別的*HandleType*， **SQLCompleteAsync**傳回 SQL_INVALID_HANDLE。  
  
 如果*處理*不是有效的控制代碼所指定型別的*HandleType*， **SQLCompleteAsync**傳回 SQL_INVALID_HANDLE。  
  
 *AsyncRetCodePtr*  
 [輸出]將包含非同步 API 的傳回碼的緩衝區指標。 如果*AsyncRetCodePtr*為 NULL，就**SQLCompleteAsync**會傳回 SQL_ERROR。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_ERROR、 sql_no_data 之後或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 如果**SQLCompleteAsync**傳回 SQL_SUCCESS，應用程式應該獲得所指向緩衝區的非同步函式的傳回碼*AsyncRetCodePtr*。 相關聯的 SQLSTATE，如果有的話，可由呼叫**SQLGetDiagRec**具有*HandleType* SQL_HANDLE_STMT 和陳述式控制代碼或*HandleType*的 SQL_HANDLE_DBC 和連接控制代碼。 這些診斷記錄是相關聯的非同步函式不正確**SQLCompleteAsync**函式。  
  
 **SQLCompleteAsync**傳回 SQL_SUCCESS，表示以外的程式碼**SQLCompleteAsync**不會正確地進行呼叫。 **SQLCompleteAsync**在此情況下將會公佈任何診斷記錄。 可能的傳回碼如下：  
  
-   SQL_INVALID_HANDLE:所表示的控制代碼*HandleType*並*處理*不是有效的控制代碼。  
  
-   SQL_ERROR:*AsyncRetCodePtr*是 NULL，或控制代碼上未啟用非同步處理。  
  
-   SQL_NO_DATA 為止：在通知模式的非同步作業不在進行中或驅動程式管理員未收到通知的應用程式。 在輪詢模式中，非同步作業不是進行中。  
  
## <a name="comments"></a>註解  
 在輪詢基礎的非同步處理模式中， *AsyncRetCodePtr*可能是 SQL_STILL_EXECUTING 時**SQLCompleteAsync**都會傳回 SQL_SUCCESS。 應用程式應該繼續輪詢直到*AsyncRetCodePtr*不 SQL_STILL_EXECUTING。 在通知基礎的非同步處理模式中， *AsyncRetCodePtr*絕對不會 SQL_STILL_EXECUTING。  
  
## <a name="see-also"></a>另請參閱  
 [非同步執行 (輪詢方法)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
