---
title: SQLSetStmtAttr （資料指標程式庫） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtAttr function [ODBC], Cursor Library
ms.assetid: 6018a733-c2c8-4047-92ec-92cf85031767
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7d4e5bd6ec27891e80933dfcc42beec9056d2d3a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62735206"
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr (資料指標程式庫)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLSetStmtAttr**資料指標程式庫中的函式。 如需一般資訊**SQLSetStmtAttr**，請參閱[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
 資料指標程式庫支援下列陳述式屬性具有**SQLSetStmtAttr**:  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROWSET_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_SIMULATE_CURSOR|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_USE_BOOKMARKS|  
  
 資料指標程式庫僅支援 SQL_CURSOR_FORWARD_ONLY 和 SQL_CURSOR_STATIC 值的 SQL_ATTR_CURSOR_TYPE 陳述式屬性。  
  
 順向資料指標，資料指標程式庫支援 SQL_CONCUR_READ_ONLY SQL_ATTR_CONCURRENCY 陳述式屬性值。 對靜態資料指標，資料指標程式庫支援的 SQL_CONCUR_READ_ONLY、 SQL_CONCUR_VALUES 值 SQL_ATTR_CONCURRENCY 陳述式屬性。  
  
 資料指標程式庫支援只 SQL_SC_NON_UNIQUE SQL_ATTR_SIMULATE_CURSOR 陳述式屬性值。  
  
 雖然 ODBC 規格支援呼叫**SQLSetStmtAttr**含有 SQL_ATTR_PARAM_BIND_TYPE 或 SQL_ATTR_ROW_BIND_TYPE 屬性之後**SQLFetch**或**SQLFetchScroll**已呼叫資料指標程式庫則否。 它可以變更繫結類型在資料指標程式庫之前，應用程式必須關閉資料指標。 資料指標程式庫支援變更 SQL_ATTR_ROW_BIND_OFFSET_PTR、 SQL_ATTR_PARAM_BIND_OFFSET_PTR、 SQL_ATTR_ROWS_FETCHED_PTR，和 SQL_ATTR_PARAMS_PROCESSED_PTR 陳述式屬性的資料指標已經開啟。  
  
 應用程式可以呼叫**SQLSetStmtAttr**具有**屬性**的 SQL_ATTR_ROW_ARRAY_SIZE 來開啟資料指標時，變更資料列集大小。 新的資料列集大小才會生效，下次**SQLFetchScroll**或是**SQLFetch**呼叫。  
  
 資料指標程式庫支援 SQL_ATTR_PARAM_BIND_OFFSET_PTR 或 SQL_ATTR_ROW_BIND_OFFSET_PTR 陳述式將屬性設定為啟用繫結位移。 繫結位移不會用於呼叫**SQLFetch**當資料指標程式庫搭配 ODBC 2。*x*驅動程式。  
  
 資料指標程式庫支援將 SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_VARIABLE。
