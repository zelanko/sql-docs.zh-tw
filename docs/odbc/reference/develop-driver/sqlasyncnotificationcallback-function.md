---
title: SQLSync 通知回撥功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c56aedc9-f7f7-4641-b605-f0f98ed4400c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6c182c48b8e5ddb70204ddd3a94d9651f97595d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294535"
---
# <a name="sqlasyncnotificationcallback-function"></a>SQLAsyncNotificationCallback 函式
**一致性**  
 版本介紹: ODBC 3.8  
  
 標準合規性:無  
  
 **摘要**  
 **SQLAsync 通知回撥**允許驅動程式在驅動程式返回SQL_STILL_EXECUTING後當前非同步操作有一些進展時回調到驅動程式管理器。 **SQLAsync 通知回調**只能由驅動程式調用。  
  
 驅動程式不呼叫**SQLAsync 通知回**檔 ,功能名稱**SQLAsync 通知回檔**。 相反,驅動程式管理器將函數指標傳遞給驅動程式,作為相應連接句柄或語句句柄SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK或SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK屬性的值。 可以分配不同的句柄,以指示不同的函數指標值。 函數指標的類型定義為SQL_ASYNC_NOTIFICATION_CALLBACK。  
  
 **SQLSync 通知回調**是線程安全的。 驅動程式可以選擇在不同的句柄上同時使用調用**SQLAsync 通知回調**的多個線程。  
  
## <a name="syntax"></a>語法  
  
```  
typedef SQLRETURN (SQL_API *SQL_ASYNC_NOTIFICATION_CALLBACK)(  
   SQLPOINTER pContex,   
   BOOL fLast);  
```  
  
## <a name="arguments"></a>引數  
 *普康特克斯*  
 指向驅動程式管理員定義的數據結構的指標。 該值透過 SQLSetConnectAttr(SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT)或 SQLSetStmtAttr(SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT)傳遞給驅動程式。  驅動程式無法訪問該值。  
  
 *fLast*  
 驅動程式用於指示此回調函數調用是當前非同步操作的最後一個調用。 當驅動程式管理器再次調用該函數時,驅動程式將返回SQL_STILL_EXECUTING以外的返回代碼。 例如,驅動程式管理器可以使用此資訊提前通知應用程式非同步操作將完成。  
  
 如果*句柄*不是*HandleType*指定的類型的有效句柄 **,SQLCancelHandle**將返回SQL_INVALID_HANDLE。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS或SQL_ERROR。  
  
## <a name="diagnostics"></a>診斷  
 **SQLAsync 通知回撥**可以返回以下兩種情況SQL_ERROR(這些表示驅動程式或驅動程式管理器中的實現問題)。  
  
|錯誤|描述|  
|-----------|-----------------|  
|連接或語句未請求通知。||  
|句柄*無效*|驅動程式在無效的句柄中傳遞,這未通過內部驅動程式管理器驗證測試。|  
  
## <a name="see-also"></a>另請參閱  
 [非同步執行 (輪詢方法)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
