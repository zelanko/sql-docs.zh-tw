---
description: 擷取的資料列數目和狀態
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
ms.openlocfilehash: bc328aab77d6e59db258c463a7dae1554f7d4c11
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429210"
---
# <a name="number-of-rows-fetched-and-status"></a>擷取的資料列數目和狀態
如果已設定 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性，它會指定一個緩衝區來傳回 **SQLFetch** 或 **SQLFetchScroll**的呼叫所提取的資料列數目，以及錯誤資料列。  (此數位為沒有狀態 SQL_ROW_NO_ROWS 的所有資料列計數 ) 。在呼叫 **SQLBulkOperations** 或 **SQLSetPos**之後，緩衝區會包含受函數所執行的大量作業所影響的資料列數目。 如果已設定 SQL_ATTR_ROW_STATUS_PTR 語句屬性， **SQLFetch** 或 **SQLFetchScroll** 會傳回資料 *列狀態陣列，* 以提供每個傳回資料列的狀態。 這些欄位所指向的兩個緩衝區都是由應用程式佈建，並由驅動程式填入。 應用程式必須確定這些指標會維持有效，直到資料指標關閉為止。  
  
 資料列狀態陣列中的專案會指出是否已成功提取每個資料列、是否要在最後一次提取之後更新、加入或刪除資料列，以及是否在提取資料列時發生錯誤。 如果 **SQLFetch** 或 **SQLFetchScroll** 在抓取多資料列資料列集的一個資料列時發生錯誤，或如果 **SQLBulkOperations** 具有 *SQL_FETCH_BY_BOOKMARK 的作業引數* ，則會在執行大量提取時發生錯誤，它會將資料列狀態陣列中的對應值設定為 SQL_ROW_ERROR、繼續提取資料列，並傳回 SQL_SUCCESS_WITH_INFO。 如需錯誤處理和資料列狀態陣列的詳細資訊，請參閱 [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md) 和 [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) 函數描述。
