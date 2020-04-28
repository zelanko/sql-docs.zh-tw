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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1bdd9b3b559d5cc78a0d44f5280aae347bc8996a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300488"
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr (資料指標程式庫)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用**SQLSetStmtAttr**函數。 如需有關**SQLSetStmtAttr**的一般資訊，請參閱[SQLSetStmtAttr 函數](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
 資料指標程式庫支援下列語句屬性搭配**SQLSetStmtAttr**：  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROWSET_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_SIMULATE_CURSOR|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_USE_BOOKMARKS|  
  
 資料指標程式庫僅支援 SQL_ATTR_CURSOR_TYPE 語句屬性的 SQL_CURSOR_FORWARD_ONLY 和 SQL_CURSOR_STATIC 值。  
  
 對於順向資料指標而言，資料指標程式庫支援 SQL_ATTR_CONCURRENCY 語句屬性的 SQL_CONCUR_READ_ONLY 值。 若為靜態資料指標，資料指標程式庫支援 SQL_ATTR_CONCURRENCY 語句屬性的 SQL_CONCUR_READ_ONLY 和 SQL_CONCUR_VALUES 值。  
  
 資料指標程式庫僅支援 SQL_ATTR_SIMULATE_CURSOR 語句屬性的 SQL_SC_NON_UNIQUE 值。  
  
 雖然在呼叫**SQLFetch**或**SQLFETCHSCROLL**之後，ODBC 規格支援使用 SQL_ATTR_PARAM_BIND_TYPE 或 SQL_ATTR_ROW_BIND_TYPE 屬性的呼叫**SQLSetStmtAttr** ，但資料指標程式庫並不會。 應用程式必須先關閉資料指標，才可以變更資料指標程式庫中的系結類型。 當資料指標開啟時，資料指標程式庫支援變更 SQL_ATTR_ROW_BIND_OFFSET_PTR、SQL_ATTR_PARAM_BIND_OFFSET_PTR、SQL_ATTR_ROWS_FETCHED_PTR 和 SQL_ATTR_PARAMS_PROCESSED_PTR 語句屬性。  
  
 應用程式可以使用 SQL_ATTR_ROW_ARRAY_SIZE 的**屬性**來呼叫**SQLSetStmtAttr** ，以在資料指標開啟時變更資料列集大小。 新的資料列集大小將在下一次呼叫**SQLFetchScroll**或**SQLFetch**時生效。  
  
 資料指標程式庫支援設定 SQL_ATTR_PARAM_BIND_OFFSET_PTR 或 SQL_ATTR_ROW_BIND_OFFSET_PTR 語句屬性，以啟用系結位移。 當資料指標程式庫與 ODBC 2 搭配使用時，系結位移不會用於**SQLFetch**的呼叫。*x*驅動程式。  
  
 資料指標程式庫支援將 SQL_ATTR_USE_BOOKMARKS 語句屬性設定為 SQL_UB_VARIABLE。
