---
description: SQLCompleteAsync 函式
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
ms.openlocfilehash: bb5ec8ff7c0aa96e37ce66cabb1e18c9993e95f7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448759"
---
# <a name="sqlcompleteasync-function"></a>SQLCompleteAsync 函式
**一致性**  
 引進的版本： ODBC 3.8 標準合規性：無  
  
 **總結**  
 **SQLCompleteAsync** 可以用來判斷非同步函式何時完成，方法是使用以通知或輪詢為基礎的處理。 如需非同步作業的詳細資訊，請參閱 [非同步執行](../../../odbc/reference/develop-app/asynchronous-execution.md)。  
  
 **SQLCompleteAsync** 只會在 ODBC 驅動程式管理員中執行。  
  
 在以通知為基礎的非同步處理模式中，您必須在驅動程式管理員引發用於通知的事件物件之後呼叫 **SQLCompleteAsync** 。 **SQLCompleteAsync** 完成非同步處理，而非同步函式將會產生傳回碼。  
  
 在以輪詢為基礎的非同步處理模式中， **SQLCompleteAsync** 是呼叫原始非同步函式的替代方法，不需要在原始非同步函式呼叫中指定引數。 不論是否啟用 ODBC 資料指標程式庫，都可以使用**SQLCompleteAsync** 。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 輸出要在其上完成非同步處理的控制碼類型。 有效的值為 SQL_HANDLE_DBC 或 SQL_HANDLE_STMT。  
  
 *Handle*  
 輸出要在其上完成非同步處理的控制碼。 如果 *控制碼* 不是 *HandleType*所指定之類型的有效控制碼， **SQLCompleteAsync** 會傳回 SQL_INVALID_HANDLE。  
  
 如果 *控制碼* 不是 *HandleType*所指定之類型的有效控制碼， **SQLCompleteAsync** 會傳回 SQL_INVALID_HANDLE。  
  
 *AsyncRetCodePtr*  
 出將包含非同步 API 傳回碼的緩衝區指標。 如果 *AsyncRetCodePtr* 為 Null，則 **SQLCompleteAsync** 會傳回 SQL_ERROR。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_ERROR、SQL_NO_DATA 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 如果 **SQLCompleteAsync** 傳回 SQL_SUCCESS，應用程式應該從 *AsyncRetCodePtr*所指向的緩衝區取得非同步函式的傳回碼。 如果有關聯的 SQLSTATE （如果有的話），可以藉 **由呼叫具有** SQL_HANDLE_STMT 的 *HandleType* 和語句控制碼，或 SQL_HANDLE_DBC 和連接控制碼的 *HandleType* ，來取得相關聯的。 這些診斷記錄會與非同步函式相關聯，而不是此 **SQLCompleteAsync** 函數。  
  
 **SQLCompleteAsync** 會傳回 SQL_SUCCESS 以外的程式碼，表示未正確地呼叫 **SQLCompleteAsync** 。 在此情況下， **SQLCompleteAsync**不會張貼任何診斷記錄。 可能的傳回碼為：  
  
-   SQL_INVALID_HANDLE： *HandleType* 和 *Handle* 所指出的控制碼不是有效的控制碼。  
  
-   SQL_ERROR： *AsyncRetCodePtr* 為 Null，或控制碼上未啟用非同步處理。  
  
-   SQL_NO_DATA：在通知模式中，非同步作業正在進行中，或驅動程式管理員尚未通知應用程式。 在輪詢模式中，非同步作業不在進行中。  
  
## <a name="comments"></a>註解  
 在以輪詢為基礎的非同步處理模式中， *AsyncRetCodePtr* 可能會在 **SQLCompleteAsync** 傳回 SQL_SUCCESS 時 SQL_STILL_EXECUTING。 應用程式應該持續輪詢，直到不 SQL_STILL_EXECUTING *AsyncRetCodePtr* 為止。 在以通知為基礎的非同步處理模式中， *AsyncRetCodePtr* 永遠不會 SQL_STILL_EXECUTING。  
  
## <a name="see-also"></a>另請參閱  
 [非同步執行 (輪詢方法) ](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
