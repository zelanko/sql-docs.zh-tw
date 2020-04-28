---
title: 驅動程式的用途 |Microsoft Docs
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
ms.openlocfilehash: c0438478f5aa625ffdd4d3bcd1c0a6f0f80d3367
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301389"
---
# <a name="what-the-driver-does"></a>驅動程式的用途
下表摘要*說明 ODBC 3.x*驅動程式應針對區塊和可滾動資料指標來執行的函數和語句屬性。  
  
|函數或<br /><br /> 陳述式屬性|評價|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR|設定**SQLFetch**和**SQLFetchScroll**填入的資料列狀態陣列位址。 如果在語句狀態 S6 中呼叫了**SQLSetPos** ，此陣列也會填入**SQLSetPos** 。 如果在狀態 S7 中呼叫**SQLSetPos** ，則不會填入此陣列，但會填入**SQLExtendedFetch**的*RowStatusArray*引數所指向的陣列。 如需詳細資訊，請參閱附錄 B： ODBC 狀態轉換資料表中的[語句轉換](../../../odbc/reference/appendixes/statement-transitions.md)。|  
|SQL_ATTR_ROWS_FETCHED_PTR|設定緩衝區的位址，其中**SQLFetch**和**SQLFetchScroll**會傳回所提取的資料列數目。 如果呼叫**SQLExtendedFetch** ，則不會填入這個緩衝區，但是*RowCountPtr*引數會指向提取的資料列數目。|  
|SQL_ATTR_ROW_ARRAY_SIZE|設定**SQLFetch**和**SQLFetchScroll**所使用的資料列集大小。|  
|SQL_ROWSET_SIZE|設定**SQLExtendedFetch**所使用的資料列集大小。 如果您想要使用呼叫**SQLExtendedFetch**或**SQLSetPos***的 odbc 2.X*應用程式，則 odbc *3.x 驅動程式*會執行此作業。|  
|**SQLBulkOperations**|如果 ODBC 3.x*驅動程式*應該搭配使用**SQLSetPos**與 SQL_ADD 作業的 odbc 2.x*應用程式*一起運作，此驅動程式必須支援具有 SQL_ADD*作業的* **SQLSetPos** ，以及具有 SQL_ADD*作業的* **SQLBulkOperations** 。 *Operation*|  
|**SQLExtendedFetch**|傳回指定的資料列集。 如果您想要使用呼叫**SQLExtendedFetch**或**SQLSetPos***的 odbc 2.X*應用程式，則 odbc *3.x 驅動程式*會執行此作業。 以下是執行詳細資料：<br /><br /> -驅動程式會從 SQL_ROWSET_SIZE 語句屬性的值抓取資料列集大小。<br />-驅動程式會從*RowStatusArray*引數抓取資料列狀態陣列的位址，而不是從 SQL_ATTR_ROW_STATUS_PTR 語句屬性。 **SQLExtendedFetch**呼叫中的*RowStatusArray*引數不得為 null 指標。 （請*注意，在 ODBC 3.x*中，SQL_ATTR_ROW_STATUS_PTR 語句屬性可以是 null 指標）。<br />-驅動程式會從*RowCountPtr*引數抓取資料列提取緩衝區的位址，而不是從 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性。<br />-驅動程式會傳回 SQLSTATE 01S01 （row 中的錯誤），表示在呼叫**SQLExtendedFetch**來提取資料列時，發生錯誤。 只有在呼叫**SQLExtendedFetch**時，而不是在呼叫**SQLFetch**或**SQLFetchScroll**時 *，ODBC 3.X*驅動程式才應該傳回 SQLSTATE 01S01 （資料列中的錯誤）。 若要保留回溯相容性，當**SQLExtendedFetch**傳回 SQLSTATE 01S01 （資料列中的錯誤）時，驅動程式管理員不會根據[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)的「狀態記錄的順序」一節中所述的規則來排序錯誤佇列中的狀態記錄。|  
|**SQLFetch**|傳回下一個資料列集。 以下是執行詳細資料：<br /><br /> -驅動程式會從 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性的值抓取資料列集大小。<br />-驅動程式會從 SQL_ATTR_ROW_STATUS_PTR 語句屬性中抓取資料列狀態陣列的位址。<br />-驅動程式會從 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性抓取取得緩衝區的資料列位址。<br />-應用程式可以混合**SQLFetchScroll**與**SQLFetch**之間的呼叫。<br />-   如果資料行0已系結，則**SQLFetch**會傳回書簽。<br />-   您可以呼叫**SQLFetch**來傳回多個資料列。<br />-驅動程式不會傳回 SQLSTATE 01S01 （資料列中的錯誤），表示在呼叫**SQLFetch**來提取資料列時，發生錯誤。|  
|**SQLFetchScroll**|傳回指定的資料列集。 以下是執行詳細資料：<br /><br /> -驅動程式會從 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性中抓取資料列集大小。<br />-驅動程式會從 SQL_ATTR_ROW_STATUS_PTR 語句屬性中抓取資料列狀態陣列的位址。<br />-驅動程式會從 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性抓取取得緩衝區的資料列位址。<br />-應用程式可以混合**SQLFetchScroll**與**SQLFetch**之間的呼叫。<br />-驅動程式不會傳回 SQLSTATE 01S01 （資料列中的錯誤），表示在呼叫**SQLFetchScroll**來提取資料列時，發生錯誤。|  
|**SQLSetPos**|執行各種定位作業。 以下是執行詳細資料：<br /><br /> -這可以在語句狀態 S6 或 S7 中呼叫。 如需詳細資訊，請參閱附錄 B： ODBC 狀態轉換資料表中的[語句轉換](../../../odbc/reference/appendixes/statement-transitions.md)。<br />-如果這是在語句狀態 S5 或 S6 中呼叫，驅動程式會從 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性中抓取資料列集大小，並從 SQL_ATTR_ROW_STATUS_PTR 語句屬性中抓取資料列狀態陣列的位址。<br />-如果這是在語句狀態 S7 中呼叫，驅動程式會從**SQLExtendedFetch**的*RowStatusArray*引數中，抓取 SQL_ROWSET_SIZE 語句屬性和資料列狀態陣列位址的資料列集大小。<br />-驅動程式會傳回 SQLSTATE 01S01 （資料列中的錯誤），以指出當呼叫**SQLSetPos**來執行大量作業時，在狀態 S7 中呼叫函數時，發生錯誤。 為了保留回溯相容性，如果**SQLSetPos**傳回 SQLSTATE 01S01 （row 中的錯誤），則驅動程式管理員不會根據[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)的「狀態記錄的順序」一節中所述的規則來排序錯誤佇列中的狀態記錄。<br />-如果驅動程式應該與使用 SQL_ADD 的*作業引數*呼叫**SQLSetPos** *的 ODBC 2.x*應用程式搭配運作，驅動程式必須支援具有 SQL_ADD 之*operation*引數的**SQLSetPos** 。|
