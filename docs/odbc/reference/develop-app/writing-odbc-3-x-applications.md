---
title: 撰寫 ODBC 3.x 應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], about upgrading
- ODBC drivers [ODBC], backward compatibility
- upgrading applications [ODBC]
- compatibility [ODBC], upgrading applications
- application upgrades [ODBC]
- upgrading applications [ODBC], about upgrading
- backward compatibility [ODBC], upgrading applications
ms.assetid: 19c54fc5-9dd6-49b6-8c9f-a38961b40a65
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a51183964fe36d799e0e62243c6a0012da99727
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793279"
---
# <a name="writing-odbc-3x-applications"></a>撰寫 ODBC 3.x 應用程式
當 ODBC *2.x*應用程式會升級到 ODBC *3.x*，就應該撰寫，它會使用這兩個 ODBC *2.x*並*3.x*驅動程式. 應用程式應該納入條件式的程式碼，以充分利用 ODBC *3.x*功能。  
  
 SQL_ATTR_ODBC_VERSION 環境屬性應該設 SQL_OV_ODBC2。 這可確保，驅動程式的行為如 ODBC *2.x*一節所述的變更方面的驅動程式[行為變更](../../../odbc/reference/develop-app/behavioral-changes.md)。  
  
 如果應用程式會使用任何一節所述的功能[新功能](../../../odbc/reference/develop-app/new-features.md)，條件式的程式碼應該用來判斷驅動程式是否為 ODBC *3.x*或 ODBC *2.x*驅動程式。 應用程式會使用**SQLGetDiagField**並**SQLGetDiagRec**若要取得 ODBC *3.x*在執行這些條件程式碼片段上處理的錯誤時的 Sqlstate。 應該考慮下列各點有關的新功能：  
  
-   受影響的資料列集大小的行為變更的應用程式應該小心，不要呼叫**SQLFetch**當陣列大小大於 1。 這些應用程式應該呼叫，換成**SQLExtendedFetch**呼叫**SQLSetStmtAttr**若要設定 SQL_ATTR_ARRAY_STATUS_PTR 陳述式屬性以及**SQLFetchScroll**，好讓它們擁有可搭配 ODBC 使用的通用程式碼*3.x*和 ODBC *2.x*驅動程式。 因為**SQLSetStmtAttr** SQL_ATTR_ROW_ARRAY_SIZE 與將對應到**SQLSetStmtAttr**與 odbc SQL_ROWSET_SIZE *2.x*驅動程式，應用程式就可以設定 SQL其多資料列的 fetch 作業 _ATTR_ROW_ARRAY_SIZE。  
  
-   要升級的大部分應用程式不會實際影響 SQLSTATE 程式碼中的變更。 對於會影響這些應用程式，它們可以機械搜尋及取代在大部分情況下，使用 「 SQLSTATE 對應 」 一節中的錯誤轉換資料表，將 ODBC *3.x* odbc 錯誤碼*2.x*程式碼。 因為 ODBC *3.x*驅動程式管理員會執行對應從 ODBC *2.x* odbc Sqlstate *3.x* Sqlstate，這些應用程式撰寫者需要只檢查適用於 ODBC *3.x* Sqlstate，而不必擔心包括 ODBC *2.x*條件式的程式碼中的 Sqlstate。  
  
-   如果應用程式能妥善使用日期、 時間和時間戳記資料類型，應用程式可以宣告本身為 ODBC *2.x*應用程式並使用其現有的程式碼而不是使用的條件與程式碼。  
  
 升級也應該包含下列步驟：  
  
-   呼叫**SQLSetEnvAttr**配置將 SQL_ATTR_ODBC_VERSION 環境屬性設定為 SQL_OV_ODBC2 連線之前。  
  
-   取代所有對**SQLAllocEnv**， **SQLAllocConnect**，或**SQLAllocStmt**呼叫**SQLAllocHandle**適當*HandleType* SQL_HANDLE_ENV、 利用 SQL_HANDLE_DBC 或利用 SQL_HANDLE_STMT 的引數。  
  
-   取代所有呼叫**SQLFreeEnv**或是**SQLFreeConnect**呼叫**SQLFreeHandle**適當*HandleType*引數利用 SQL_HANDLE_DBC 或 SQL_HANDLE_STMT。  
  
