---
title: "擷取資料列數目以及狀態 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- row status array [ODBC]
- number of rows fetched [ODBC]
- result sets [ODBC], row status array
ms.assetid: a069b979-5108-4905-932f-8ae8e7905ff2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3e79fec9836fb7a6528bea63c78a8e6479dac8e1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="number-of-rows-fetched-and-status"></a>提取的資料列的數目和狀態
如果已設定 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性，它會指定傳回的呼叫所提取的資料列數目的緩衝區**SQLFetch**或**SQLFetchScroll**，和錯誤資料列。 （這個號碼是沒有狀態 SQL_ROW_NO_ROWS 的所有資料列計數）。若要在呼叫之後**SQLBulkOperations**或**SQLSetPos**，緩衝區會包含由函式執行的大量作業所影響的資料列數目。 如果已設定 SQL_ATTR_ROW_STATUS_PTR 陳述式屬性， **SQLFetch**或**SQLFetchScroll**傳回*資料列狀態陣列，*這樣會提供每個狀態傳回的資料列。 這些欄位所指向之緩衝區兩者都是由應用程式所配置，而且驅動程式所填入。 應用程式必須確定這些指標保持有效，直到關閉資料指標。  
  
 在資料列狀態陣列狀態是否更新時，是否成功，提取每個資料列加入，或刪除項目自上一次提取，以及是否提取資料列時發生錯誤。 如果**SQLFetch**或**SQLFetchScroll**遭遇錯誤時擷取一個資料列的多重資料列的資料列集，或如果**SQLBulkOperations**與*作業* SQL_FETCH_BY_BOOKMARK 引數執行大量擷取時遇到錯誤，SQL_ROW_ERROR 資料列狀態陣列中設定對應的值，會繼續提取資料列，並會傳回 SQL_SUCCESS_WITH_INFO。 如需有關錯誤處理和資料列狀態陣列的詳細資訊，請參閱[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)和[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)函式描述。

