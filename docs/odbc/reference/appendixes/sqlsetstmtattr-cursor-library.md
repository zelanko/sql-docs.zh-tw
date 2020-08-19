---
description: SQLSetStmtAttr (資料指標程式庫)
title: SQLSetStmtAttr (資料指標程式庫) |Microsoft Docs
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
ms.openlocfilehash: 96466e354875224c05bef4c94d72249bad9a4cff
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429490"
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr (資料指標程式庫)
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用 **SQLSetStmtAttr** 函數。 如需 **SQLSetStmtAttr**的一般資訊，請參閱 [SQLSetStmtAttr 函數](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
 資料指標程式庫支援下列使用 **SQLSetStmtAttr**的語句屬性：  

:::row:::
    :::column:::
        SQL_ATTR_CONCURRENCY  
        SQL_ATTR_CURSOR_TYPE  
        SQL_ATTR_FETCH_BOOKMARK_PTR  
        SQL_ATTR_PARAM_BIND_OFFSET_PTR  
        SQL_ATTR_PARAM_BIND_TYPE  
    :::column-end:::
    :::column:::
        SQL_ATTR_ROW_BIND_OFFSET_PTR  
        SQL_ATTR_ROW_BIND_TYPE  
        SQL_ATTR_ROWSET_ARRAY_SIZE  
        SQL_ATTR_SIMULATE_CURSOR  
        SQL_ATTR_USE_BOOKMARKS  
    :::column-end:::
:::row-end:::

 資料指標程式庫僅支援 SQL_ATTR_CURSOR_TYPE 語句屬性的 SQL_CURSOR_FORWARD_ONLY 和 SQL_CURSOR_STATIC 值。  
  
 針對順向資料指標，資料指標程式庫支援 SQL_ATTR_CONCURRENCY 語句屬性的 SQL_CONCUR_READ_ONLY 值。 若為靜態資料指標，資料指標程式庫支援 SQL_ATTR_CONCURRENCY 語句屬性的 SQL_CONCUR_READ_ONLY 和 SQL_CONCUR_VALUES 值。  
  
 資料指標程式庫僅支援 SQL_ATTR_SIMULATE_CURSOR 語句屬性的 SQL_SC_NON_UNIQUE 值。  
  
 雖然在呼叫**SQLFetch**或**SQLFETCHSCROLL**之後，ODBC 規格支援使用 SQL_ATTR_PARAM_BIND_TYPE 或 SQL_ATTR_ROW_BIND_TYPE 屬性來呼叫**SQLSetStmtAttr** ，但資料指標程式庫並不支援。 應用程式必須先關閉資料指標，然後才能變更資料指標程式庫中的系結類型。 當資料指標開啟時，資料指標程式庫支援變更 SQL_ATTR_ROW_BIND_OFFSET_PTR、SQL_ATTR_PARAM_BIND_OFFSET_PTR、SQL_ATTR_ROWS_FETCHED_PTR 和 SQL_ATTR_PARAMS_PROCESSED_PTR 語句屬性。  
  
 當資料指標開啟時，應用程式可以呼叫 SQL_ATTR_ROW_ARRAY_SIZE**屬性**的**SQLSetStmtAttr**來變更資料列集大小。 新的資料列集大小會在下一次呼叫 **SQLFetchScroll** 或 **SQLFetch** 時生效。  
  
 資料指標程式庫支援設定 SQL_ATTR_PARAM_BIND_OFFSET_PTR 或 SQL_ATTR_ROW_BIND_OFFSET_PTR 語句屬性以啟用系結位移。 當資料指標程式庫與 ODBC 2 搭配使用時，不會使用系結位移來呼叫 **SQLFetch** 。*x* 驅動程式。  
  
 資料指標程式庫支援將 SQL_ATTR_USE_BOOKMARKS 語句屬性設定為 SQL_UB_VARIABLE。
