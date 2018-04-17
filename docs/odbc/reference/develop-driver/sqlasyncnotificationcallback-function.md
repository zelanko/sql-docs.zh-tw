---
title: SQLAsyncNotificationCallback 函式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c56aedc9-f7f7-4641-b605-f0f98ed4400c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9acbede4cb76f529264fb0c6e9a888becd37660f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sqlasyncnotificationcallback-function"></a>SQLAsyncNotificationCallback 函式
**一致性**  
 版本引進了： ODBC 3.8  
  
 標準相容性： 無  
  
 **摘要**  
 **SQLAsyncNotificationCallback**允許驅動程式新增至驅動程式管理員在驅動程式會傳回 SQL_STILL_EXECUTING 後就某些進行目前的非同步作業時呼叫。 **SQLAsyncNotificationCallback**只能由驅動程式呼叫。  
  
 驅動程式不會呼叫**SQLAsyncNotificationCallback**函式名稱**SQLAsyncNotificationCallback**。 相反地，驅動程式管理員傳遞至驅動程式做為對應的連接控制代碼或陳述式控制代碼，SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 或 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 屬性的值的函式指標分別。 不同的控制代碼可能會指派不同的函式指標值。 函式指標的類型定義為 SQL_ASYNC_NOTIFICATION_CALLBACK。  
  
 **SQLAsyncNotificationCallback**是安全執行緒。 驅動程式可以選擇使用多個執行緒呼叫**SQLAsyncNotificationCallback**上不同處理同時。  
  
## <a name="syntax"></a>語法  
  
```  
typedef SQLRETURN (SQL_API *SQL_ASYNC_NOTIFICATION_CALLBACK)(  
   SQLPOINTER pContex,   
   BOOL fLast);  
```  
  
## <a name="arguments"></a>引數  
 *pContex*  
 驅動程式管理員所定義的資料結構的指標。 值會傳遞至驅動程式，透過 SQLSetConnectAttr(SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT) 或 SQLSetStmtAttr(SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT)。  驅動程式沒有存取的值。  
  
 *fLast*  
 用來表示這個回呼函式引動過程是目前的非同步作業的最後一個驅動程式。 驅動程式管理員一次呼叫函式時，驅動程式會傳回 SQL_STILL_EXECUTING 以外的傳回碼。 驅動程式管理員可以使用這項資訊，例如，以通知應用程式預先才會完成非同步作業。  
  
 如果*處理*不是有效的控制代碼所指定型別的*HandleType*， **SQLCancelHandle**傳回 SQL_INVALID_HANDLE。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS 或 SQL_ERROR。  
  
## <a name="diagnostics"></a>診斷  
 **SQLAsyncNotificationCallback**可以傳回 SQL_ERROR，如下列兩種情況下 （這些指示中的驅動程式或驅動程式管理員實作問題。  
  
|錯誤|Description|  
|-----------|-----------------|  
|連接或陳述式沒有要求通知。||  
|無效*處理*|驅動程式會傳入無效的控制代碼，失敗的內部驅動程式管理員驗證測試。|  
  
## <a name="see-also"></a>另請參閱  
 [非同步執行 (輪詢方法)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
