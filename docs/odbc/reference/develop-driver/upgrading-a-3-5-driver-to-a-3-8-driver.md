---
title: "升級至 3.8 驅動程式 3.5 驅動程式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ffba36ac-d22e-40b9-911a-973fa9e10bd3
caps.latest.revision: "27"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5dc39bf1203a06d571bf188e17e7066e53167415
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>升級至 3.8 驅動程式 3.5 驅動程式
本主題提供指導方針和 ODBC 3.5 驅動程式升級到 ODBC 3.8 驅動程式的考量。  
  
##### <a name="version-numbers"></a>版本號碼  
 下列指導方針與相關的版本號碼：  
  
-   驅動程式應該支援 SQL_OV_ODBC3_80 SQL_ATTR_ODBC_VERSION，SQL_OV_ODBC2、 sql_ov_odbc3 時和 SQL_OV_ODBC3_80 以外的值傳回 SQL_ERROR。 未來版本的驅動程式管理員會假設驅動程式支援 ODBC 相容性層級，如果驅動程式傳回 SQL_SUCCESS 從[SQLSetEnvAttr 函數](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。  
  
-   3.8 版的驅動程式應該會傳回從 03.80 **SQLGetInfo** SQL_DRIVER_ODBC_VER 會傳遞至*資訊類型*。 不過，較舊的驅動程式管理員，已包含在較舊版本的 Microsoft Windows 中，會視為 3.5 版驅動程式的驅動程式，並發出警告。  
  
     在 Windows 7 中的驅動程式管理員版本會是 03.80。 Windows 8 中的驅動程式管理員版本是透過 SQLGetInfo SQL_DM_VER 03.81 (*資訊類型*參數)。 SQL_ODBC_VER 會報告為 Windows 7 和 Windows 8 中 03.80 的版本。  
  
##### <a name="driver-specific-c-data-types"></a>驅動程式特有的 C 資料類型  
 驅動程式可以有自訂的 C 資料類型時 ﹐ 與 3.8 版的 ODBC 應用程式。 (如需詳細資訊，請參閱[ODBC 中的 C 資料類型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。)不過，沒有實作任何特定驅動程式的 C 類型 3.8 驅動程式的需求。 驅動程式仍應執行的 C 類型; 範圍檢查，但驅動程式管理員將不會執行，3.8 驅動程式。 若要協助驅動程式開發，驅動程式特定，C 資料類型的值可以定義格式如下：  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>驅動程式特定資料類型、 描述元類型、 資訊類型、 診斷的型別和屬性  
 在開發新的驅動程式時，您應該使用驅動程式專屬範圍資料類型，描述元類型、 資訊類型、 診斷的型別和屬性。 在討論驅動程式特定的範圍和其基底型別值[驅動程式特定資料類型，描述元類型、 資訊類型、 診斷的型別，以及屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
##### <a name="connection-pooling"></a>連接共用  
 更有效管理連接共用，ODBC 3.8 導入了 SQL_ATTR_RESET_CONNECTION 連接屬性中的**SQLSetConnectAttr**。 SQL_RESET_CONNECTION_YES 是唯一有效的值，這個屬性。 驅動程式管理員置於連接的連接集區，讓驅動程式才能重設預設值的其他連接屬性之前，將會設定 SQL_ATTR_RESET_CONNECTION。  
  
 若要避免不必要與伺服器通訊，驅動程式可以延後從集區重複使用連接後，直到下一步的通訊與遠端伺服器中，重設連接屬性。  
  
 請注意 SQL_ATTR_RESET_CONNECTION 僅用於驅動程式管理員與驅動程式之間的通訊。 應用程式無法直接將此屬性。 3.8 版的所有驅動程式應該實作此連接屬性。  
  
##### <a name="streamed-output-parameters"></a>資料流的輸出參數  
 ODBC 3.8 版導入資料流的輸出參數，更容易擴充的方式，擷取輸出參數。 (如需詳細資訊，請參閱[使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。)若要支援這項功能，驅動程式應該 SQL_GD_OUTPUT_PARAMS 傳回值中時設定 SQL_GETDATA_EXTENSIONS*資訊類型*中**SQLGetInfo**呼叫。 支援資料流的輸出參數的 SQL 類型必須實作驅動程式中。 驅動程式管理員不會產生錯誤。 無效的 SQL 型別。 支援資料流的輸出參數的 SQL 類型被定義在驅動程式。  
  
 如果應用程式使用驅動程式應傳回 SQL_ERROR **SQLGetData**擷取參數不是所傳回的參數相同**SQLParamData**。  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a>針對連接作業 （輪詢方法） 的非同步執行  
 驅動程式可啟用各種連線作業的非同步支援。  
  
 從 Windows 7 中，ODBC 支援輪詢方法 (如需詳細資訊，請參閱[非同步執行 （輪詢方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)。 沒有 3.8 版的 ODBC 驅動程式，實作連接控制代碼上的非同步作業的需求。 即使驅動程式不會實作非同步作業，在連接控制代碼，驅動程式仍應實作 SQL_ASYNC_DBC_FUNCTIONS*資訊類型*並傳回**SQL_ASYNC_DBC_NOT_CAPABLE**。  
  
 當啟用非同步連接作業時，連接作業的執行時間會是所有的重複呼叫的總時間。 如果最後一個重複呼叫發生後的總時間已超過 SQL_ATTR_CONNECTION_TIMEOUT 連接屬性所設定的值，但作業尚未完成，驅動程式會傳回 SQL_ERROR，並使用 SQLState HYT01 記錄的診斷記錄，「 連線逾時已過期 」 的訊息。 如果作業完成，就不會逾時。  
  
##### <a name="sqlcancelhandle-function"></a>SQLCancelHandle 函式  
 支援 ODBC 3.8 [SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)，用來取消連接和陳述式的作業。 支援的驅動程式**SQLCancelHandle**必須匯出函式。 驅動程式應該不會取消正在進行中，如果應用程式會呼叫任何同步或非同步連線函式**SQLCancel**或**SQLCancelHandle**陳述式控制代碼上。 同樣地，驅動程式應該不會取消正在進行中，如果應用程式呼叫任何同步或非同步的陳述式函數**SQLCancelHandle**連接控制代碼上。 此外，驅動程式應該不會取消瀏覽的作業 (**SQLBrowseConnect**傳回 SQL_NEED_DATA) 如果在應用程式呼叫**SQLCancelHandle**連接控制代碼上。 在這些情況下，驅動程式應該會傳回 HY010，「 函數順序錯誤 」。  
  
 不需要同時支援**SQLCancelHandle**和非同步連線作業一次。 驅動程式可以支援非同步連接作業，但不是**SQLCancelHandle**，反之亦然。  
  
##### <a name="suspended-connections"></a>暫止的連接  
 ODBC 3.8 驅動程式管理員可以進入暫停狀態的連接。 應用程式會呼叫**SQLDisconnect**釋放與連接相關聯的資源。 在此情況下，驅動程式應該嘗試釋放資源數量越好，而沒有檢查連接狀態。 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
##### <a name="driver-aware-connection-pooling"></a>可感知驅動程式的連接共用  
 Windows 8 中的 ODBC 允許來自訂連接集區行為的驅動程式。 如需詳細資訊，請參閱[感知驅動程式的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。  
  
##### <a name="asynchronous-execution-notification-method"></a>非同步執行 (通知方法)  
 ODBC 3.8 支援非同步作業，開始在 Windows 8 上提供的通知方法。 如需詳細資訊，請參閱[非同步執行 （通知方法）](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft 提供的 ODBC 驅動程式](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [ODBC 3.8 的新功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
