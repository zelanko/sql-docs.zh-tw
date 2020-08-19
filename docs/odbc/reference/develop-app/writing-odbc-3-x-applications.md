---
description: 撰寫 ODBC 3.x 應用程式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7df97b99df10e613ee45aaa3c01174b46160e740
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421352"
---
# <a name="writing-odbc-3x-applications"></a>撰寫 ODBC 3.x 應用程式
當 ODBC 2.x*應用程式*升級為 odbc 3.x*時，應該*撰寫它以搭配 odbc *2.x 和 3.x*驅動程式使用 *。* 應用程式應該併入條件式程式碼，以充分*利用 ODBC 3.x 功能。*  
  
 SQL_ATTR_ODBC_VERSION 環境屬性應設定為 SQL_OV_ODBC2。 這可確保 *驅動程式的* 行為就像 ODBC 2.x 驅動程式，與「 [行為變更](../../../odbc/reference/develop-app/behavioral-changes.md)」一節中所述的變更有關。  
  
 如果應用程式將使用 [新功能](../../../odbc/reference/develop-app/new-features.md)一節中所述的任何功能，則應該使用條件式程式碼來判斷驅動程式是否為 odbc *3.x 或 odbc* 2.x *驅動程式* 。 應用程式會使用 **SQLGetDiagField** 和 **SQLGETDIAGREC** 來取得 *ODBC 3.x* SQLSTATEs，同時對這些條件式程式碼片段執行錯誤處理。 應考慮下列關於新功能的重點：  
  
-   當陣列大小大於1時，受到資料列集大小行為變更影響的應用程式應該小心不要呼叫 **SQLFetch** 。 這些應用程式應該使用**SQLSetStmtAttr**的呼叫來取代**SQLExtendedFetch**的呼叫，以設定 SQL_ATTR_ARRAY_STATUS_PTR 語句屬性和**SQLFetchScroll**，讓它們具有可同時搭配 odbc *3.x 和 odbc* *2.x 驅動程式*使用的通用程式碼。 由於具有 SQL_ATTR_ROW_ARRAY_SIZE 的**SQLSetStmtAttr**會對應到*具有 ODBC 2.x*驅動程式 SQL_ROWSET_SIZE 的**SQLSetStmtAttr** ，因此應用程式可以直接設定其多資料列提取作業的 SQL_ATTR_ROW_ARRAY_SIZE。  
  
-   大部分正在升級的應用程式實際上並不會受到 SQLSTATE 碼變更的影響。 針對受影響的應用程式，他們可以在大部分情況下使用「SQLSTATE 對應」一節中的錯誤轉換表來進行機械搜尋和取代，將*odbc 3.x*錯誤碼轉換成 odbc 2.x*程式碼。* 由於 ODBC 3.x*驅動程式*管理員會執行從 odbc *2.X SQLSTATEs 至*odbc *3.x SQLSTATEs 的*對應，因此這些應用程式寫入器只需要檢查 odbc 3.x SQLSTATEs，而不必擔心在條件式程式碼中*包含 odbc 2.x* *SQLSTATEs。*  
  
-   如果應用程式充分利用日期、時間和時間戳記資料類型，應用程式可以將自己宣告為 ODBC 2.x 應用程式，並使用其現有的程式碼，而不是使用重 *設程式碼* 。  
  
 升級也應該包含下列步驟：  
  
-   在配置連接之前呼叫 **SQLSetEnvAttr** ，以將 SQL_ATTR_ODBC_VERSION 環境屬性設定為 SQL_OV_ODBC2。  
  
-   **以 SQL_HANDLE_ENV** 、SQL_HANDLE_DBC 或 SQL_HANDLE_STMT 的適當*HandleType*引數，取代對**SQLAllocEnv**、 **SQLAllocConnect**或**SQLAllocStmt**的所有呼叫。  
  
-   使用 SQL_HANDLE_DBC 或 SQL_HANDLE_STMT 的適當*HandleType*引數，將對**SQLFreeEnv**或**SQLFreeConnect**的呼叫取代為對**SQLFreeHandle**的呼叫。  
  
-   使用**SQLSetConnectAttr**的呼叫來取代**SQLSetConnectOption**的所有呼叫。 如果設定其值為字串的屬性，請適當地設定 *StringLength* 引數。 將 *屬性* 引數從 SQL_XXXX 變更為 SQL_ATTR_XXXX。  
  
