---
title: 擷取的資料列的數目和狀態 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- row status array [ODBC]
- number of rows fetched [ODBC]
- result sets [ODBC], row status array
ms.assetid: a069b979-5108-4905-932f-8ae8e7905ff2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab4830ddd56335959dd7049a1dabdcc3a0354213
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149335"
---
# <a name="number-of-rows-fetched-and-status"></a>擷取的資料列數目和狀態
如果尚未設定 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性，它會指定傳回的呼叫所提取的資料列數目的緩衝區**SQLFetch**或是**SQLFetchScroll**，和錯誤資料列。 （此數字是沒有狀態 SQL_ROW_NO_ROWS 的所有資料列計數）。在呼叫之後**SQLBulkOperations**或是**SQLSetPos**，緩衝區會包含由函式執行大量作業所影響的資料列數目。 如果尚未設定 sql_attr_row_status_ptr 設定陳述式屬性， **SQLFetch**或是**SQLFetchScroll**會傳回*資料列狀態陣列，* 以提供每個狀態傳回的資料列。 這兩個這些欄位所指向的緩衝區配置應用程式及驅動程式所填入。 應用程式必須確定這些指標保持有效，直到關閉資料指標。  
  
 資料列狀態陣列狀態中的項目是否已更新是否成功，擷取每個資料列加入，或刪除，因為它一次擷取，以及提取資料列時發生錯誤。 如果**SQLFetch**或**SQLFetchScroll**時發生錯誤擷取一個資料列的多資料列的資料列集，或如果**SQLBulkOperations**具有*作業* SQL_FETCH_BY_BOOKMARK 引數而發生錯誤時執行大量擷取、 SQL_ROW_ERROR 資料列狀態陣列中設定對應的值、 持續擷取資料列，以及會傳回 SQL_SUCCESS_WITH_INFO。 如需有關錯誤處理和資料列狀態陣列的詳細資訊，請參閱 < [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)並[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)函式描述。
