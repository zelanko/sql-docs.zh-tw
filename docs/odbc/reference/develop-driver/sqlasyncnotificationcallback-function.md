---
title: SQLAsyncNotificationCallback 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c56aedc9-f7f7-4641-b605-f0f98ed4400c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 96073b8d5e68d10caaff268aae4c5af60554ef76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915547"
---
# <a name="sqlasyncnotificationcallback-function"></a>SQLAsyncNotificationCallback 函式
**合規性**  
 導入的版本：ODBC 3.8  
  
 標準的合規性：None  
  
 **摘要**  
 **SQLAsyncNotificationCallback**可讓驅動程式管理員時驅動程式傳回 SQL_STILL_EXECUTING 之後會有一些進度，目前的非同步作業呼叫的驅動程式。 **SQLAsyncNotificationCallback**只能由驅動程式呼叫。  
  
 驅動程式不會呼叫**SQLAsyncNotificationCallback**函式名稱**SQLAsyncNotificationCallback**。 相反地，驅動程式管理員傳遞至驅動程式做為對應的連接控制代碼或陳述式控制代碼，SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 或 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 屬性的值的函式指標分別。 不同的控制代碼可能會指派不同的函式指標值。 函式指標的型別定義為 SQL_ASYNC_NOTIFICATION_CALLBACK。  
  
 **SQLAsyncNotificationCallback**是安全執行緒。 驅動程式可以選擇使用多個呼叫的執行緒**SQLAsyncNotificationCallback**上不同處理同時。  
  
## <a name="syntax"></a>語法  
  
```  
typedef SQLRETURN (SQL_API *SQL_ASYNC_NOTIFICATION_CALLBACK)(  
   SQLPOINTER pContex,   
   BOOL fLast);  
```  
  
## <a name="arguments"></a>引數  
 *pContex*  
 驅動程式管理員所定義的資料結構的指標。 透過 SQLSetConnectAttr(SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT) 或 SQLSetStmtAttr(SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT) 驅動程式傳遞的值。  驅動程式沒有存取的值。  
  
 *fLast*  
 用來表示這個回呼函式引動過程是目前的非同步作業的最後一個驅動程式。 驅動程式管理員會再次呼叫此函式時，驅動程式會傳回 SQL_STILL_EXECUTING 以外的傳回碼。 驅動程式管理員可以使用這項資訊，例如，通知應用程式在事先才會完成非同步作業。  
  
 如果*處理*不是有效的控制代碼所指定型別的*HandleType*， **SQLCancelHandle**傳回 SQL_INVALID_HANDLE。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS 或 SQL_ERROR。  
  
## <a name="diagnostics"></a>診斷  
 **SQLAsyncNotificationCallback**可以傳回 SQL_ERROR，如下列兩種情況下 （這些資訊表示驅動程式或驅動程式管理員中的實作問題。  
  
|錯誤|描述|  
|-----------|-----------------|  
|連接或陳述式並未要求通知。||  
|無效*處理*|驅動程式傳入無效的控制代碼，而無法內部的驅動程式管理員驗證測試。|  
  
## <a name="see-also"></a>另請參閱  
 [非同步執行 (輪詢方法)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
