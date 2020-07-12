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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f56def542b71906d1e9432d724fdab8143ccb346
ms.sourcegitcommit: dacd9b6f90e6772a778a3235fb69412662572d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2020
ms.locfileid: "86279586"
---
# <a name="sqlcompleteasync-function"></a>SQLCompleteAsync 函式
**標準**  
 引進的版本： ODBC 3.8 標準合規性：無  
  
 **摘要**  
 **SQLCompleteAsync**可以用來判斷非同步函式何時使用以通知或輪詢為基礎的處理完成。 如需非同步作業的詳細資訊，請參閱[非同步執行](../../../odbc/reference/develop-app/asynchronous-execution.md)。  
  
 **SQLCompleteAsync**只會在 ODBC 驅動程式管理員中執行。  
  
 在以通知為基礎的非同步處理模式中，必須在驅動程式管理員引發用於通知的事件物件之後呼叫**SQLCompleteAsync** 。 **SQLCompleteAsync**完成非同步處理，且非同步函式會產生傳回碼。  
  
 在以輪詢為基礎的非同步處理模式中， **SQLCompleteAsync**是呼叫原始非同步函式的替代方法，而不需要在原始的非同步函式呼叫中指定引數。 不論是否已啟用 ODBC 資料指標程式庫，都可以使用**SQLCompleteAsync** 。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 源要在其上完成非同步處理的控制碼類型。 有效的值為 SQL_HANDLE_DBC 或 SQL_HANDLE_STMT。  
  
 *Handle*  
 源要在其上完成非同步處理的控制碼。 如果*handle*不是*HandleType*所指定之類型的有效控制碼， **SQLCompleteAsync**會傳回 SQL_INVALID_HANDLE。  
  
 如果*handle*不是*HandleType*所指定之類型的有效控制碼， **SQLCompleteAsync**會傳回 SQL_INVALID_HANDLE。  
  
 *AsyncRetCodePtr*  
 輸出緩衝區的指標，將包含非同步 API 的傳回碼。 如果*AsyncRetCodePtr*為 Null，則**SQLCompleteAsync**會傳回 SQL_ERROR。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_ERROR、SQL_NO_DATA 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 如果**SQLCompleteAsync**傳回 SQL_SUCCESS，應用程式應該從*AsyncRetCodePtr*所指向的緩衝區取得非同步函式的傳回碼。 如果有相關聯的 SQLSTATE，您可以呼叫**SQLGetDiagRec**與 SQL_HANDLE_STMT *HandleType*和語句控制碼，或是 SQL_HANDLE_DBC 和連接控制碼的*HandleType* ，來取得關聯的（如果有的話）。 這些診斷記錄會與非同步函式相關聯，而不是與這個**SQLCompleteAsync**函數關聯。  
  
 **SQLCompleteAsync**會傳回 SQL_SUCCESS 以外的程式碼，以指出未正確呼叫**SQLCompleteAsync** 。 在此情況下， **SQLCompleteAsync**不會張貼任何診斷記錄。 可能的傳回碼如下：  
  
-   SQL_INVALID_HANDLE： *HandleType*和*HANDLE*所指示的控制碼不是有效的控制碼。  
  
-   SQL_ERROR： *AsyncRetCodePtr*是 Null，或未在控制碼上啟用非同步處理。  
  
-   SQL_NO_DATA：在通知模式中，非同步作業不在進行中，或驅動程式管理員尚未通知應用程式。 在輪詢模式中，非同步作業不在進行中。  
  
## <a name="comments"></a>註解  
 在以輪詢為基礎的非同步處理模式中， *AsyncRetCodePtr*可能會在**SQLCompleteAsync**傳回 SQL_SUCCESS 時 SQL_STILL_EXECUTING。 應用程式應該持續輪詢，直到*AsyncRetCodePtr*不 SQL_STILL_EXECUTING 為止。 在以通知為基礎的非同步處理模式中， *AsyncRetCodePtr*永遠不會 SQL_STILL_EXECUTING。  
  
## <a name="see-also"></a>另請參閱  
 [非同步執行 (輪詢方法) ](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
