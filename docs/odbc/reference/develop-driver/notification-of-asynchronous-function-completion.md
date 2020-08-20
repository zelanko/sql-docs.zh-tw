---
description: 非同步函式完成的通知
title: 非同步函式完成的通知 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 336565da-4203-4745-bce2-4f011c08e357
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d6e762e6b144e6a713f22429dccf43e1d27d8b24
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476257"
---
# <a name="notification-of-asynchronous-function-completion"></a>非同步函式完成的通知
在 Windows 8 SDK 中，ODBC 新增了一項機制，可在非同步作業完成時通知應用程式，我們會將其稱為「完成時通知」。 如需詳細資訊， (查看 [非同步執行 (通知方法) ](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md) 。 ) 本主題討論驅動程式開發人員的一些問題。  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>驅動程式管理員與驅動程式之間的介面  
 驅動程式管理員會在內部提供回呼函數 [SQLAsyncNotificationCallback](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md)函式。 **SQLAsyncNotificationCallback** 只能由驅動程式呼叫--應用程式無法直接呼叫它。 當最後一次傳回 SQL_STILL_EXECUTING，驅動程式會在每次從伺服器收到新資料時呼叫 **SQLAsyncNotificationCallback** 。  
  
 驅動程式管理員提供回呼機制，因此驅動程式可以在對應的函式傳回之後，執行非同步作業的某些進度發出通知驅動程式管理員 SQL_STILL_EXECUTING  
  
 驅動程式管理員會在驅動程式連接控制碼上設定 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 屬性，其具有非 Null 的函式指標（類型為 SQL_ASYNC_NOTIFICATION_CALLBACK），以便驅動程式在該控制碼上的任何非同步作業都能以通知模式運作。 同樣地，驅動程式管理員會使用非 Null 的函式指標（也是 SQL_ASYNC_NOTIFICATION_CALLBACK 類型）來設定驅動程式語句控制碼上的 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 屬性，以便驅動程式在該控制碼上的任何非同步作業都能以通知模式運作。  
  
 如果在驅動程式控制碼上執行非同步作業，非同步驅動程式函式應該會以非封鎖的樣式來運作。 如果作業無法立即完成，驅動程式函數應該會傳回 SQL_STILL_EXECUTING。 這項需求對於輪詢模式和通知模式都是如此。  
  
 如果控制碼在通知非同步模式中，則驅動程式必須呼叫通知回呼函式，其位址是 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 或 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 屬性的值，然後在傳回 SQL_STILL_EXECUTING 之後。 換句話說，一個傳回 SQL_STILL_EXECUTING 必須與通知回呼函式的一個調用配對。 驅動程式應該使用 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT 或 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT handle 屬性的目前值做為回呼函數參數 *pCoNtext*的值。  
  
 驅動程式絕不能在呼叫驅動程式函式的執行緒中回呼;沒有理由在函式傳回之前通知進度。 驅動程式應該使用自己的執行緒回呼。 驅動程式管理員不會使用驅動程式的回呼執行緒來執行廣泛的處理邏輯。  
  
 驅動程式管理員會在驅動程式回呼之後，再次呼叫原始函式。 驅動程式管理員可以使用不是應用程式執行緒或驅動程式執行緒的執行緒。 如果驅動程式使用與執行緒相關聯的某些資訊 (例如，安全性權杖或使用者識別碼) ，驅動程式應該將必要的資訊儲存在初始非同步呼叫中，並在整個非同步作業完成之前，使用儲存的值。 通常，只有 **SQLDriverConnect**、 **SQLConnect**或 **SQLBrowseConnect** 需要使用這類資訊。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
