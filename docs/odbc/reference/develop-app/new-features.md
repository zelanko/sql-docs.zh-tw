---
title: 新功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], new features in release
- ODBC drivers [ODBC], backward compatibility
- new features [ODBC]
- compatibility [ODBC], new features in release
- ODBC [ODBC], new features
ms.assetid: a8fcdd00-6cb3-4871-9489-6018b3d0d65f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b40803dac6c9f296043a8dcac50f9bc69036875a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302396"
---
# <a name="new-features"></a>新功能
ODBC *3.x*中引入了以下新功能。 使用 ODBC *2.x*驅動程式的 ODBC *3.x*應用程式將無法使用此功能。 使用 ODBC *2.x*驅動程式時,ODBC *3.x*驅動程式管理器不會映射這些功能。  
  
-   以描述符句柄為參數的函數:SQLSetDescField、SQLGetDescField、SQLSetDescRec、SQLGetDescRec 和**SQLCopyDesc**。 **SQLSetDescField** **SQLGetDescField** **SQLSetDescRec** **SQLGetDescRec**  
  
-   函數**SQLSetEnvAttr**與**SQLGetEnvAttr**。  
  
-   使用**SQLAllocHandle**來分配描述符句柄。 (使用**SQLAllocHandle**分配環境、連接和語句句柄是重複的,而不是新的功能。  
  
-   使用**SQLGetConnect Attr**獲取SQL_ATTR_AUTO_IPD連接屬性。 (使用**SQLSetConnectAttr**設定,並使用**SQLGetConnectAttr**來取得其他連接屬性是重複的,而不是新的功能。  
  
-   使用**SQLSetStmtAttr 設定 SQLTmtAttr,** 以及**SQLGetStmtAttr**來獲取以下語句屬性。 (使用**SQLSetStmtAttr**來設置,並且**SQLGetStmtAttr**來獲取其他語句屬性是重複的,而不是新的。  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_ENABLE_AUTO_IPD  
  
     SQL_ATTR_FETCH_BOOKMARK_PTR  
  
     SQL_ATTR_BIND_OFFSET  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     SQL_DESC_PARAM_STATUS_PTR  
  
     SQL_ATTR_PARAMS_PROCESSED_PTR  
  
     SQL_ATTR_PARAMSET_SIZE  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_ROW_ARRAY_SIZE  
  
-   使用**SQLGetStmtAttr**獲取以下語句屬性。 (使用**SQLGetStmtAttr**獲取其他語句屬性是重複的功能,而不是新功能。  
  
     SQL_ATTR_IMP_ROW_DESCSQL_ATTR_IMP_PARAM_DESC  
  
-   使用間隔 C 數據類型、間隔 SQL 資料類型、BIGINT C 數據類型和SQL_C_NUMERIC數據結構。  
  
-   參數的行綁定。  
  
-   基於偏移的書籤提取,例如使用fetch*方向*參數SQL_FETCH_BOOKMARK調用**SQLFetchScroll,** 並指定偏移量(而不是 0)。  
  
-   **SQLFetch**傳回行狀態陣列、提取的行數、獲取多行、將呼叫與**SQLFetchScroll**混合,以及將呼叫與**SQLBulk 操作**或**SQLSetPos**混合。 有關詳細資訊,請參閱下一節「[區塊游標、可滾動游標」 與 ODBC 3.x 應用程式的向後相容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)。  
  
-   命名參數。  
  
-   任何 ODBC *3.x*特定**SQLGetInfo**選項。 (如果使用 ODBC *2.x*驅動程式的 ODBC *3.x*應用程式呼叫SQL_XXX_CURSOR_ATTRIBUTES1資訊類型,這些類型已替換了多個 ODBC *2.x*資訊類型,則某些資訊可能可靠,但有些資訊可能不可靠。 有關詳細資訊,請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)。)  
  
-   綁定偏移。  
  
-   按書籤(透過呼叫**SQLBulk 操作**)更新、刷新和刪除。  
  
-   在 S5 狀態下調用**SQLBulk 操作**或**SQLSetPos。**  
  
-   診斷記錄中ROW_NUMBER和COLUMN_NUMBER欄位(必須透過替換函數**SQLGetDiagField**或**SQLGetDiagRec**檢索)。  
  
-   近似行計數。  
  
-   警告資訊(從**SQLFetchScroll SQL_ROW_SUCCESS_WITH_INFO)。**  
  
-   可變長度書籤。  
  
-   參數陣列的擴展錯誤資訊。  
  
-   目錄函數返回的結果集中的所有新列。  
  
-   在列 0 上使用**SQLDescribeCol**和**SQLColAttribute。**  
  
-   在調用**SQLColAttribute**中使用任何 ODBC *3.x*特定的列屬性。  
  
-   使用多個環境句柄。  
  
 本節包含以下主題。  
  
-   [適用於 ODBC 3.x 應用程式的區塊資料指標、可捲動的資料指標和回溯相容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
