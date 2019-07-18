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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 74c9a97c2511bc9c9a738b9e63548a9179552489
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086338"
---
# <a name="new-features"></a>新功能
ODBC 中已引進下列新功能*3.x*。 ODBC *3.x*應用程式使用 ODBC *2.x*驅動程式不能使用這項功能。 ODBC *3.x*驅動程式管理員不會對應這些功能，使用 ODBC 時*2.x*驅動程式。  
  
-   接受的描述元的函式會處理做為引數：**SQLSetDescField**， **SQLGetDescField**， **SQLSetDescRec**， **SQLGetDescRec**，並**SQLCopyDesc**。  
  
-   函式**SQLSetEnvAttr**並**SQLGetEnvAttr**。  
  
-   善用**SQLAllocHandle**配置描述項控制代碼。 (使用**SQLAllocHandle**配置環境、 連接和陳述式控制代碼是重複的、 未新增的功能。)  
  
-   善用**SQLGetConnectAttr**取得 SQL_ATTR_AUTO_IPD 連接屬性。 (使用**SQLSetConnectAttr**若要設定，以及**SQLGetConnectAttr**其他連接屬性來取得，是重複的、 未新增的功能。)  
  
-   善用**SQLSetStmtAttr**若要設定，並**SQLGetStmtAttr**若要取得，下列陳述式屬性。 (使用**SQLSetStmtAttr**若要設定，以及**SQLGetStmtAttr**若要取得，其他陳述式屬性是重複的、 未新增的功能。)  
  
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
  
-   善用**SQLGetStmtAttr**取得下列陳述式屬性。 (使用**SQLGetStmtAttr**以取得其他陳述式屬性是重複的功能，而不是新的功能。)  
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   使用間隔 C 資料類型、 間隔 SQL 資料類型、 BIGINT C 資料類型和 SQL_C_NUMERIC 資料結構。  
  
-   資料列取向的繫結的參數。  
  
-   位移為基礎的書籤提取，例如呼叫**SQLFetchScroll**具有*Sqlfetchscroll*引數，以及要使用 SQL_FETCH_BOOKMARK 指定 0 以外的位移。  
  
-   **SQLFetch**傳回的資料列狀態陣列，擷取的資料列，擷取多個資料列，使用混合的呼叫數字**SQLFetchScroll**，並使用混合的呼叫**SQLBulkOperations**或**SQLSetPos**。 如需詳細資訊，請參閱下一步 區段中，[區塊資料指標、 可捲動的資料指標和 ODBC 3.x 應用程式的回溯相容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)。  
  
-   具名的參數。  
  
-   任何 ODBC *3.x*-特定**SQLGetInfo**選項。 (如果 ODBC *3.x*應用程式使用 ODBC *2.x*驅動程式會呼叫 SQL_XXX_CURSOR_ATTRIBUTES1 資訊型別，已取代數個 ODBC *2.x*資訊類型的部分資訊可能可靠，但某些可能不可靠。 如需詳細資訊，請參閱 < [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)。)  
  
-   繫結的位移。  
  
-   更新、 重新整理，以及刪除書籤 (透過呼叫**SQLBulkOperations**)。  
  
-   呼叫**SQLBulkOperations**或是**SQLSetPos** S5 狀態中。  
  
-   中的診斷記錄的 ROW_NUMBER 和 R1C1 欄位 (具有要擷取的取代函式**SQLGetDiagField**或是**SQLGetDiagRec**)。  
  
-   大約的資料列計數。  
  
-   警告資訊 (從 SQL_ROW_SUCCESS_WITH_INFO **SQLFetchScroll**)。  
  
-   可變長度的書籤。  
  
-   擴充的錯誤資訊陣列的參數。  
  
-   所有目錄函式所傳回之結果集內的新資料行。  
  
-   利用**SQLDescribeCol**並**SQLColAttribute** 0 的資料行上。  
  
-   使用任何 ODBC *3.x*-的呼叫中的特定資料行屬性**SQLColAttribute**。  
  
-   使用多個環境控制代碼。  
  
 本章節包含下列主題。  
  
-   [適用於 ODBC 3.x 應用程式的區塊資料指標、可捲動的資料指標和回溯相容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
