---
title: 將 3.5 驅動程式升級到 3.8 驅動程式 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ffba36ac-d22e-40b9-911a-973fa9e10bd3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dcd01d050e806b733d75c54058945d367a33d6a7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294429"
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>將 3.5 驅動程式升級至 3.8 驅動程式
本主題提供了將 ODBC 3.5 驅動程式升級到 ODBC 3.8 驅動程式的指南和注意事項。  
  
##### <a name="version-numbers"></a>版本號碼  
 以下準則涉及版本號:  
  
-   驅動程式應支援SQL_ATTR_ODBC_VERSIONSQL_OV_ODBC3_80,返回SQL_ERRORSQL_OV_ODBC2、SQL_OV_ODBC3和SQL_OV_ODBC3_80以外的值。 如果驅動程式從[SQLSetEnv Attr 函數](../../../odbc/reference/syntax/sqlsetenvattr-function.md)傳回SQL_SUCCESS,則驅動程式管理器的未來版本將假定驅動程式支援 ODBC 合規性級別。  
  
-   版本 3.8 驅動程式應傳回 03.80 從**SQLGetInfo**時SQL_DRIVER_ODBC_VER傳遞到*InfoType*。 但是,舊版本的 Microsoft Windows 中包括的舊驅動程式管理器會將驅動程式視為版本 3.5 驅動程式,併發出警告。  
  
     在 Windows 7 中,驅動程式管理器版本為 03.80。 在 Windows 8 中,驅動程式管理器版本透過 SQLGetInfo SQL_DM_VER(*資訊類型*參數)為 03.81。 SQL_ODBC_VER在 Windows 7 和 Windows 8 中報告版本為 03.80。  
  
##### <a name="driver-specific-c-data-types"></a>特定於驅動程式的 C 資料型態  
 當驅動程式適用於版本 3.8 ODBC 應用程式時,它可以具有自定義的 C 數據類型。 (關於詳細資訊,請參考[ODBC 中的 C 資料型態](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。但是,不需要 3.8 驅動程式實現任何特定於驅動程式的 C 類型。 但是,驅動程式仍應執行 C 類型的範圍檢查;驅動程式管理員不會對 3.8 驅動程式執行此操作。 為了便於驅動程式開發,可以以以下格式定義特定於驅動程式的 C 資料類型的值:  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>特定於驅動程式的資料類型、描述符類型、資訊類型、診斷類型和屬性  
 在開發新驅動程式時,應對數據類型、描述符類型、資訊類型、診斷類型和屬性使用特定於驅動程式的範圍。 特定於驅動程式的範圍及其基本類型值在[特定於驅動程序的數據類型、描述符類型、資訊類型、診斷類型和屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)中進行了討論。  
  
##### <a name="connection-pooling"></a>連接共用  
 為了更好地管理連接池,ODBC 3.8 引入了**SQLSetConnectAttr**中的SQL_ATTR_RESET_CONNECTION連接屬性。 SQL_RESET_CONNECTION_YES是此屬性的唯一有效值。 SQL_ATTR_RESET_CONNECTION將在驅動程式管理器將連接放入連接池之前進行設置,從而允許驅動程式將其他連接屬性重置為其預設值。  
  
 為了避免與伺服器進行不必要的通信,驅動程式可以將連接屬性重置推遲到從池中重用連接后與遠端伺服器的下一次通信。  
  
 請注意,SQL_ATTR_RESET_CONNECTION僅用於驅動程式管理器和驅動程序之間的通信。 應用程式不能直接設置此屬性。 所有版本3.8驅動程式都應實現此連接屬性。  
  
##### <a name="streamed-output-parameters"></a>串流輸出參數  
 ODBC 版本 3.8 引入了流式輸出參數,這是檢索輸出參數的一種更具可擴充性的方法。 (關於詳細資訊,請參考使用[SQLGetData 偵測參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。為了支援此功能,當SQL_GETDATA_EXTENSIONS是**SQLGetInfo**調用中的*InfoType*時,驅動程式應在返回值中設置SQL_GD_OUTPUT_PARAMS。 必須在驅動程式中實現對具有流式輸出參數的 SQL 類型的支援。 驅動程式管理員不會為無效的 SQL 類型生成錯誤。 支援流式輸出參數的 SQL 類型在驅動程式中定義。  
  
 如果應用程式使用**SQLGetData**檢索與**SQLParamData**傳回的參數不一樣的參數,則驅動程式應返回SQL_ERROR。  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a>連接操作的非同步執行(輪詢方法)  
 驅動程式可以為各種連接操作啟用非同步支援。  
  
 從 Windows 7 開始,ODBC 支援輪詢方法(有關詳細資訊,請參閱[異步執行(輪詢方法)。](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md) 不需要版本 3.8 ODBC 驅動程式對連接句柄實現非同步操作。 即使驅動程式未在連接句柄上實現非同步操作,驅動程式仍應實現SQL_ASYNC_DBC_FUNCTIONS *InfoType*並傳回**SQL_ASYNC_DBC_NOT_CAPABLE**。  
  
 啟用非同步連線操作後,連接操作的執行時間是所有重複調用的總時間。 如果上次重複調用發生在總時間超過SQL_ATTR_CONNECTION_TIMEOUT連接屬性設置的值之後,並且操作尚未完成,則驅動程式返回SQL_ERROR,並記錄 SQLState HYT01 和消息"連接超時已過期"。。 如果操作完成,則沒有超時。  
  
##### <a name="sqlcancelhandle-function"></a>SQLCancelHandle 函式  
 ODBC 3.8 支援[SQLCancelHandle 函數](../../../odbc/reference/syntax/sqlcancelhandle-function.md),用於取消連接和語句操作。 支援**SQLCancelHandle**的驅動程式必須匯出該函數。 如果應用程式在語句句柄上調用**SQLCancel**或**SQLCancelHandle,** 驅動程式不應取消正在進行的任何同步或異步連接功能。 同樣,如果應用程式在連接句柄上調用**SQLCancelHandle,** 驅動程式不應取消正在進行的任何同步或異步語句函數。 此外,如果應用程式在連接句柄上調用**SQLCancelHandle,** 驅動程式不應取消流覽操作 **(SQLBrowse Connect**返回SQL_NEED_DATA)。 在這些情況下,驅動程式應返回 HY010,"功能序列錯誤」。  
  
 不必同時支援**SQLCancelHandle**和非同步連接操作。 驅動程式可以支援非同步連接操作,但不能支援**SQLCancelHandle,** 反之亦然。  
  
##### <a name="suspended-connections"></a>暫停連線  
 ODBC 3.8 驅動程式管理員可以將連接置於掛起狀態。 應用程式將調用**SQLDisconnect**以釋放與連接關聯的資源。 在這種情況下,驅動程式應嘗試釋放盡可能多的資源,而不檢查連接的狀態。 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
##### <a name="driver-aware-connection-pooling"></a>可感知驅動程式的連接共用  
 Windows 8 中的 ODBC 允許驅動程式自定義連接池行為。 有關詳細資訊,請參閱[驅動程式感知連接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。  
  
##### <a name="asynchronous-execution-notification-method"></a>非同步執行 (通知方法)  
 ODBC 3.8 支援非同步操作的通知方法,可在Windows 8上開始。 有關詳細資訊,請參閱[非同步執行(通知方法)。](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [微軟提供的ODBC驅動程式](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [ODBC 3.8 的新功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
