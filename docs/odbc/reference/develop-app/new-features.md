---
title: 新功能 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302396"
---
# <a name="new-features"></a>新功能
ODBC 3.x 中引進了下列新*功能。* 使用*odbc 2.x* *驅動程式的 odbc 3.x 應用程式*將無法使用這種功能。 使用 ODBC *2.x 驅動程式時，odbc 3.X* *驅動程式管理員*不會對應這些功能。  
  
-   接受描述項控制碼做為引數的函式： **SQLSetDescField**、 **SQLGetDescField**、 **SQLSetDescRec**、 **SQLGetDescRec**和**SQLCopyDesc**。  
  
-   函式會**SQLSetEnvAttr**和**SQLGetEnvAttr**。  
  
-   使用**SQLAllocHandle**來配置描述項控制碼。 （使用**SQLAllocHandle**來配置環境、連接和語句控制碼是重複的，而不是新的功能）。  
  
-   使用**SQLGetConnectAttr**來取得 SQL_ATTR_AUTO_IPD 連接屬性。 （使用**SQLSetConnectAttr**來設定，而**SQLGetConnectAttr**要取得，其他連接屬性則是重複的，而不是新的功能）。  
  
-   使用**SQLSetStmtAttr**來設定和**SQLGetStmtAttr**以取得下列語句屬性。 （使用**SQLSetStmtAttr**來設定和**SQLGetStmtAttr**以取得，其他語句屬性則是重複的，而不是新的功能）。  
  
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
  
-   使用**SQLGetStmtAttr**來取得下列語句屬性。 （使用**SQLGetStmtAttr**取得其他語句屬性是重複的功能，而不是新的功能）。  
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   使用 interval C 資料類型、間隔 SQL 資料類型、BIGINT C 資料類型，以及 SQL_C_NUMERIC 的資料結構。  
  
-   參數的資料列取向系結。  
  
-   以位移為基礎的書簽提取，例如以 SQL_FETCH_BOOKMARK 的*FetchOrientation*引數呼叫**SQLFetchScroll** ，並指定0以外的位移。  
  
-   **SQLFetch**會傳回資料列狀態陣列、提取的資料列數目、提取多個資料列、使用**SQLFetchScroll**的混合呼叫，以及使用**SQLBulkOperations**或**SQLSetPos**的混合呼叫。 如需詳細資訊，請參閱下一節： [ODBC 3.X 應用程式的區塊資料指標、可滾動游標和回溯相容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)。  
  
-   具名引數。  
  
-   任何*ODBC 3.x*特定**SQLGetInfo**選項。 （如果*使用 odbc 2.x* *驅動程式的 odbc 3.x 應用程式*呼叫了 SQL_XXX_CURSOR_ATTRIBUTES1 資訊類型，而這種情況已經取代了數個*ODBC 2.x*資訊類型，部分資訊可能會很可靠，但有些則可能不可靠。 如需詳細資訊，請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)）。  
  
-   系結位移。  
  
-   依書簽更新、重新整理和刪除（透過呼叫**SQLBulkOperations**）。  
  
-   在 S5 狀態中呼叫**SQLBulkOperations**或**SQLSetPos** 。  
  
-   診斷記錄中的 ROW_NUMBER 和 COLUMN_NUMBER 欄位（必須由取代函數**SQLGetDiagField**或**SQLGetDiagRec**抓取）。  
  
-   大約的資料列計數。  
  
-   警告資訊（來自**SQLFetchScroll**的 SQL_ROW_SUCCESS_WITH_INFO）。  
  
-   可變長度的書簽。  
  
-   參數陣列的延伸錯誤資訊。  
  
-   目錄函式所傳回之結果集中的所有新資料行。  
  
-   在資料行0上使用**SQLDescribeCol**和**SQLColAttribute** 。  
  
-   在**SQLColAttribute**的呼叫中使用*任何 ODBC 3.x 特定的資料*行屬性。  
  
-   使用多個環境控制碼。  
  
 本章節包含下列主題。  
  
-   [適用於 ODBC 3.x 應用程式的區塊資料指標、可捲動的資料指標和回溯相容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
