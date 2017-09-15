---
title: "撰寫 ODBC 3.x 應用程式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application upgrades [ODBC], about upgrading
- ODBC drivers [ODBC], backward compatibility
- upgrading applications [ODBC]
- compatibility [ODBC], upgrading applications
- application upgrades [ODBC]
- upgrading applications [ODBC], about upgrading
- backward compatibility [ODBC], upgrading applications
ms.assetid: 19c54fc5-9dd6-49b6-8c9f-a38961b40a65
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3941a679210a18b39ed201dd564b9613b48a2a58
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="writing-odbc-3x-applications"></a>撰寫 ODBC 3.x 應用程式
當 ODBC 2。*x*應用程式會升級到 ODBC 3。*x*，應該寫入，它會使用這兩個 ODBC 2。*x*和 3。*x*驅動程式。 應用程式應將條件式程式碼，以充分利用 ODBC 3。*x*功能。  
  
 SQL_ATTR_ODBC_VERSION 環境屬性應該設 SQL_OV_ODBC2。 這會確保此驅動程式的行為，ODBC 2 例如*.x*一節所述的變更的驅動程式[的行為變更](../../../odbc/reference/develop-app/behavioral-changes.md)。  
  
 如果應用程式會使用任何一節所述的功能[新功能](../../../odbc/reference/develop-app/new-features.md)，條件式程式碼應該用來判斷驅動程式是否為 ODBC 3。*x*或 ODBC 2*.x*驅動程式。 應用程式使用**SQLGetDiagField**和**SQLGetDiagRec**取得 ODBC 3。*x*進行錯誤處理這些條件的程式碼片段時的 Sqlstate。 應該考慮下列新功能的相關要點：  
  
-   資料列集大小行為的變更所影響的應用程式應該小心不要呼叫**SQLFetch**當陣列大小大於 1。 這些應用程式應該取代呼叫**SQLExtendedFetch**呼叫**SQLSetStmtAttr**設定 SQL_ATTR_ARRAY_STATUS_PTR 陳述式屬性，在**SQLFetchScroll**，使得它們具有適用於這兩個 ODBC 3 的通用程式碼。*x*和 ODBC 2。*x*驅動程式。 因為**SQLSetStmtAttr** SQL_ATTR_ROW_ARRAY_SIZE 與將對應至**SQLSetStmtAttr**與 ODBC 2 SQL_ROWSET_SIZE。*x*驅動程式，應用程式可以只將 SQL_ATTR_ROW_ARRAY_SIZE 設定為其多資料列提取作業。  
  
-   大部分的應用程式要升級不實際受到 SQLSTATE 程式碼中的變更。 會影響這些應用程式，它們可以機械搜尋並取代在大部分情況下，使用 「 SQLSTATE 對應 」 一節中的錯誤轉換資料表來轉換 ODBC 3。*x*錯誤碼 ODBC 2*.x*代碼。 因為 ODBC 3*.x*驅動程式管理員會執行對應的 ODBC 2。*x* ODBC 3 的 Sqlstate。*x* Sqlstate，這些應用程式寫入器需要只檢查針對 ODBC 3。*x* Sqlstate，而不必擔心包括 ODBC 2。*x*條件式程式碼中的 Sqlstate。  
  
-   如果應用程式會很棒的日期、 時間和時間戳記資料類型使用，應用程式可以宣告本身為 ODBC 2。*x*應用程式並使用其現有的程式碼而不是使用的條件與程式碼。  
  
 升級也應該包含下列步驟：  
  
-   呼叫**SQLSetEnvAttr**然後再配置設 SQL_OV_ODBC2 SQL_ATTR_ODBC_VERSION 環境屬性的連接。  
  
-   取代所有呼叫**SQLAllocEnv**， **SQLAllocConnect**，或**SQLAllocStmt**呼叫**SQLAllocHandle**適當*HandleType* SQL_HANDLE_ENV、 利用 SQL_HANDLE_DBC 或利用 SQL_HANDLE_STMT 的引數。  
  
-   取代所有呼叫**SQLFreeEnv**或**SQLFreeConnect**呼叫**SQLFreeHandle**適當*HandleType*引數利用 SQL_HANDLE_DBC 或 SQL_HANDLE_STMT。  
  
