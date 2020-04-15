---
title: SQLCompleteasync 函數 |微軟文件
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
ms.openlocfilehash: 4e09d61ef516e846798dd3af2d07dafa78af4605
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299653"
---
# <a name="sqlcompleteasync-function"></a>SQLCompleteAsync 函式
**一致性**  
 版本介紹: ODBC 3.8  
  
 標準合規性:無  
  
 **摘要**  
 **SQLCompleteAsync**可用於使用基於通知或輪詢的處理確定非同步函數何時完成。 有關同步操作的詳細資訊,請參閱[非同步執行](../../../odbc/reference/develop-app/asynchronous-execution.md)。  
  
 **SQLCompleteAsync**僅在 ODBC 驅動程式管理器中實現。  
  
 在基於通知的非同步處理模式下,必須在驅動程式管理器引發用於通知的事件物件後呼叫**SQLCompleteAsync。** **SQLCompleteAsync**完成非同步處理,非同步函數將生成返回代碼。  
  
 在基於輪詢的非同步處理模式下 **,SQLCompleteAsync**是調用原始非同步函數的替代方法,無需在原始異步函數調用中指定參數。 無論是否啟用了 ODBC 游標庫,都可以使用**SQLCompleteAsync。**  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 [輸入]要完成非同步處理的句柄的類型。 有效值SQL_HANDLE_DBC或SQL_HANDLE_STMT。  
  
 *Handle*  
 [輸入]要完成非同步處理的句柄。 如果*句柄*不是*HandleType*指定的類型的有效句柄,**則 SQLCompleteAsync**將返回SQL_INVALID_HANDLE。  
  
 如果*句柄*不是*HandleType*指定的類型的有效句柄,**則 SQLCompleteAsync**將返回SQL_INVALID_HANDLE。  
  
 *非同步再編碼器*  
 【輸出]指向將包含非同步 API 返回代碼的緩衝區的指標。 如果*非同步編碼器*為 NULL,**則 SQLCompleteAsync**返回SQL_ERROR。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_ERROR、SQL_NO_DATA 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 如果**SQLCompleteAsync**返回SQL_SUCCESS,則應用程式應從*AsyncRetCodeptr*指向的緩衝區獲取非同步函數的返回代碼。 關聯的 SQLSTATE(如果有)可以通過使用*SQL_HANDLE_STMT的句柄類型*、語句句柄或SQL_HANDLE_DBC的*句柄類型*和連接句柄調用**SQLGetDiagRec**來獲取。 這些診斷記錄與非同步函數相關聯,而不是此**SQLCompleteAsync**函數。  
  
 **SQLCompleteAsync**傳回SQL_SUCCESS以外的代碼,以指示未正確呼叫**SQLCompleteAsync。** **在這種情況下,SQLCompleteAsync**不會發佈任何診斷記錄。 可能的退貨碼包括:  
  
-   *SQL_INVALID_HANDLE:HandleType*和 Handle 指示的*句柄*不是有效的句柄。  
  
-   *SQL_ERROR:AsyncRetCodePtr*為 NULL,或者手柄上未啟用非同步處理。  
  
-   SQL_NO_DATA:在通知模式下,非同步操作未進行,或者驅動程式管理員未通知應用程式。 在輪詢模式下,非同步操作未進行。  
  
## <a name="comments"></a>註解  
 在基於輪詢的非同步處理模式下,當**SQLCompleteAsync**返回SQL_SUCCESS時,可能會SQL_STILL_EXECUTING *AsyncRetCodePtr。* 應用程式應保留輪詢,直到*asyncRetCodePtr*不SQL_STILL_EXECUTING。 在基於通知的非同步處理模式下 *,AsyncRetCodePtr*永遠不會SQL_STILL_EXECUTING。  
  
## <a name="see-also"></a>另請參閱  
 [非同步執行 (輪詢方法)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
