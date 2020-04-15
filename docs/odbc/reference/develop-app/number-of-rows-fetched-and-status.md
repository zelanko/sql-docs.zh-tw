---
title: 已提取的行數和狀態 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302359"
---
# <a name="number-of-rows-fetched-and-status"></a>擷取的資料列數目和狀態
如果已設置SQL_ATTR_ROWS_FETCHED_PTR語句屬性,它將指定一個緩衝區,該緩衝區返回調用**SQLFetch**或**SQLFetchScroll**獲取的行數,以及錯誤行。 (此數位是未SQL_ROW_NO_ROWS狀態的所有行的計數。調用**SQLBulk 操作**或**SQLSetPos**後,緩衝區包含受函數執行的批量操作影響的行數。 如果設置了SQL_ATTR_ROW_STATUS_PTR語句屬性 **,SQLFetch**或**SQLFetchScroll**將返回*行狀態陣列,該陣組*提供每個返回行的狀態。 這些欄位指向的兩個緩衝區都由應用程式分配並由驅動程式填充。 應用程式必須確保這些指標保持有效,直到游標關閉。  
  
 行狀態陣列中的條目狀態每行是否成功提取,自上次提取行以來是否更新、添加或刪除,以及獲取行時是否發生錯誤。 如果**SQLFetch**或**SQLScroll**在檢索多行行集的一行時遇到錯誤,或者如果具有*操作*參數的**SQLBulk 操作**SQL_FETCH_BY_BOOKMARK在執行批量提取時遇到錯誤,則它將行狀態陣列中的相應值設置為SQL_ROW_ERROR,繼續提取行,並返回SQL_SUCCESS_WITH_INFO。 有關錯誤處理和行狀態陣列的詳細資訊,請參閱[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)和[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)函數說明。
