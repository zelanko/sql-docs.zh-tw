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
ms.openlocfilehash: 9939d11e3a779cc25d7faeb4950783353947f140
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081450"
---
# <a name="writing-odbc-3x-applications"></a>撰寫 ODBC 3.x 應用程式
當 ODBC 2.x*應用程式*升級至 odbc 3.x*時，應該*將它撰寫成可以與 odbc *2.x 和 3.x*驅動程式一起使用。 ** 應用程式應納入條件式程式碼，以充分*利用 ODBC 3.x 功能。*  
  
 SQL_ATTR_ODBC_VERSION 環境屬性應設定為 SQL_OV_ODBC2。 這可確保*驅動程式的*行為與「[行為變更](../../../odbc/reference/develop-app/behavioral-changes.md)」一節中所述的變更有關。  
  
 如果應用程式將使用「[新增功能](../../../odbc/reference/develop-app/new-features.md)」一節中所述的任何功能，則應該使用條件式程式碼來判斷驅動程式是否為 odbc *3.x 或 odbc* *2.x 驅動程式*。 應用程式會使用**SQLGetDiagField**和**SQLGETDIAGREC**來取得*ODBC 3.x* SQLSTATEs，同時對這些條件式程式碼片段進行錯誤處理。 應考慮下列關於新功能的重點：  
  
-   當陣列大小大於1時，應用程式會受到資料列集大小行為變更的影響，而不需要呼叫**SQLFetch** 。 這些應用程式應該使用**SQLSetStmtAttr**的呼叫來取代對**SQLExtendedFetch**的呼叫，以設定 SQL_ATTR_ARRAY_STATUS_PTR 語句屬性和**SQLFetchScroll**，使其具有可與 odbc *3.x 和 odbc* *2.x 驅動程式*一起運作的通用程式碼。 因為具有 SQL_ATTR_ROW_ARRAY_SIZE 的**SQLSetStmtAttr**會對應至**SQLSETSTMTATTR** ，*而 ODBC 2.x*驅動程式的 SQL_ROWSET_SIZE，應用程式可以直接設定其多資料列提取作業的 SQL_ATTR_ROW_ARRAY_SIZE。  
  
-   大部分升級的應用程式實際上不會受到 SQLSTATE 代碼變更的影響。 對於受影響的應用程式，他們可以執行機械搜尋，並在大多數情況下使用「SQLSTATE 對應」區段中的錯誤轉換表來取代，將*odbc 3.x*錯誤碼轉換成 odbc 2.x*程式碼。* 由於 ODBC 3.x*驅動程式*管理員會執行從 odbc *2.X SQLSTATEs 到*odbc *3.x SQLSTATEs 的*對應，因此這些應用程式寫入器只需要檢查 odbc 3.x SQLSTATEs，而不必擔心在條件式程式碼中*包含 odbc 2.x* *SQLSTATEs。*  
  
-   如果應用程式充分利用 date、time 和 timestamp 資料類型，應用程式就可以將其本身宣告*為 ODBC 2.x*應用程式，並使用其現有的程式碼，而不是使用調節程式碼。  
  
 升級也應該包含下列步驟：  
  
-   在配置連接之前呼叫**SQLSetEnvAttr** ，以將 SQL_ATTR_ODBC_VERSION 環境屬性設定為 SQL_OV_ODBC2。  
  
-   將所有對**SQLAllocEnv**、 **SQLAllocConnect**或**SQLAllocStmt**的呼叫取代為 SQL_HANDLE_ENV、SQL_HANDLE_DBC 或 SQL_HANDLE_STMT 的適當*HandleType*引數呼叫**SQLAllocHandle** 。  
  
-   以 SQL_HANDLE_DBC 或 SQL_HANDLE_STMT 的適當*HandleType*引數呼叫**SQLFreeHandle** ，以取代所有對**SQLFreeEnv**或**SQLFreeConnect**的呼叫。  
  
-   將**SQLSetConnectOption**的所有呼叫取代為**SQLSetConnectAttr**的呼叫。 如果設定的屬性值為字串，請適當地設定*StringLength*引數。 將*屬性*引數從 SQL_XXXX 變更為 SQL_ATTR_XXXX。  
  
