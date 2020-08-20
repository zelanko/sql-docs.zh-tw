---
description: 將 3.5 驅動程式升級至 3.8 驅動程式
title: 將3.5 驅動程式升級至3.8 驅動程式 |Microsoft Docs
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
ms.openlocfilehash: ac140c92b4042df1b4754d3a56237a6aa4b3afaf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461330"
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>將 3.5 驅動程式升級至 3.8 驅動程式
本主題提供將 ODBC 3.5 驅動程式升級至 ODBC 3.8 驅動程式的指導方針和考慮。  
  
##### <a name="version-numbers"></a>版本號碼  
 下列指導方針與版本號碼相關：  
  
-   驅動程式應該支援 SQL_ATTR_ODBC_VERSION 的 SQL_OV_ODBC3_80，傳回 SQL_OV_ODBC2、SQL_OV_ODBC3 和 SQL_OV_ODBC3_80 以外的值 SQL_ERROR。 如果驅動程式從 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)函式傳回 SQL_SUCCESS，驅動程式管理員的未來版本將會假設驅動程式支援 ODBC 相容性層級。  
  
-   當 SQL_DRIVER_ODBC_VER 傳遞給*InfoType*時，3.8 版驅動程式應該會從**SQLGetInfo**傳回03.80。 但是舊版的驅動程式管理員（隨附于舊版的 Microsoft Windows）會將該驅動程式視為3.5 版驅動程式，併發出警告。  
  
     在 Windows 7 中，驅動程式管理員的版本是03.80。 在 Windows 8 中，驅動程式管理員版本是03.81 透過 SQLGetInfo SQL_DM_VER (*InfoType* 參數) 。 SQL_ODBC_VER 在 Windows 7 和 Windows 8 中報告版本為03.80。  
  
