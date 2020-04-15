---
title: SQLSetStmtAttr(游標庫) |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300488"
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr (資料指標程式庫)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 本主題討論在游標庫中使用**SQLSetStmtAttr**函數。 有關**SQLSetStmtAttr**的一般資訊,請參閱[SQLSetStmtAttr 函數](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
 游標庫支援以下文句屬性與**SQLSetStmtAttr**:  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROWSET_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_SIMULATE_CURSOR|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_USE_BOOKMARKS|  
  
 游標庫僅支援SQL_ATTR_CURSOR_TYPE語句屬性SQL_CURSOR_FORWARD_ONLY和SQL_CURSOR_STATIC值。  
  
 對於僅轉發遊標,游標庫支援SQL_ATTR_CONCURRENCY語句屬性SQL_CONCUR_READ_ONLY值。 對於靜態游標,游標庫支援SQL_ATTR_CONCURRENCY語句屬性SQL_CONCUR_READ_ONLY和SQL_CONCUR_VALUES值。  
  
 游標庫僅支援SQL_ATTR_SIMULATE_CURSOR語句屬性SQL_SC_NON_UNIQUE值。  
  
 儘管 ODBC 規範支援在調用**SQLFetch**或**SQLFetchScroll**後使用SQL_ATTR_PARAM_BIND_TYPE或SQL_ATTR_ROW_BIND_TYPE屬性調用**SQLSetStmtAttr,** 但游標庫不支援。 在更改游標庫中的綁定類型之前,應用程式必須關閉游標。 游標庫支援在游標打開時更改SQL_ATTR_ROW_BIND_OFFSET_PTR、SQL_ATTR_PARAM_BIND_OFFSET_PTR、SQL_ATTR_ROWS_FETCHED_PTR和SQL_ATTR_PARAMS_PROCESSED_PTR語句屬性。  
  
 應用程式可以使用SQL_ATTR_ROW_ARRAY_SIZE**屬性**調用**SQLSetStmtAttr,** 以在游標打開時更改行集大小。 下次調用**SQLFetchScroll 或** **SQLFetch**時,新的行集大小將生效。  
  
 游標庫支援設定SQL_ATTR_PARAM_BIND_OFFSET_PTR或SQL_ATTR_ROW_BIND_OFFSET_PTR語句屬性以啟用綁定偏移。 當游標庫與 ODBC 2 一起使用時,綁定偏移量將不用於對**SQLFetch**的調用。*x*驅動程式。  
  
 游標庫支援將SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_VARIABLE。