-   將**SQLGetConnectOption**的所有呼叫取代為**SQLGetConnectAttr**的呼叫。 如果取得字串或二進位屬性，請將*BufferLength*設定為適當的值，並傳入*StringLength*引數。 將*屬性*引數從 SQL_XXXX 變更為 SQL_ATTR_XXXX。  
  
-   將**SQLSetStmtOption**的所有呼叫取代為**SQLSetStmtAttr**的呼叫。 如果設定的屬性值為字串，請適當地設定*StringLength*引數。 將*屬性*引數從 SQL_XXXX 變更為 SQL_ATTR_XXXX。  
  
-   將**SQLGetStmtOption**的所有呼叫取代為**SQLGetStmtAttr**的呼叫。 如果取得字串或二進位屬性，請將*BufferLength*設定為適當的值，並傳入*StringLength*引數。 將*屬性*引數從 SQL_XXXX 變更為 SQL_ATTR_XXXX。  
  
-   將**SQLTransact**的所有呼叫取代為**SQLEndTran**的呼叫。 如果**SQLTransact**呼叫中最右邊的有效控制碼是環境控制碼，則應在具有適當*控制碼*引數的**SQLEndTran**呼叫中使用 SQL_HANDLE_ENV 的*HandleType*引數。 如果**SQLTransact**呼叫中最右邊的有效控制碼是連接控制碼，則應在具有適當*控制碼*引數的**SQLEndTran**呼叫中使用 SQL_HANDLE_DBC 的*HandleType*引數。  
  
-   將**SQLColAttributes**的所有呼叫取代為**SQLColAttribute**的呼叫。 如果*FieldIdentifier*引數是 SQL_COLUMN_PRECISION、SQL_COLUMN_SCALE 或 SQL_COLUMN_LENGTH，請勿變更函數名稱以外的任何專案。 如果不是，請將*FieldIdentifier*從 SQL_COLUMN_XXXX 變更為 SQL_DESC_XXXX。 如果*FieldIdentifier* SQL_DESC_CONCISE_TYPE，且資料類型是 datetime 資料類型，請將變更為對應*的 ODBC 3.x*資料類型。  
  
-   如果使用區塊資料指標、可滾動游標或兩者，則應用程式會執行下列動作：  
  
    -   使用**SQLSetStmtAttr**設定資料列集大小、資料指標類型和資料指標並行。  
  
    -   呼叫**SQLSetStmtAttr** ，將 SQL_ATTR_ROW_STATUS_PTR 設定為指向狀態記錄的陣列。  
  
    -   呼叫**SQLSetStmtAttr** ，將 SQL_ATTR_ROWS_FETCHED_PTR 設定為指向 SQLINTEGER。  
  
    -   執行必要的系結，並執行 SQL 語句。  
  
    -   呼叫迴圈中的**SQLFetchScroll**來提取資料列，並在結果集內四處移動。  
  
    -   如果它想要依書簽提取，應用程式會呼叫**SQLSetStmtAttr** ，將 SQL_ATTR_FETCH_BOOKMARK_PTR 設定為變數，其中將包含所要提取之資料列的書簽，並使用 SQL_FETCH_BOOKMARK 的*FetchOrientation*引數呼叫**SQLFetchScroll** 。  
  
-   如果使用參數陣列，應用程式會執行下列動作：  
  
    -   呼叫**SQLSetStmtAttr** ，將 SQL_ATTR_PARAMSET_SIZE 屬性設定為參數陣列的大小。  
  
    -   呼叫**SQLSetStmtAttr** ，將 SQL_ATTR_ROWS_PROCESSED_PTR 設定為指向內部 UDWORD 變數。  
  
    -   視情況執行準備、系結和執行作業。  
  
    -   如果執行因為某些原因（例如 SQL_NEED_DATA）而停止，它可以藉由檢查 SQL_ATTR_ROWS_PROCESSED_PTR 所指向的位置來尋找參數的「目前」資料列。  
  
 此章節包含下列主題。  
  
-   [應用程式回溯相容性的取代函式對應](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [呼叫 SQLCloseCursor](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [呼叫 SQLGetDiagField](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [呼叫 SQLSetPos](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [資料指標程式庫作業](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [對應資料指標 Attributes1 資訊類型](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)
