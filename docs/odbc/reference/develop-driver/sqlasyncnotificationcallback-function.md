---
description: SQLAsyncNotificationCallback 函式
title: SQLAsyncNotificationCallback 函式 |Microsoft Docs
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
ms.openlocfilehash: b9d03e8a3fa7e62c19dd09a210dca3a56348c692
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476227"
---
# <a name="sqlasyncnotificationcallback-function"></a>SQLAsyncNotificationCallback 函式
**一致性**  
 引進的版本： ODBC 3。8  
  
 標準合規性：無  
  
 **總結**  
 當目前的非同步作業在驅動程式傳回 SQL_STILL_EXECUTING 之後， **SQLAsyncNotificationCallback**可允許驅動程式回呼至驅動程式管理員。 **SQLAsyncNotificationCallback** 只能由驅動程式呼叫。  
  
 驅動程式不會以函數名稱**SQLAsyncNotificationCallback**呼叫**SQLAsyncNotificationCallback** 。 相反地，驅動程式管理員會將函式指標傳遞至驅動程式，做為對應之連接控制碼或語句控制碼的 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 或 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 屬性的值。 不同的控制碼可能會被指派不同的函式指標值。 函數指標的型別定義為 SQL_ASYNC_NOTIFICATION_CALLBACK。  
  
 **SQLAsyncNotificationCallback** 是安全線程。 驅動程式可以選擇使用多個執行緒，同時在不同的控制碼上呼叫 **SQLAsyncNotificationCallback** 。  
  
## <a name="syntax"></a>語法  
  
```  
typedef SQLRETURN (SQL_API *SQL_ASYNC_NOTIFICATION_CALLBACK)(  
   SQLPOINTER pContex,   
   BOOL fLast);  
```  
  
## <a name="arguments"></a>引數  
 *pContex*  
 驅動程式管理員所定義之資料結構的指標。 此值會透過 SQLSetConnectAttr (SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT) 或 SQLSetStmtAttr (SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT) 傳遞至驅動程式。  驅動程式沒有值的存取權。  
  
 *fLast*  
 驅動程式用來表示這個回呼函數調用是目前非同步作業的最後一個。 驅動程式管理員再次呼叫函式時，驅動程式會傳回 SQL_STILL_EXECUTING 以外的傳回碼。 例如，驅動程式管理員可以使用這項資訊來通知應用程式，非同步作業將會完成。  
  
 如果 *控制碼* 不是 *HandleType*所指定之類型的有效控制碼， **SQLCancelHandle** 會傳回 SQL_INVALID_HANDLE。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS 或 SQL_ERROR。  
  
## <a name="diagnostics"></a>診斷  
 **SQLAsyncNotificationCallback** 可能會在下列兩種情況下傳回 SQL_ERROR (這表示驅動程式或驅動程式管理員中的執行問題。  
  
|錯誤|描述|  
|-----------|-----------------|  
|連接或語句未要求通知。||  
|不正確 *控制碼*|驅動程式傳入了不正確控制碼，而導致內部驅動程式管理員驗證測試失敗。|  
  
## <a name="see-also"></a>另請參閱  
 [非同步執行 (輪詢方法) ](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
