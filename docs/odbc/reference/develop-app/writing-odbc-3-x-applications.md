---
title: 編寫 ODBC 3.x 應用程式 |微軟文件
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
ms.openlocfilehash: 3ba48d76babcaa5fcc49a541088f7c4cc349b569
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288986"
---
# <a name="writing-odbc-3x-applications"></a>撰寫 ODBC 3.x 應用程式
當 ODBC *2.x*應用程式升級到 ODBC *3.x*時,應編寫它,以便它同時適用於 ODBC *2.x*和*3.x*驅動程式。 應用程式應合併條件代碼以充分利用 ODBC *3.x*功能。  
  
 SQL_ATTR_ODBC_VERSION環境屬性應設置為SQL_OV_ODBC2。 這將確保驅動程式的行為類似於 ODBC *2.x*驅動程式相對於「[行為更改](../../../odbc/reference/develop-app/behavioral-changes.md)」部分中描述的更改。  
  
 如果應用程式將使用新[功能](../../../odbc/reference/develop-app/new-features.md)「部分中描述的任何功能,則應使用條件代碼來確定驅動程式是 ODBC *3.x*還是 ODBC *2.x*驅動程式。 應用程式使用**SQLGetDiagField**和**SQLGetDiagRec**來獲取 ODBC *3.x* SQLSTATEs,同時對這些條件代碼片段執行錯誤處理。 應考慮有關新功能的以下幾點:  
  
-   受行組大小行為更改影響的應用程式在陣列大小大於 1 時,應小心不要調用**SQLFetch。** 這些應用程式應用對**SQLSetStmtAttr**的呼叫替換對**SQLAtttAttr**的呼叫,以設定SQL_ATTR_ARRAY_STATUS_PTR語句屬性和**SQLFetchScroll,** 以便它們具有適用於 ODBC *3.x*和 ODBC *2.x*驅動程式的通用代碼。 由於帶有SQL_ATTR_ROW_ARRAY_SIZE的**SQLSetStmtAttr**將映射到具有 SQL_ROWSET_SIZE的 ODBC *2.x*驅動程式的**SQLSetStmtAttr,** 因此應用程式只需為其多行提取操作設定SQL_ATTR_ROW_ARRAY_SIZE即可。  
  
-   大多數正在升級的應用程式實際上不受 SQLSTATE 代碼更改的影響。 對於受影響的應用程式,在大多數情況下,可以使用"SQLSTATE 映射"部分中的錯誤轉換表將ODBC *3.x*錯誤代碼轉換為ODBC *2.x*代碼,進行機械搜索和替換。 由於 ODBC *3.x*驅動程式管理器將執行從 ODBC *2.x* SQLSTAT 到 ODBC *3.x* SQLSTAT 的映射,因此這些應用程式編寫器只需檢查 ODBC *3.x* SQLSTATEs,而不必擔心在條件代碼中包括 ODBC *2.x* SQLSTAT。  
  
-   如果應用程式充分利用了日期、時間和時間戳數據類型,則應用程式可以聲明自己是 ODBC *2.x*應用程式,並使用其現有代碼而不是使用調理代碼。  
  
 升級還應包括以下步驟:  
  
-   在分配連接以將SQL_ATTR_ODBC_VERSION環境屬性設置為SQL_OV_ODBC2之前,請調用**SQLSetEnvAttr。**  
  
-   將對**SQLAllocEnv、SQLAllocConnect**或**SQLAllocStmt**的所有調用替換為對**SQLAllocHandle**的調用,以及SQL_HANDLE_ENV、SQL_HANDLE_DBC或SQL_HANDLE_STMT的**SQLAllocConnect**相應*HandleType*參數。  
  
-   將**SQLFreeEnv**或**SQLFreeConnect**的所有呼叫替換為對**SQLFreeHandle**的呼叫,以及SQL_HANDLE_DBC或SQL_HANDLE_STMT的相應*HandleType*參數。  
  
-   將**SQLSetConnectOption**的所有呼叫替換為對**SQLSetConnectAttr 的**呼叫。 如果設置其值為字串的屬性,則適當設置*StringLength*參數。 將*屬性*參數從SQL_XXXX更改為SQL_ATTR_XXXX。  
  
