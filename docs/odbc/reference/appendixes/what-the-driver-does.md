---
description: 驅動程式的用途
title: 驅動程式的功能 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: 75dcdea6-ff6b-4ac8-aa11-a1f9edbeb8e6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4f15473d1eb0e6344fbd5772f2b28233c07aa7a3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386224"
---
# <a name="what-the-driver-does"></a>驅動程式的用途
下表摘要 *說明 ODBC 3.x* 驅動程式應針對區塊和可滾動資料指標執行的函數和語句屬性。  
  
|函數或<br /><br /> 陳述式屬性|註解|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR|設定 **SQLFetch** 和 **SQLFetchScroll**填入的資料列狀態陣列位址。 如果在語句狀態 S6 中呼叫**SQLSetPos** ，這個陣列也會由**SQLSetPos**填滿。 如果在狀態 S7 中呼叫**SQLSetPos** ，則不會填入此陣列，但是會填入**SQLExtendedFetch**的*RowStatusArray*引數所指向的陣列。 如需詳細資訊，請參閱附錄 B： ODBC 狀態轉換資料表中的 [語句轉換](../../../odbc/reference/appendixes/statement-transitions.md) 。|  
|SQL_ATTR_ROWS_FETCHED_PTR|設定緩衝區的位址，其中 **SQLFetch** 和 **SQLFetchScroll** 會傳回所提取的資料列數目。 如果呼叫 **SQLExtendedFetch** ，則不會填入這個緩衝區，而 *RowCountPtr* 引數會指向提取的資料列數目。|  
|SQL_ATTR_ROW_ARRAY_SIZE|設定 **SQLFetch** 和 **SQLFetchScroll**所使用的資料列集大小。|  
|SQL_ROWSET_SIZE|設定 **SQLExtendedFetch**所使用的資料列集大小。 如果 ODBC 3.x 驅動程式想要使用會呼叫**SQLExtendedFetch**或**SQLSetPos**的*ODBC 2.x* *應用程式，* 則會執行此作業。|  
|**SQLBulkOperations**|如果 ODBC 3.x*驅動程式*應該搭配使用**SQLSetPos**與作業 SQL_ADD 的 odbc 2.x 應用程式搭配使用， *Operation*則除了具有 SQL_ADD 作業的**SQLBulkOperations**之外，驅動程式還必須支援具有*2.x* SQL_ADD *Operation* *作業的* **SQLSetPos** 。|  
|**SQLExtendedFetch**|傳回指定的資料列集。 如果 ODBC 3.x 驅動程式想要使用會呼叫**SQLExtendedFetch**或**SQLSetPos**的*ODBC 2.x* *應用程式，* 則會執行此作業。 以下是執行詳細資料：<br /><br /> -驅動程式會從 SQL_ROWSET_SIZE 語句屬性的值抓取資料列集大小。<br />-驅動程式會從 *RowStatusArray* 引數抓取資料列狀態陣列的位址，而不是 SQL_ATTR_ROW_STATUS_PTR 語句屬性。 呼叫**SQLExtendedFetch**的*RowStatusArray*引數不得為 null 指標。  (請 *注意，在 ODBC 3.x*中，SQL_ATTR_ROW_STATUS_PTR 語句屬性可以是 null 指標。 ) <br />-驅動程式會從 *RowCountPtr* 引數抓取資料列提取緩衝區的位址，而不是 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性。<br />-驅動程式會在資料列) 中傳回 SQLSTATE 01S01 (錯誤，指出在呼叫 **SQLExtendedFetch**時提取資料列時發生錯誤。 只有在呼叫**SQLExtendedFetch**時 *，ODBC 3.x*驅動程式應該會在資料列) 中傳回 SQLSTATE 01S01 (錯誤，而不應傳回**SQLFetch**或**SQLFetchScroll** 。 為了保留回溯相容性，當 **SQLExtendedFetch**傳回資料列) 中的 SQLSTATE 01S01 (錯誤時，驅動程式管理員不會根據 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)的「狀態記錄的順序」一節中所述的規則來排序錯誤佇列中的狀態記錄。|  
|**SQLFetch**|傳回下一個資料列集。 以下是執行詳細資料：<br /><br /> -驅動程式會從 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性的值抓取資料列集大小。<br />-驅動程式會從 SQL_ATTR_ROW_STATUS_PTR 語句屬性抓取資料列狀態陣列的位址。<br />-驅動程式會從 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性抓取資料列提取緩衝區的位址。<br />-應用程式可以混合 **SQLFetchScroll** 與 **SQLFetch**之間的呼叫。<br />-   如果資料行0系結， **SQLFetch**會傳回書簽。<br />-   您可以呼叫**SQLFetch** ，以傳回一個以上的資料列。<br />-此驅動程式不會傳回資料列) 中的 SQLSTATE 01S01 (錯誤，表示在呼叫 **SQLFetch**時提取資料列時發生錯誤。|  
|**SQLFetchScroll**|傳回指定的資料列集。 以下是執行詳細資料：<br /><br /> -驅動程式會從 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性抓取資料列集大小。<br />-驅動程式會從 SQL_ATTR_ROW_STATUS_PTR 語句屬性抓取資料列狀態陣列的位址。<br />-驅動程式會從 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性抓取資料列提取緩衝區的位址。<br />-應用程式可以混合 **SQLFetchScroll** 與 **SQLFetch**之間的呼叫。<br />-此驅動程式不會傳回資料列) 中的 SQLSTATE 01S01 (錯誤，表示在呼叫 **SQLFetchScroll**時提取資料列時發生錯誤。|  
|**SQLSetPos**|執行各種定位作業。 以下是執行詳細資料：<br /><br /> -這可以在語句狀態 S6 或 S7 中呼叫。 如需詳細資訊，請參閱附錄 B： ODBC 狀態轉換資料表中的 [語句轉換](../../../odbc/reference/appendixes/statement-transitions.md) 。<br />-如果在語句狀態 S5 或 S6 中呼叫這項功能，驅動程式會從 SQL_ATTR_ROW_STATUS_PTR 語句屬性的 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性和資料列狀態陣列的位址抓取資料列集大小。<br />-如果這是在語句狀態 S7 中呼叫，驅動程式會從**SQLExtendedFetch**的*RowStatusArray*引數中，從 SQL_ROWSET_SIZE 語句屬性和資料列狀態陣列的位址抓取資料列集大小。<br />-驅動程式會在資料列) 中傳回 SQLSTATE 01S01 (錯誤，以指出當呼叫 **SQLSetPos** 來提取資料列時，如果在狀態 S7 中呼叫該函式，就會發生錯誤。 為了保留回溯相容性，如果 **SQLSetPos**傳回資料列) 中的 SQLSTATE 01S01 (錯誤，則驅動程式管理員不會根據 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)的「狀態記錄的順序」一節中所述的規則來排序錯誤佇列中的狀態記錄。<br />-如果驅動程式應該搭配使用 SQL_ADD 之作業引數呼叫**SQLSetPos** *的 ODBC 2.x*應用程式使用，則驅動程式必須支援*SQL_ADD 的作業**引數來*進行**SQLSetPos** 。|
