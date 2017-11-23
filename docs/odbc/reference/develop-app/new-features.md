---
title: "新功能 |Microsoft 文件"
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
helpviewer_keywords:
- backward compatibility [ODBC], new features in release
- ODBC drivers [ODBC], backward compatibility
- new features [ODBC]
- compatibility [ODBC], new features in release
- ODBC [ODBC], new features
ms.assetid: a8fcdd00-6cb3-4871-9489-6018b3d0d65f
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 016c2cefd6280a7b2cc21e4b5e290468d8271973
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="new-features"></a>新功能
在 ODBC 3 已經導入下列新功能。*x*。 ODBC 3。*x*應用程式使用 ODBC 2*.x*驅動程式不能使用這項功能。 ODBC 3。*x*驅動程式管理員不會對應這些功能時使用的 ODBC 2*.x*驅動程式。  
  
-   取得描述元的函式處理做為引數： **SQLSetDescField**， **SQLGetDescField**， **SQLSetDescRec**， **SQLGetDescRec**，和**SQLCopyDesc**。  
  
-   函式**SQLSetEnvAttr**和**SQLGetEnvAttr**。  
  
-   使用**SQLAllocHandle**配置描述項控制代碼。 (使用**SQLAllocHandle**配置環境、 連接和陳述式控制代碼是重複的、 未新增的功能。)  
  
-   使用**SQLGetConnectAttr**取得 SQL_ATTR_AUTO_IPD 連接屬性。 (使用**SQLSetConnectAttr**若要設定，和**SQLGetConnectAttr**若要取得，其他連接屬性可以重複、 未新增的功能。)  
  
-   使用**SQLSetStmtAttr**若要設定，和**SQLGetStmtAttr**若要取得，下列陳述式屬性。 (使用**SQLSetStmtAttr**若要設定，和**SQLGetStmtAttr**若要取得，其他陳述式屬性是重複的、 未新增的功能。)  
  
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
  
-   使用**SQLGetStmtAttr**取得下列陳述式屬性。 (使用**SQLGetStmtAttr**以取得其他陳述式屬性是重複的功能，而不是新的功能。)  
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   使用間隔 C 資料類型、 間隔 SQL 資料類型、 BIGINT C 資料類型，以及 SQL_C_NUMERIC 資料結構。  
  
-   資料列取向的繫結的參數。  
  
-   位移為基礎的書籤提取，例如呼叫**SQLFetchScroll**與*Sqlfetchscroll* SQL_FETCH_BOOKMARK 和指定的位移 0 以外的引數。  
  
-   **SQLFetch**傳回資料列狀態陣列，提取的資料列，提取多個資料列，包含混合的呼叫數**SQLFetchScroll**，並混合呼叫**SQLBulkOperations**或**SQLSetPos**。 如需詳細資訊，請參閱下節中，[區塊資料指標，可捲動資料指標，ODBC 3.x 應用程式的回溯相容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)。  
  
-   具名的參數。  
  
-   任何 ODBC 3。*x*– 特定**SQLGetInfo**選項。 （若為 ODBC 3。*x*應用程式使用 ODBC 2。*x*驅動程式會呼叫 SQL_XXX_CURSOR_ATTRIBUTES1 資訊類型，其具有取代數個 ODBC 2。*x*資訊類型的部分資訊可能是可靠的但有些可能不可靠。 如需詳細資訊，請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)。)  
  
-   繫結的位移。  
  
-   更新、 重新整理，以及刪除書籤 (透過呼叫**SQLBulkOperations**)。  
  
-   呼叫**SQLBulkOperations**或**SQLSetPos** S5 狀態中。  
  
-   診斷記錄中的 ROW_NUMBER 和 R1C1 欄位 (具有要取代的函式所擷取**SQLGetDiagField**或**SQLGetDiagRec**)。  
  
-   近似資料列計數。  
  
-   警告資訊 (從 SQL_ROW_SUCCESS_WITH_INFO **SQLFetchScroll**)。  
  
-   可變長度的書籤。  
  
-   擴充的錯誤資訊陣列的參數。  
  
-   所有新的資料行目錄函數所傳回之結果集內。  
  
-   使用**SQLDescribeCol**和**SQLColAttribute**上資料行 0。  
  
-   使用的任何 ODBC 3。*x*– 的呼叫中的特定資料行屬性**SQLColAttribute**。  
  
-   使用多個環境控制代碼。  
  
 本章節包含下列主題。  
  
-   [適用於 ODBC 3.x 應用程式的區塊資料指標、可捲動的資料指標和回溯相容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