-   取代所有對**SQLSetConnectOption**呼叫**SQLSetConnectAttr**。 如果將屬性設定其值為字串時，設定*StringLength*引數適當。 變更*屬性*SQL_XXXX 從要 SQL_ATTR_XXXX 的引數。  
  
-   取代所有對**SQLGetConnectOption**呼叫**SQLGetConnectAttr**。 如果收到的字串或二進位屬性，設定*Columnsize*至適當的值，並傳入*StringLength*引數。 變更*屬性*SQL_XXXX 從要 SQL_ATTR_XXXX 的引數。  
  
-   取代所有對**SQLSetStmtOption**呼叫**SQLSetStmtAttr**。 如果將屬性設定其值為字串時，設定*StringLength*引數適當。 變更*屬性*SQL_XXXX 從要 SQL_ATTR_XXXX 的引數。  
  
-   取代所有對**SQLGetStmtOption**呼叫**SQLGetStmtAttr**。 如果收到的字串或二進位屬性，設定*Columnsize*至適當的值，並傳入*StringLength*引數。 變更*屬性*SQL_XXXX 從要 SQL_ATTR_XXXX 的引數。  
  
-   取代所有對**SQLTransact**呼叫**SQLEndTran**。 如果在最右邊有效的控制代碼**SQLTransact**呼叫是環境控制代碼*HandleType*利用 SQL_HANDLE_ENV 的引數應在**SQLEndTran**呼叫適當*處理*引數。 如果最右邊有效的控制代碼，在您**SQLTransact**呼叫是連接控制代碼*HandleType*利用 SQL_HANDLE_DBC 的引數應用於**SQLEndTran**呼叫適當*處理*引數。  
  
-   取代所有對**SQLColAttributes**呼叫**SQLColAttribute**。 如果*FieldIdentifier*引數是 SQL_COLUMN_PRECISION、 SQL_COLUMN_SCALE 或 SQL_COLUMN_LENGTH，不會將函式的名稱以外的任何變更。 如果沒有，請變更*FieldIdentifier*從 SQL_DESC_XXXX 的 SQL_COLUMN_XXXX。 如果*FieldIdentifier* SQL_DESC_CONCISE_TYPE 且資料類型是 datetime 資料類型，將變更為對應的 ODBC *3.x*資料型別。  
  
-   如果使用區塊資料指標、 可捲動資料指標，或兩者，應用程式會執行下列動作：  
  
    -   設定資料列集大小、 資料指標類型，以及使用的資料指標並行**SQLSetStmtAttr**。  
  
    -   呼叫**SQLSetStmtAttr**設定 sql_attr_row_status_ptr 設定為指向狀態記錄的陣列。  
  
    -   呼叫**SQLSetStmtAttr**設為指向 SQLINTEGER SQL_ATTR_ROWS_FETCHED_PTR。  
  
    -   執行必要的繫結，並執行 SQL 陳述式。  
  
    -   呼叫**SQLFetchScroll**集中迴圈來擷取資料列，並在結果中四處移動。  
  
    -   如果它想要擷取依書籤時，應用程式會呼叫**SQLSetStmtAttr** SQL_ATTR_FETCH_BOOKMARK_PTR 設變數將包含的資料列，它想要擷取，以及呼叫的書籤**SQLFetchScroll**具有*Sqlfetchscroll*要使用 sql_fetch_bookmark 的引數。  
  
-   使用參數陣列，如果應用程式會執行下列動作：  
  
    -   呼叫**SQLSetStmtAttr**將 SQL_ATTR_PARAMSET_SIZE 屬性設定為參數陣列的大小。  
  
    -   呼叫**SQLSetStmtAttr**設為指向內部的 UDWORD 變數 SQL_ATTR_ROWS_PROCESSED_PTR。  
  
    -   會執行準備、 繫結，然後執行適當作業。  
  
    -   如果基於某些原因 （例如 SQL_NEED_DATA) 停止執行，它可以尋找 「 目前 」 的資料列的參數，藉由檢查 SQL_ATTR_ROWS_PROCESSED_PTR 所指向的位置。  
  
 此章節包含下列主題。  
  
-   [應用程式回溯相容性的取代函式對應](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [呼叫 SQLCloseCursor](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [呼叫 SQLGetDiagField](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [呼叫 SQLSetPos](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [資料指標程式庫作業](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [對應資料指標 Attributes1 資訊類型](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)
