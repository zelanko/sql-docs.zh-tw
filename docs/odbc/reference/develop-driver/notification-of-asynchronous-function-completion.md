---
title: 非同步函式完成的通知 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 336565da-4203-4745-bce2-4f011c08e357
author: MightyPen
ms.author: genemi
ms.openlocfilehash: de3496661f2ab329e5bf662a9cb8fa749cb81bfc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68129317"
---
# <a name="notification-of-asynchronous-function-completion"></a>非同步函式完成的通知
在 Windows 8 SDK 中，ODBC 新增了一種機制，可在非同步作業完成時通知應用程式，我們會將其稱為「完成時通知」。 （如需詳細資訊，請參閱[非同步執行（通知方法）](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md) ）。本主題討論驅動程式開發人員的一些問題。  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>驅動程式管理員和驅動程式之間的介面  
 驅動程式管理員在內部提供回呼函式[SQLAsyncNotificationCallback](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md)函式。 **SQLAsyncNotificationCallback**只能由驅動程式呼叫--應用程式無法直接呼叫它。 每當在最後一次傳回 SQL_STILL_EXECUTING 之後收到伺服器的新資料時，驅動程式就會呼叫**SQLAsyncNotificationCallback** 。  
  
 驅動程式管理員會提供回呼機制，讓驅動程式可以在對應的函式傳回之後執行非同步作業的某個進度時通知驅動程式管理員 SQL_STILL_EXECUTING  
  
 驅動程式管理員會使用非 Null 函式指標（屬於 SQL_ASYNC_NOTIFICATION_CALLBACK 類型）在驅動程式連接控制碼上設定 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 屬性，讓驅動程式在任何非同步通知模式下運作。該控制碼上的作業。 同樣地，驅動程式管理員會將驅動程式語句控制碼上的 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 屬性設定為非 Null 函式指標（也是 SQL_ASYNC_NOTIFICATION_CALLBACK 類型），以讓驅動程式在的通知模式下運作。該控制碼上的任何非同步作業。  
  
 如果非同步作業是在驅動程式控制碼上執行，非同步驅動程式函式應該會以非封鎖樣式運作。 如果作業無法立即完成，驅動程式函式應該會傳回 SQL_STILL_EXECUTING。 這項需求在輪詢模式和通知模式中都是如此。  
  
 如果控制碼處於通知非同步模式，則驅動程式必須呼叫通知回呼函式，其位址為 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 或 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 屬性的值，之後一次傳回 SQL_STILL_EXECUTING。 換句話說，傳回 SQL_STILL_EXECUTING 的一個必須與通知回呼函式的一個調用配對。 驅動程式應該使用 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT 或 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT handle 屬性的目前值，做為回撥函式參數*pCoNtext*的值。  
  
 驅動程式不能在呼叫驅動程式函式的執行緒中回呼。沒有理由在函式傳回之前通知進度。 驅動程式應該使用自己的執行緒來回呼。 驅動程式管理員不會使用驅動程式的回呼執行緒來執行大量處理邏輯。  
  
 驅動程式管理員會在驅動程式回呼之後再次呼叫原始的函式。 驅動程式管理員可能會使用既不是應用程式執行緒，也不是驅動程式執行緒的執行緒。 如果驅動程式使用與執行緒相關聯的某些資訊（例如，安全性權杖或使用者識別碼），則驅動程式應將所需的資訊儲存在初始非同步呼叫中，並在整個非同步作業之前使用儲存的值。後. 通常，只有**SQLDriverConnect**、 **SQLConnect**或**SQLBrowseConnect**需要使用該類型的資訊。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
