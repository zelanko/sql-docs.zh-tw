---
title: 非同步函式完成的通知 |Microsoft 文件
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
ms.topic: conceptual
ms.assetid: 336565da-4203-4745-bce2-4f011c08e357
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f9ef152274bd9ceea650ebd3c74f97c51c18500c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="notification-of-asynchronous-function-completion"></a>非同步函式完成的通知
在 Windows 8 SDK 中，ODBC 會加入非同步作業完成時，我們將為 「 通知完成 」 的通知應用程式的機制。 (請參閱[非同步執行 （通知方法）](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)如需詳細資訊。)本主題會討論的一些問題的驅動程式開發人員。  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>驅動程式管理員與驅動程式之間的介面  
 驅動程式管理員在內部提供的回呼函式[SQLAsyncNotificationCallback 函式](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md)。 **SQLAsyncNotificationCallback**只能呼叫驅動程式-應用程式無法直接呼叫它。 驅動程式呼叫**SQLAsyncNotificationCallback**每當新的資料從伺服器接收到最後一個傳回 SQL_STILL_EXECUTING 之後。  
  
 驅動程式管理員會提供回呼機制，因此在對應的函式傳回 SQL_STILL_EXECUTING 後執行非同步作業進行某個進度時，驅動程式可以通知驅動程式管理員  
  
 驅動程式管理員 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 將屬性設定為非 NULL 函式指標，其中的型別 SQL_ASYNC_NOTIFICATION_CALLBACK，以通知模式的運作的驅動程式與驅動程式連接控制代碼上任何非同步上該控制代碼的作業。 同樣地，驅動程式管理員會設定 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 屬性上具有非 NULL 函式指標，這也是型別 SQL_ASYNC_NOTIFICATION_CALLBACK，以通知模式的運作的驅動程式的驅動程式陳述式控制代碼該控制代碼上任何非同步作業。  
  
 如果驅動程式的控制代碼上執行非同步作業，則非同步驅動程式函式應該用於非封鎖的樣式。 如果無法立即完成此作業，則驅動程式函式應傳回 SQL_STILL_EXECUTING。 此需求適用於輪詢模式和通知模式。  
  
 如果控制代碼為通知的非同步模式，驅動程式必須呼叫通知回撥函式的位址是 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 或 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 屬性的值，一次之後傳回 SQL_STILL_EXECUTING。 也就是說，一個傳回 SQL_STILL_EXECUTING 必須搭配通知的回呼函式的單一引動過程。 驅動程式應該呼叫後函式參數值中使用 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT 或 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT 的控制代碼屬性的目前值*pContext*。  
  
 驅動程式必須回呼中呼叫的驅動程式函式; 執行緒沒有理由函式傳回前通知進度。 驅動程式應該使用自己的執行緒回呼。 驅動程式管理員不會使用驅動程式的回呼執行緒來執行廣泛的處理邏輯。  
  
 驅動程式管理員將驅動程式會呼叫傳回之後，再次呼叫原始函式。 驅動程式管理員可以使用應用程式執行緒都在驅動程式執行緒的執行緒。 如果驅動程式會使用一些執行緒 （例如，安全性權杖或使用者識別碼） 與相關聯的資訊，驅動程式應將所需的資訊儲存在初始的非同步呼叫，並使用整個非同步作業之前儲存的值完成。 通常，只有**SQLDriverConnect**， **SQLConnect**，或**SQLBrowseConnect**需要使用該種類的資訊。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
