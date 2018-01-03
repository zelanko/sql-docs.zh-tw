---
title: "SQLSetStmtAttr （資料指標程式庫） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLSetStmtAttr function [ODBC], Cursor Library
ms.assetid: 6018a733-c2c8-4047-92ec-92cf85031767
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d707170f7e321ce41d096da6651c0e825621713
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr （資料指標程式庫）
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLSetStmtAttr**資料指標程式庫中的函式。 如需一般資訊**SQLSetStmtAttr**，請參閱[SQLSetStmtAttr 函數](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
 資料指標程式庫支援下列陳述式屬性具有**SQLSetStmtAttr**:  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROWSET_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_SIMULATE_CURSOR|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_USE_BOOKMARKS|  
  
 資料指標程式庫僅支援 SQL_CURSOR_FORWARD_ONLY 和 SQL_CURSOR_STATIC 值的 SQL_ATTR_CURSOR_TYPE 陳述式屬性。  
  
 順向資料指標的資料指標程式庫支援陳述式屬性 SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY 的值。 對靜態資料指標，資料指標程式庫支援陳述式屬性 SQL_ATTR_CONCURRENCY 的 SQL_CONCUR_READ_ONLY、 SQL_CONCUR_VALUES 值。  
  
 資料指標程式庫支援只 SQL_SC_NON_UNIQUE SQL_ATTR_SIMULATE_CURSOR 陳述式屬性值。  
  
 雖然 ODBC 規格支援呼叫**SQLSetStmtAttr** SQL_ATTR_PARAM_BIND_TYPE 或 SQL_ATTR_ROW_BIND_TYPE 屬性之後**SQLFetch**或**SQLFetchScroll**已經呼叫，資料指標程式庫並不會。 它可以變更繫結類型在資料指標程式庫之前，應用程式必須關閉資料指標。 資料指標程式庫支援變更 SQL_ATTR_ROW_BIND_OFFSET_PTR、 SQL_ATTR_PARAM_BIND_OFFSET_PTR、 SQL_ATTR_ROWS_FETCHED_PTR，且 SQL_ATTR_PARAMS_PROCESSED_PTR 陳述式屬性的資料指標已開啟。  
  
 應用程式可以呼叫**SQLSetStmtAttr**與**屬性**的 SQL_ATTR_ROW_ARRAY_SIZE 來開啟資料指標時，變更資料列集大小。 新的資料列集大小將會在下一次生效**SQLFetchScroll**或**SQLFetch**呼叫。  
  
 資料指標程式庫支援的設定，以啟用繫結位移 SQL_ATTR_PARAM_BIND_OFFSET_PTR 或 SQL_ATTR_ROW_BIND_OFFSET_PTR 陳述式屬性。 繫結位移不能用於呼叫**SQLFetch**當資料指標程式庫搭配 ODBC 2。*x*驅動程式。  
  
 資料指標程式庫支援將 SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_VARIABLE。
