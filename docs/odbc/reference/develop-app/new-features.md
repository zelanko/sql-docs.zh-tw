---
description: 新功能
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
ms.openlocfilehash: 2015d424e0c755352fa66f3ac67503b612b6982f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429230"
---
# <a name="new-features"></a>新功能
ODBC 3.x 引進了下列新*功能。* 使用*odbc 2.x* *驅動程式的 odbc 3.x 應用程式*將無法使用此功能。 *Odbc 2.x 驅動程式*管理員在*使用 odbc 2.x*驅動程式時，不會對應這些功能。  
  
-   採用描述項控制碼作為引數的函式： **SQLSetDescField**、 **SQLGetDescField**、 **SQLSetDescRec**、 **SQLGetDescRec**和 **SQLCopyDesc**。  
  
-   **SQLSetEnvAttr**和**SQLGetEnvAttr**函數。  
  
-   使用 **SQLAllocHandle** 來配置描述項控制碼。  (使用 **SQLAllocHandle** 來配置環境、連接和語句控制碼是重複的，而不是新的功能。 )   
  
-   使用 **SQLGetConnectAttr** 來取得 SQL_ATTR_AUTO_IPD 的連接屬性。  (使用 **SQLSetConnectAttr** 來設定和 **SQLGetConnectAttr** ，以取得其他連接屬性，而不是新的、功能。 )   
  
-   使用 **SQLSetStmtAttr** 來設定和 **SQLGetStmtAttr** ，以取得下列語句屬性。  (使用 **SQLSetStmtAttr** 來設定和 **SQLGetStmtAttr** 以取得，其他語句屬性會重複，而不是新的功能。 )   
  
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
  
-   使用 **SQLGetStmtAttr** 來取得下列語句屬性。  (使用 **SQLGetStmtAttr** 來取得其他語句屬性是重複的功能，而不是新的功能。 )   
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   使用 interval C 資料類型、SQL 資料類型的間隔、BIGINT C 資料類型，以及 SQL_C_NUMERIC 資料結構。  
  
-   參數的資料列取向系結。  
  
-   以位移為基礎的書簽提取，例如使用 SQL_FETCH_BOOKMARK 的*FetchOrientation*引數來呼叫**SQLFetchScroll** ，並指定0以外的位移。  
  
-   **SQLFetch** 傳回資料列狀態陣列、提取的資料列數目、提取多個資料列、使用 **SQLFetchScroll**的混合呼叫，以及使用 **SQLBulkOperations** 或 **SQLSetPos**的混合呼叫。 如需詳細資訊，請參閱下一節： [ODBC 3.X 應用程式的區塊資料指標、可滾動的資料指標和回溯相容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)。  
  
-   具名引數。  
  
-   任何 *ODBC 3.x 特定的* **SQLGetInfo** 選項。  (如果 ODBC 3.x*應用程式**使用 odbc 2.x*驅動程式來呼叫已取代數個 ODBC 2.x 資訊類型的 SQL_XXX_CURSOR_ATTRIBUTES1 資訊類型，部分*資訊可能*是可靠的，但有些可能不可靠。 如需詳細資訊，請參閱 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)。 )   
  
-   系結位移。  
  
-    (透過呼叫 **SQLBulkOperations**) 來更新、重新整理及刪除書簽。  
  
-   以 S5 狀態呼叫 **SQLBulkOperations** 或 **SQLSetPos** 。  
  
-   診斷記錄 (中的 [ROW_NUMBER] 和 [COLUMN_NUMBER] 欄位，必須由取代函式 **SQLGetDiagField** 或 **SQLGetDiagRec**) 取出。  
  
-   大約的資料列計數。  
  
-   從 **SQLFetchScroll**) SQL_ROW_SUCCESS_WITH_INFO 的警告資訊 (。  
  
-   可變長度的書簽。  
  
-   參數陣列的延伸錯誤資訊。  
  
-   目錄函數所傳回之結果集中的所有新資料行。  
  
-   在資料行0上使用 **SQLDescribeCol** 和 **SQLColAttribute** 。  
  
-   在**SQLColAttribute**的呼叫中使用*任何 ODBC 3.x 特定的資料*行屬性。  
  
-   使用多個環境控制碼。  
  
 本節包含下列主題。  
  
-   [適用於 ODBC 3.x 應用程式的區塊資料指標、可捲動的資料指標和回溯相容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