-   使用**SQLGetConnectAttr**的呼叫來取代**SQLGetConnectOption**的所有呼叫。 如果取得字串或二進位屬性，請將 *BufferLength* 設定為適當的值，並傳入 *StringLength* 引數。 將 *屬性* 引數從 SQL_XXXX 變更為 SQL_ATTR_XXXX。  
  
-   使用**SQLSetStmtAttr**的呼叫來取代**SQLSetStmtOption**的所有呼叫。 如果設定其值為字串的屬性，請適當地設定 *StringLength* 引數。 將 *屬性* 引數從 SQL_XXXX 變更為 SQL_ATTR_XXXX。  
  
-   使用**SQLGetStmtAttr**的呼叫來取代**SQLGetStmtOption**的所有呼叫。 如果取得字串或二進位屬性，請將 *BufferLength* 設定為適當的值，並傳入 *StringLength* 引數。 將 *屬性* 引數從 SQL_XXXX 變更為 SQL_ATTR_XXXX。  
  
-   使用**SQLEndTran**的呼叫來取代**SQLTransact**的所有呼叫。 如果**SQLTransact**呼叫中最右邊的有效控制碼是環境控制碼，則應該在**SQLEndTran**呼叫中使用適當的*控制碼*引數來使用 SQL_HANDLE_ENV 的*HandleType*引數。 如果**SQLTransact**呼叫中最右邊的有效控制碼是連接控制碼，則應該在**SQLEndTran**呼叫中使用適當的*控制碼*引數來使用 SQL_HANDLE_DBC 的*HandleType*引數。  
  
-   使用**SQLColAttribute**的呼叫來取代**SQLColAttributes**的所有呼叫。 如果 *FieldIdentifier* 引數是 SQL_COLUMN_PRECISION、SQL_COLUMN_SCALE 或 SQL_COLUMN_LENGTH，則請勿變更函式名稱以外的任何名稱。 如果沒有，請將 *FieldIdentifier* 從 SQL_COLUMN_XXXX 變更為 SQL_DESC_XXXX。 如果 *FieldIdentifier* 是 SQL_DESC_CONCISE_TYPE，且資料類型是 datetime 資料類型，請變更為對應 *的 ODBC 3.x* 資料類型。  
  
-   如果使用區塊資料指標、可滾動的資料指標或兩者，則應用程式會執行下列動作：  
  
    -   使用 **SQLSetStmtAttr**來設定資料列集大小、資料指標類型和資料指標並行。  
  
    -   呼叫 **SQLSetStmtAttr** ，以將 SQL_ATTR_ROW_STATUS_PTR 設定為指向狀態記錄陣列。  
  
    -   呼叫 **SQLSetStmtAttr** 以將 SQL_ATTR_ROWS_FETCHED_PTR 設定為指向 SQLINTEGER。  
  
    -   執行必要的系結，並執行 SQL 語句。  
  
    -   在迴圈中呼叫 **SQLFetchScroll** 來提取資料列，並在結果集內四處移動。  
  
    -   如果它想要以書簽提取，應用程式會呼叫**SQLSetStmtAttr** ，將 SQL_ATTR_FETCH_BOOKMARK_PTR 設定為變數，該變數將包含要提取之資料列的書簽，並使用 SQL_FETCH_BOOKMARK 的*FetchOrientation*引數來呼叫**SQLFetchScroll** 。  
  
-   如果使用參數的陣列，應用程式會執行下列動作：  
  
    -   呼叫 **SQLSetStmtAttr** ，將 SQL_ATTR_PARAMSET_SIZE 屬性設定為參數陣列的大小。  
  
    -   呼叫 **SQLSetStmtAttr** ，以將 SQL_ATTR_ROWS_PROCESSED_PTR 設定為指向內部 UDWORD 變數。  
  
    -   適當地執行準備、系結和執行作業。  
  
    -   如果執行因某些原因而中止 (例如 SQL_NEED_DATA) ，它可以藉由檢查 SQL_ATTR_ROWS_PROCESSED_PTR 所指向的位置，找到「目前」的參數資料列。  
  
 此章節包含下列主題。  
  
-   [應用程式回溯相容性的取代函式對應](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [呼叫 SQLCloseCursor](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [呼叫 SQLGetDiagField](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [呼叫 SQLSetPos](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [資料指標程式庫作業](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [對應資料指標 Attributes1 資訊類型](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)
