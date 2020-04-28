---
title: 提取的資料列數目和狀態 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 20e1632e8da765b0da2785bd846b67d13ebe01ed
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302359"
---
# <a name="number-of-rows-fetched-and-status"></a>擷取的資料列數目和狀態
如果已設定 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性，它會指定一個緩衝區，傳回**SQLFetch**或**SQLFetchScroll**的呼叫所提取的資料列數，以及錯誤的資料列。 （此數目是所有沒有狀態 SQL_ROW_NO_ROWS 的資料列計數）。呼叫**SQLBulkOperations**或**SQLSetPos**之後，緩衝區會包含受到函數執行之大量作業影響的資料列數目。 如果已設定 SQL_ATTR_ROW_STATUS_PTR 語句屬性， **SQLFetch**或**SQLFetchScroll**會傳回資料*列狀態陣列，* 以提供每個傳回資料列的狀態。 這些欄位所指向的兩個緩衝區都會由應用程式佈建，並由驅動程式填入。 應用程式必須確保這些指標保持有效，直到資料指標關閉為止。  
  
 資料列狀態陣列中的專案會指出每個資料列是否已成功提取、是否已在上次提取之後更新、加入或刪除，以及是否在提取資料列時發生錯誤。 如果**SQLFetch**或**SQLFetchScroll**在抓取多資料列資料列集的一個資料列時發生錯誤，或如果**SQLBulkOperations**的*Operation*引數 SQL_FETCH_BY_BOOKMARK 在執行大量提取時發生錯誤，它會將資料列狀態陣列中對應的值設定為 SQL_ROW_ERROR、繼續提取資料列，然後傳回 SQL_SUCCESS_WITH_INFO。 如需有關錯誤處理和資料列狀態陣列的詳細資訊，請參閱[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)和[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)函數描述。