-   取代所有呼叫**SQLSetConnectOption**呼叫**SQLSetConnectAttr**。 如果將屬性設定其值為字串時，設定*StringLength*引數正確。 變更*屬性*至 SQL_ATTR_XXXX SQL_XXXX 引數。  
  
-   取代所有呼叫**SQLGetConnectOption**呼叫**SQLGetConnectAttr**。 取得字串或二進位屬性時，如果設定*Columnsize*至適當的值，並傳入*StringLength*引數。 變更*屬性*至 SQL_ATTR_XXXX SQL_XXXX 引數。  
  
-   取代所有呼叫**SQLSetStmtOption**呼叫**SQLSetStmtAttr**。 如果將屬性設定其值為字串時，設定*StringLength*引數正確。 變更*屬性*至 SQL_ATTR_XXXX SQL_XXXX 引數。  
  
-   取代所有呼叫**SQLGetStmtOption**呼叫**SQLGetStmtAttr**。 取得字串或二進位屬性時，如果設定*Columnsize*至適當的值，並傳入*StringLength*引數。 變更*屬性*至 SQL_ATTR_XXXX SQL_XXXX 引數。  
  
-   取代所有呼叫**SQLTransact**呼叫**SQLEndTran**。 如果在最右邊有效的控制代碼**SQLTransact**呼叫是環境控制代碼， *HandleType*利用 SQL_HANDLE_ENV 的引數應該用於**SQLEndTran**呼叫適當*處理*引數。 如果在最右邊有效的控制代碼您**SQLTransact**呼叫是在連接控制代碼， *HandleType*利用 SQL_HANDLE_DBC 的引數應該用於**SQLEndTran**呼叫適當*處理*引數。  
  
-   取代所有呼叫**SQLColAttributes**呼叫**SQLColAttribute**。 如果*FieldIdentifier*引數是 SQL_COLUMN_PRECISION、 SQL_COLUMN_SCALE 或 SQL_COLUMN_LENGTH，不會將函式的名稱以外的任何變更。 如果沒有，請變更*FieldIdentifier*從 SQL_DESC_XXXX 的 SQL_COLUMN_XXXX。 如果*FieldIdentifier* 、 SQL_DESC_CONCISE_TYPE，且資料類型是 datetime 資料類型變更為對應的 ODBC 3*.x*資料型別。  
  
-   如果使用區塊資料指標、 可捲動資料指標，或兩者，應用程式會執行下列動作：  
  
    -   設定資料列集大小、 資料指標類型，以及資料指標並行使用**SQLSetStmtAttr**。  
  
    -   呼叫**SQLSetStmtAttr**設定 sql_attr_row_status_ptr 設定為指向狀態記錄的陣列。  
  
    -   呼叫**SQLSetStmtAttr**設定為指向 SQLINTEGER SQL_ATTR_ROWS_FETCHED_PTR。  
  
    -   執行必要的繫結，並執行 SQL 陳述式。  
  
    -   呼叫**SQLFetchScroll**集中迴圈來提取資料列，並在結果中四處移動。  
  
    -   如果它要擷取的書籤，應用程式呼叫**SQLSetStmtAttr** SQL_ATTR_FETCH_BOOKMARK_PTR 設變數將包含的書籤的資料列，它想要擷取，以及呼叫**SQLFetchScroll**與*Sqlfetchscroll*要使用 sql_fetch_bookmark 的引數。  
  
-   使用參數陣列，如果應用程式會執行下列動作：  
  
    -   呼叫**SQLSetStmtAttr**將 SQL_ATTR_PARAMSET_SIZE 屬性為參數陣列的大小。  
  
    -   呼叫**SQLSetStmtAttr**設定為指向內部的 UDWORD 變數 SQL_ATTR_ROWS_PROCESSED_PTR。  
  
    -   會執行準備、 繫結，並執行適當作業。  
  
    -   如果基於某些原因 （例如 SQL_NEED_DATA) 停止執行，它可以尋找 「 目前 」 的資料列的參數，藉由檢查 SQL_ATTR_ROWS_PROCESSED_PTR 所指向的位置。  
  
 此章節包含下列主題。  
  
-   [取代函式對應的應用程式的回溯相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [呼叫 SQLCloseCursor](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [呼叫 SQLGetDiagField](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [呼叫 SQLSetPos](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [資料指標程式庫作業](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [對應的資料指標 Attributes1 資訊類型](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)
