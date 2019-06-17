---
title: 將 3.5 驅動程式升級至 3.8 驅動程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ffba36ac-d22e-40b9-911a-973fa9e10bd3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: df2fa8df9af317bd76b2d7f10e50f7cc937e4660
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63254160"
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>將 3.5 驅動程式升級至 3.8 驅動程式
本主題提供指導方針與考量升級 ODBC 3.5 驅動程式符合 ODBC 3.8 驅動程式。  
  
##### <a name="version-numbers"></a>版本號碼  
 下列指導方針與相關的版本號碼：  
  
-   驅動程式應該支援 SQL_OV_ODBC3_80 SQL_ATTR_ODBC_VERSION，SQL_OV_ODBC2、 sql_ov_odbc3 時和 SQL_OV_ODBC3_80 以外的值傳回 SQL_ERROR。 未來版本的驅動程式管理員會假設驅動程式支援 ODBC 相容性層級，如果驅動程式傳回 SQL_SUCCESS，從[SQLSetEnvAttr 函式](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。  
  
-   3\.8 版的驅動程式應該會傳回從 03.80 **SQLGetInfo** SQL_DRIVER_ODBC_VER 時傳遞給*資訊類型*。 不過，較舊的驅動程式管理員，已包含在舊版的 Microsoft Windows 中，會視為 3.5 版驅動程式的驅動程式，並發出警告。  
  
     在 Windows 7 中，驅動程式管理員版本會為 03.80。 在 Windows 8 中，驅動程式管理員版本是透過 SQLGetInfo SQL_DM_VER 03.81 (*資訊類型*參數)。 SQL_ODBC_VER 會回報為 03.80 Windows 7 和 Windows 8 中的版本。  
  
##### <a name="driver-specific-c-data-types"></a>驅動程式特有的 C 資料類型  
 驅動程式可以有自訂的 C 資料類型時它會使用 3.8 版的 ODBC 應用程式。 (如需詳細資訊，請參閱 < [ODBC 中的 C 資料類型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。)不過，沒有 3.8 驅動程式來實作任何特定驅動程式的 C 類型的需求。 但驅動程式仍應執行的 C 類型; 範圍檢查驅動程式管理員不會做的 3.8 驅動程式。 若要協助驅動程式開發，驅動程式特定，C 資料類型的值可以定義格式如下：  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>驅動程式專屬資料型別、 描述項類型、 資訊類型、 診斷類型和屬性  
 在開發新的驅動程式時，您應該使用驅動程式特定範圍的資料型別、 描述項類型、 資訊類型、 診斷類型和屬性。 驅動程式專屬的範圍和其基底類型值會討論[驅動程式專屬資料型別、 描述項類型、 資訊類型、 診斷類型和屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
##### <a name="connection-pooling"></a>連接共用  
 更有效率地管理連接共用，如 ODBC 3.8 導入了 SQL_ATTR_RESET_CONNECTION 連接屬性中的**SQLSetConnectAttr**。 SQL_RESET_CONNECTION_YES 是唯一有效的值，這個屬性。 驅動程式管理員置於連接的連接集區中，讓驅動程式的其他連接屬性重設為預設值之前，將會設定 SQL_ATTR_RESET_CONNECTION。  
  
 若要避免不必要的通訊，與伺服器，驅動程式可以延後的下一步 通訊與遠端伺服器，直到重設之後重複使用連接集區中, 的 「 連接 」 屬性。  
  
 請注意 SQL_ATTR_RESET_CONNECTION 僅用於驅動程式管理員和驅動程式之間的通訊。 應用程式無法直接設定此屬性。 3\.8 版的所有驅動程式應該實作此連接屬性。  
  
##### <a name="streamed-output-parameters"></a>資料流的輸出參數  
 ODBC 3.8 版引進了資料流的輸出參數，更有彈性的方式，擷取輸出參數。 (如需詳細資訊，請參閱 <<c0> [ 使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。)若要支援這項功能，驅動程式應該 SQL_GD_OUTPUT_PARAMS 中傳回的值時設定 SQL_GETDATA_EXTENSIONS*資訊類型*中**SQLGetInfo**呼叫。 支援資料流的輸出參數的 SQL 類型必須實作驅動程式中。 驅動程式管理員不會產生無效的 SQL 類型的錯誤。 支援資料流的輸出參數的 SQL 類型被定義在驅動程式。  
  
 如果應用程式使用驅動程式應傳回 SQL_ERROR **SQLGetData**來擷取參數不是所傳回的參數相同**SQLParamData**。  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a>針對連接作業 （輪詢方法） 的非同步執行  
 驅動程式可啟用各種連線作業的非同步支援。  
  
 從 Windows 7 開始，ODBC 支援輪詢方法 (如需詳細資訊，請參閱 <<c0> [ 非同步執行 （輪詢的方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)。 沒有 3.8 版的 ODBC 驅動程式，實作在連接控制代碼上的非同步作業的需求。 即使驅動程式不會實作非同步作業，在連接控制代碼，驅動程式仍應實作 SQL_ASYNC_DBC_FUNCTIONS*資訊類型*，並傳回**SQL_ASYNC_DBC_NOT_CAPABLE**。  
  
 非同步連接作業啟用時，連接作業的執行時間會是所有的重複呼叫的總時間。 如果最後一個重複的總時間已超過 SQL_ATTR_CONNECTION_TIMEOUT 連接屬性所設定的值，但尚未完成作業之後，就會發生呼叫，驅動程式會傳回 SQL_ERROR，並使用 SQLState HYT01 記錄的診斷記錄和「 連線逾時已過期 」 的訊息。 如果作業完成，就不會逾時。  
  
##### <a name="sqlcancelhandle-function"></a>SQLCancelHandle 函式  
 支援 ODBC 3.8 [SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)，用來取消連接和陳述式的作業。 支援的驅動程式**SQLCancelHandle**必須匯出函式。 驅動程式應該不會取消正在進行中，如果應用程式呼叫任何同步或非同步連線函式**SQLCancel**或是**SQLCancelHandle**陳述式控制代碼。 同樣地，驅動程式應該不會取消正在進行中，如果應用程式呼叫任何同步或非同步的陳述式函式**SQLCancelHandle**連接控制代碼上。 此外，驅動程式應該取消瀏覽作業 (**SQLBrowseConnect**會傳回 SQL_NEED_DATA) 如果應用程式會呼叫**SQLCancelHandle**連接控制代碼上。 在這些情況下，驅動程式應傳回 HY010，「 函數順序錯誤 」。  
  
 您不需要同時支援**SQLCancelHandle**和非同步連接作業，在相同的時間。 驅動程式可支援非同步連接作業而非**SQLCancelHandle**，反之亦然。  
  
##### <a name="suspended-connections"></a>暫止的連線  
 ODBC 3.8 驅動程式管理員會讓連接處於暫停狀態。 應用程式會呼叫**SQLDisconnect**釋放與連接相關聯的資源。 在此情況下，驅動程式應該嘗試盡可能釋放許多資源，而不檢查連線狀態。 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
##### <a name="driver-aware-connection-pooling"></a>可感知驅動程式的連接共用  
 Windows 8 中的 ODBC 允許來自訂連接集區行為的驅動程式。 如需詳細資訊，請參閱 <<c0> [ 感知驅動程式的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。  
  
##### <a name="asynchronous-execution-notification-method"></a>非同步執行 (通知方法)  
 ODBC 3.8 支援非同步作業，從 Windows 8 上的通知方法。 如需詳細資訊，請參閱 <<c0> [ 非同步執行 （通知方法）](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft 提供的 ODBC 驅動程式](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [ODBC 3.8 的新功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