-   將**SQLGetConnectOption**的所有調用替換為對**SQLGetConnectAttr 的**調用。 如果取得字串或二進位屬性,則將*BufferLength*設定為適當的值並傳遞*StringLength 參數*。 將*屬性*參數從SQL_XXXX更改為SQL_ATTR_XXXX。  
  
-   將**SQLSetStmtOption**的所有呼叫替換為對**SQLSetStmtAttr 的**調用。 如果設置其值為字串的屬性,則適當設置*StringLength*參數。 將*屬性*參數從SQL_XXXX更改為SQL_ATTR_XXXX。  
  
-   將所有對**SQLGetStmtOption**的調用替換為對**SQLGetStmtAttr 的**調用。 如果取得字串或二進位屬性,則將*BufferLength*設定為適當的值並傳遞*StringLength 參數*。 將*屬性*參數從SQL_XXXX更改為SQL_ATTR_XXXX。  
  
-   將**SQLTransact**的所有呼叫替換為對**SQLEndTran**的呼叫。 如果**SQLTransact**調用中最正確的句柄是環境句柄,則應在**SQLEndTran**調用中使用 SQL_HANDLE_ENV的*句柄類型*參數,並帶有相應的*句柄*參數。 如果**SQLTransact**調用中最正確的句柄是連接句柄,則應在**SQLEndTran**調用中使用SQL_HANDLE_DBC的*句柄類型*參數,並帶有相應的*句柄*參數。  
  
-   將**SQLColattributes**的所有調用替換為對**SQLColattribute 的**調用。 如果*FieldIdentifier*參數是SQL_COLUMN_PRECISION、SQL_COLUMN_SCALE或SQL_COLUMN_LENGTH,則不要更改函數名稱以外的任何內容。 如果沒有,則將*字段標識符*從SQL_COLUMN_XXXX更改為SQL_DESC_XXXX。 如果*欄位識別碼*SQL_DESC_CONCISE_TYPE並且資料類型是日期時間數據類型,則更改為相應的 ODBC *3.x*資料類型。  
  
-   如果使用區塊游標、可滾動遊標或兩者,則應用程式執行以下操作:  
  
    -   使用**SQLSetStmtAttr**設定列組大小、游標類型和游標併發。  
  
    -   調用**SQLSetStmtAttr**以設定SQL_ATTR_ROW_STATUS_PTR以指向狀態記錄陣列。  
  
    -   調用**SQLSetStmtAttr**以設定SQL_ATTR_ROWS_FETCHED_PTR以指向 SQLINTEGER。  
  
    -   執行所需的綁定並執行 SQL 語句。  
  
    -   在循環中調用**SQLFetchScroll**以提取行並在結果集中移動。  
  
    -   如果應用程式希望按書籤獲取,則應用程式將調用**SQLSetStmtAttr**以將SQL_ATTR_FETCH_BOOKMARK_PTR設置為一個變數,該變數將包含要提取的行的書籤,並且使用 SQL_FETCH_BOOKMARK的 Fetch*方向*參數調用**SQLFetchScroll。**  
  
-   如果使用參數陣列,應用程式將執行以下操作:  
  
    -   呼叫**SQLSetStmtAttr**將SQL_ATTR_PARAMSET_SIZE屬性設置為參數陣列的大小。  
  
    -   調用**SQLSetStmtAttr**以設定SQL_ATTR_ROWS_PROCESSED_PTR以指向內部 UDWORD 變數。  
  
    -   根據需要執行準備、綁定和執行操作。  
  
    -   如果執行由於某種原因(如SQL_NEED_DATA)停止,它可以通過檢查SQL_ATTR_ROWS_PROCESSED_PTR指向的位置來查找參數的"當前"行。  
  
 此章節包含下列主題。  
  
-   [應用程式回溯相容性的取代函式對應](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [呼叫 SQLCloseCursor](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [呼叫 SQLGetDiagField](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [呼叫 SQLSetPos](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [資料指標程式庫作業](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [對應資料指標 Attributes1 資訊類型](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)