##### <a name="driver-specific-c-data-types"></a>驅動程式特定的 C 資料類型  
 當驅動程式與3.8 版 ODBC 應用程式搭配使用時，可以有自訂的 C 資料類型。  (需詳細資訊，請參閱 [ODBC 中的 C 資料類型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。 ) 不過，3.8 驅動程式不需要執行任何驅動程式專屬的 C 類型。 但驅動程式仍應執行 C 類型的範圍檢查;驅動程式管理員不會針對3.8 驅動程式進行此作業。 為了加速驅動程式開發，您可以用下列格式來定義驅動程式特定的 C 資料類型值：  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>驅動程式特定的資料類型、描述項類型、資訊類型、診斷類型與屬性  
 開發新的驅動程式時，您應該針對資料類型、描述項類型、資訊類型、診斷類型和屬性使用驅動程式特定的範圍。 驅動程式特定的範圍及其基底類型值會在 [驅動程式專屬的資料類型、描述項類型、資訊類型、診斷類型與屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)中討論。  
  
##### <a name="connection-pooling"></a>連接共用  
 為了更妥善管理連接共用，ODBC 3.8 在 **SQLSetConnectAttr**中引進了 SQL_ATTR_RESET_CONNECTION 的連接屬性。 SQL_RESET_CONNECTION_YES 是此屬性唯一有效的值。 SQL_ATTR_RESET_CONNECTION 將會在驅動程式管理員將連接放置於連接集區之前設定，讓驅動程式將其他連接屬性重設為預設值。  
  
 為了避免與伺服器進行不必要的通訊，在從集區重複使用連接之後，驅動程式可以延遲連接屬性重設，直到下次與遠端伺服器通訊為止。  
  
 請注意，SQL_ATTR_RESET_CONNECTION 只用于驅動程式管理員與驅動程式之間的通訊。 應用程式無法直接設定這個屬性。 所有版本3.8 驅動程式都應該執行此連接屬性。  
  
##### <a name="streamed-output-parameters"></a>資料流程輸出參數  
 ODBC 3.8 版導入了串流的輸出參數，這是一種更可調整的方式來抓取輸出參數。  (需詳細資訊，請參閱[使用 SQLGetData 來取得輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。 ) 若要支援這項功能，當 SQL_GETDATA_EXTENSIONS 是**SQLGetInfo**呼叫中的*InfoType*時，驅動程式應該在傳回值中設定 SQL_GD_OUTPUT_PARAMS。 具有資料流程輸出參數的 SQL 類型支援必須在驅動程式中執行。 驅動程式管理員不會針對不正確 SQL 類型產生錯誤。 支援資料流程輸出參數的 SQL 類型是在驅動程式中定義。  
  
 如果應用程式使用 **SQLGetData** 來捕獲的參數與 **SQLParamData**所傳回的參數不同，則驅動程式應該會傳回 SQL_ERROR。  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a> (輪詢方法的連接作業的非同步執行)   
 驅動程式可以針對各種連接作業啟用非同步支援。  
  
 從 Windows 7 開始，ODBC 支援輪詢方法 (如需詳細資訊，請參閱 [非同步執行 (輪詢方法) ](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)。 版本 3.8 ODBC 驅動程式不需要在連接控制碼上執行非同步作業。 即使驅動程式未在連接控制碼上執行非同步作業，驅動程式仍應執行 SQL_ASYNC_DBC_FUNCTIONS *InfoType* ，並傳回 **SQL_ASYNC_DBC_NOT_CAPABLE**。  
  
 當非同步連接作業已啟用時，連接作業的執行時間就是所有重複呼叫的總時間。 如果最後一次重複呼叫發生于總時間超過 SQL_ATTR_CONNECTION_TIMEOUT 連接屬性所設定的值，而且作業尚未完成，則驅動程式會傳回 SQL_ERROR 並記錄具有 SQLState HYT01 的診斷記錄和「連接逾時已過期」訊息。 如果作業已完成，則不會有任何時間。  
  
##### <a name="sqlcancelhandle-function"></a>SQLCancelHandle 函式  
 ODBC 3.8 支援 [SQLCancelHandle 函數](../../../odbc/reference/syntax/sqlcancelhandle-function.md)，可用來取消連接和語句作業。 支援 **SQLCancelHandle** 的驅動程式必須匯出函數。 如果應用程式在語句控制碼上呼叫 **SQLCancel** 或 **SQLCancelHandle** ，驅動程式就不應該取消任何進行中的同步或非同步連接函數。 同樣地，如果應用程式在連接控制碼上呼叫 **SQLCancelHandle** ，驅動程式就不應該取消任何正在進行的同步或非同步語句函式。 此外，如果應用程式在連接控制碼上呼叫**SQLCancelHandle** ，驅動程式就不應該取消流覽作業 (**SQLBrowseConnect**會傳回 SQL_NEED_DATA) 。 在這些情況下，驅動程式應該會傳回 HY010 「函數順序錯誤」。  
  
 不需要同時支援 **SQLCancelHandle** 和非同步連接作業。 驅動程式可支援非同步連接作業，但無法 **SQLCancelHandle**，反之亦然。  
  
##### <a name="suspended-connections"></a>擱置的連接  
 ODBC 3.8 驅動程式管理員可以讓連線進入暫停狀態。 應用程式會呼叫 **SQLDisconnect** 來釋放與連接相關聯的資源。 在此情況下，驅動程式應該盡可能地釋放最多的資源，而不需要檢查連接的狀態。 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
##### <a name="driver-aware-connection-pooling"></a>可感知驅動程式的連接共用  
 Windows 8 中的 ODBC 可讓驅動程式自訂連接集區行為。 如需詳細資訊，請參閱 [驅動程式感知連接](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)共用。  
  
##### <a name="asynchronous-execution-notification-method"></a>非同步執行 (通知方法)  
 ODBC 3.8 支援非同步作業的通知方法（從 Windows 8 開始提供）。 如需詳細資訊，請參閱 [非同步執行 (通知方法) ](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft 提供的 ODBC 驅動程式](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [ODBC 3.8 的新功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
