---
title: "驅動程式的用途 |Microsoft 文件"
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
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: 75dcdea6-ff6b-4ac8-aa11-a1f9edbeb8e6
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 07e94046370f8140fdacec2cf708de0a62311a27
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="what-the-driver-does"></a>驅動程式的用途
下表摘要說明哪些函式和陳述式屬性 ODBC 3*.x*驅動程式應該實作區塊和可捲動資料指標。  
  
|函式或<br /><br /> 陳述式屬性|註解|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR 設定|設定資料列狀態陣列的地址填入**SQLFetch**和**SQLFetchScroll**。 這個陣列也會填入**SQLSetPos**如果**SQLSetPos**稱為 S6 處於陳述式。 如果**SQLSetPos**稱為處於 S7 時，這個陣列不填滿但所指陣列*RowStatusArray*引數的**SQLExtendedFetch**填滿。 如需詳細資訊，請參閱[陳述式轉換](../../../odbc/reference/appendixes/statement-transitions.md)附錄 b: ODBC 狀態轉換表中。|  
|SQL_ATTR_ROWS_FETCHED_PTR|在其中設定緩衝區的位址**SQLFetch**和**SQLFetchScroll**傳回提取的資料列數目。 如果**SQLExtendedFetch**是呼叫，這個緩衝區未填入但*RowCountPtr*引數指向提取的資料列數目。|  
|SQL_ATTR_ROW_ARRAY_SIZE|設定所使用的資料列集大小**SQLFetch**和**SQLFetchScroll**。|  
|SQL_ROWSET_SIZE|設定所使用的資料列集大小**SQLExtendedFetch**。 ODBC 3*.x*驅動程式會實作此如果他們想要使用的 ODBC 2。*x*呼叫的應用程式**SQLExtendedFetch**或**SQLSetPos**。|  
|**SQLBulkOperations**|如果 ODBC 3*.x*驅動程式應該可以搭配 ODBC 2。*x*使用的應用程式**SQLSetPos**與*作業*SQL_ADD，驅動程式必須支援**SQLSetPos**與*作業*的除了 SQL_ADD **SQLBulkOperations**與*作業*SQL_ADD。|  
|**SQLExtendedFetch**|傳回指定的資料列集。 ODBC 3*.x*驅動程式會實作此如果他們想要使用的 ODBC 2。*x*呼叫的應用程式**SQLExtendedFetch**或**SQLSetPos**。 以下是實作詳細資料：<br /><br /> -驅動程式會從 SQL_ROWSET_SIZE 陳述式屬性的值中擷取資料列集大小。<br />-驅動程式會擷取資料列狀態陣列，從位址*RowStatusArray*引數，不將 sql_attr_row_status_ptr 設定陳述式屬性。 *RowStatusArray*呼叫中的引數**SQLExtendedFetch**不能是 null 指標。 (請注意，在 ODBC 3*.x*，SQL_ATTR_ROW_STATUS_PTR 陳述式屬性可以是 null 指標。)<br />-驅動程式會擷取資料列提取緩衝區中的位址*RowCountPtr*引數，不將 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性。<br />-驅動程式會傳回 SQLSTATE 01S01 （資料列中的錯誤），表示呼叫提取資料列時發生錯誤**SQLExtendedFetch**。 ODBC 3*.x*驅動程式應該會傳回 SQLSTATE 01S01 （資料列中的錯誤） 時，才**SQLExtendedFetch**呼叫時，沒有當**SQLFetch**或**SQLFetchScroll**呼叫。 若要保留回溯相容性，當 SQLSTATE 01S01 （資料列中的錯誤） 由**SQLExtendedFetch**，驅動程式管理員不會排序狀態記錄中錯誤佇列，根據 「 序列的狀態中所述的規則記錄 」 一節[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。|  
|**SQLFetch**|傳回下一個資料列集。 以下是實作詳細資料：<br /><br /> -驅動程式會從 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性的值中擷取資料列集大小。<br />-驅動程式會從 SQL_ATTR_ROW_STATUS_PTR 陳述式屬性擷取資料列狀態陣列的位址。<br />-驅動程式會擷取從 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性擷取緩衝區的資料列的位址。<br />-應用程式可以混合之間的呼叫**SQLFetchScroll**和**SQLFetch**。<br />-   **SQLFetch**傳回書籤，如果繫結資料行 0。<br />-   **SQLFetch**可以呼叫以傳回多個資料列。<br />-驅動程式不會傳回 SQLSTATE 01S01 （資料列中的錯誤），表示呼叫提取資料列時發生錯誤**SQLFetch**。|  
|**SQLFetchScroll**|傳回指定的資料列集。 以下是實作詳細資料：<br /><br /> -驅動程式會從 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性擷取的資料列集大小。<br />-驅動程式會從 SQL_ATTR_ROW_STATUS_PTR 陳述式屬性擷取資料列狀態陣列的位址。<br />-驅動程式會擷取從 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性擷取緩衝區的資料列的位址。<br />-應用程式可以混合之間的呼叫**SQLFetchScroll**和**SQLFetch**。<br />-驅動程式不會傳回 SQLSTATE 01S01 （資料列中的錯誤），表示呼叫提取資料列時發生錯誤**SQLFetchScroll**。|  
|**SQLSetPos**|執行各種定位的作業。 以下是實作詳細資料：<br /><br /> -這可以在陳述式狀態 S6 或 S7 呼叫。 如需詳細資訊，請參閱[陳述式轉換](../../../odbc/reference/appendixes/statement-transitions.md)附錄 b: ODBC 狀態轉換表中。<br />-如果這呼叫陳述式狀態 S5 或 S6，驅動程式會擷取資料列集大小從 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性和資料列狀態陣列，從 SQL_ATTR_ROW_STATUS_PTR 陳述式屬性的位址。<br />-如果這呼叫陳述式狀態 S7，驅動程式擷取資料列集大小 SQL_ROWSET_SIZE 陳述式屬性和資料列狀態陣列，從位址*RowStatusArray*引數的**SQLExtendedFetch**。<br />-驅動程式會傳回 SQLSTATE 01S01 （資料列中的錯誤） 要指出呼叫提取資料列時發生錯誤**SQLSetPos**處於 S7 呼叫此函式時執行大量作業。 若要保留回溯相容性，如果 SQLSTATE 01S01 （資料列中的錯誤） 由**SQLSetPos**，驅動程式管理員不會排序在序列的狀態 記錄中所述的規則錯誤佇列中的狀態記錄區段[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。<br />-如果驅動程式應該使用 ODBC 2。*x*呼叫的應用程式**SQLSetPos**與*作業*SQL_ADD 引數，此驅動程式必須支援**SQLSetPos** 與*作業*SQL_ADD 引數。|

