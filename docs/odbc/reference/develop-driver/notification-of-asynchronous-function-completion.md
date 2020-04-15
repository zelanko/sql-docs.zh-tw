---
title: 非同步功能完成通知 |微軟文件
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
ms.openlocfilehash: a453967f2ffdda4af2a44429737f700f4a994cf8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287818"
---
# <a name="notification-of-asynchronous-function-completion"></a>非同步函式完成的通知
在 Windows 8 SDK 中,ODBC 添加了一種機制,以便在非同步操作完成時通知應用程式,我們將將其稱為"完成通知」。 (有關詳細資訊,請參閱[非同步執行(通知方法)。](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)本主題討論驅動程式開發人員的一些問題。  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>驅動程式管理員和驅動程式之間的介面  
 驅動程式管理員內部提供回檔函數[SQLAsync 通知回檔函數](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md)。 **SQLAsync 通知回調**只能由驅動程式呼叫 - 應用程式不能直接呼叫它。 每當上次返回SQL_STILL_EXECUTING後從伺服器收到新數據時,驅動程序都會調用**SQLAsync 通知回撥。**  
  
 驅動程式管理員提供回調機制,這樣當相應的函數返回SQL_STILL_EXECUTING后,在執行非同步操作方面取得了一些進展時,驅動程式可以通知驅動程式管理器SQL_STILL_EXECUTING  
  
 驅動程式管理器使用非 NULL 函數指標在驅動程式連接句柄上設定SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK屬性,該指標的類型為SQL_ASYNC_NOTIFICATION_CALLBACK,以便驅動程式在該句柄上的任何異步操作在通知模式下工作。 同樣,Driver Manager 使用非 NULL 函數指標(也屬於SQL_ASYNC_NOTIFICATION_CALLBACK類型)在驅動程式語句句柄上設置SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK屬性,以便驅動程式在該句柄上的任何異步操作在通知模式下工作。  
  
 如果在驅動程式句柄上執行非同步操作,非同步驅動程式函數應以非阻塞樣式工作。 如果操作無法立即完成,則驅動程式功能應返回SQL_STILL_EXECUTING。 輪詢模式和通知模式都要求此要求為 true。  
  
 如果句柄處於通知異步模式,驅動程式必須在返回SQL_STILL_EXECUTING后調用通知回調函數,該函數的位址是SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK或SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK屬性的值。 換句話說,一個返回SQL_STILL_EXECUTING必須與通知回調函數的一個調用配對。 驅動程式應使用SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT的當前值或SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT句柄屬性作為回調函數參數*pContext*的值。  
  
 驅動程式不得在調用驅動程式函數的線程中回調;沒有理由在函數返回之前通知進度。 驅動程式應使用自己的線程進行回調。 驅動程式管理員不會使用驅動程序的回調線程執行廣泛的處理邏輯。  
  
 驅動程式管理器將在驅動程式回電后再次調用原始函數。 驅動程式管理員可以使用既不是應用程式線程也不是驅動程式線程的線程。 如果驅動程式使用與線程關聯的某些資訊(例如,安全令牌或用戶識別符),驅動程式應在初始異步調用中保存所需資訊,並在整個非同步操作完成之前使用保存的值。 通常,只有**SQLDriverConnect、SQLConnect**或**SQLBrowse Connect****SQLConnect**需要使用此類資訊。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
