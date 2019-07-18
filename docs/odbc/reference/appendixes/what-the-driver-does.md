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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5f27efed55a2ae63b8c3726263077441bdacc49b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135723"
---
# <a name="what-the-driver-does"></a>驅動程式的用途
下表摘要說明哪些函式和陳述式屬性 ODBC *3.x*驅動程式應該實作區塊的可捲動資料指標。  
  
|函式或<br /><br /> 陳述式屬性|註解|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR|集資料列狀態陣列的位址以填滿**SQLFetch**並**SQLFetchScroll**。 這個陣列也會填入**SQLSetPos**如果**SQLSetPos**稱為 S6 處於陳述式。 如果**SQLSetPos**稱為在 S7 狀態下，不會填滿此陣列，但所指陣列*RowStatusArray*引數**SQLExtendedFetch**填滿。 如需詳細資訊，請參閱 <<c0> [ 陳述式轉換](../../../odbc/reference/appendixes/statement-transitions.md)中附錄 b:狀態轉換資料表。|  
|SQL_ATTR_ROWS_FETCHED_PTR|設定緩衝區的地址所在**SQLFetch**並**SQLFetchScroll**傳回提取的資料列數目。 如果**SQLExtendedFetch**是呼叫，這個緩衝區未填入，但*RowCountPtr*引數指向提取的資料列數目。|  
|SQL_ATTR_ROW_ARRAY_SIZE|設定所使用的資料列集大小**SQLFetch**並**SQLFetchScroll**。|  
|SQL_ROWSET_SIZE|設定所使用的資料列集大小**SQLExtendedFetch**。 ODBC *3.x*如果他們想要使用 ODBC 驅動程式實作此*2.x*呼叫的應用程式**SQLExtendedFetch**或是**SQLSetPos**。|  
|**SQLBulkOperations**|如果 ODBC *3.x*驅動程式應該使用 ODBC *2.x*使用的應用程式**SQLSetPos**具有*作業*的 SQL_ADD，驅動程式必須支援**SQLSetPos**具有*作業*的 SQL_ADD 除了**SQLBulkOperations**具有*作業*的 SQL（_A)。|  
|**SQLExtendedFetch**|傳回指定的資料列集。 ODBC *3.x*如果他們想要使用 ODBC 驅動程式實作此*2.x*呼叫的應用程式**SQLExtendedFetch**或是**SQLSetPos**。 以下是實作詳細資料：<br /><br /> -驅動程式會擷取 SQL_ROWSET_SIZE 陳述式屬性的值中的資料列集大小。<br />-驅動程式會擷取的資料列狀態陣列的地址*RowStatusArray*引數，不是 sql_attr_row_status_ptr 設定陳述式屬性。 *RowStatusArray*呼叫中的引數**SQLExtendedFetch**不能是 null 指標。 (請注意，在 ODBC *3.x*，sql_attr_row_status_ptr 設定陳述式屬性可以是 null 指標。)<br />-驅動程式會擷取從擷取的資料列緩衝區位址*RowCountPtr*引數，不是 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性。<br />-驅動程式會傳回 SQLSTATE 01S01 （資料列中的錯誤），表示呼叫提取資料列時發生錯誤**SQLExtendedFetch**。 ODBC *3.x*驅動程式應該會傳回 SQLSTATE 01S01 （資料列中的錯誤） 時，才**SQLExtendedFetch**呼叫時，不當**SQLFetch**或**SQLFetchScroll**呼叫。 若要保留回溯相容性，當 SQLSTATE 01S01 （資料列中的錯誤） 由**SQLExtendedFetch**，驅動程式管理員不會根據 「 順序的狀態中所述的規則錯誤佇列中排序狀態記錄記錄 」 一節[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。|  
|**SQLFetch**|傳回下一個資料列集。 以下是實作詳細資料：<br /><br /> -驅動程式會擷取 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性的值中的資料列集大小。<br />-驅動程式會擷取 sql_attr_row_status_ptr 設定陳述式屬性中的資料列狀態陣列的位址。<br />-驅動程式會擷取從 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性擷取緩衝區的資料列的位址。<br />-應用程式可以混合使用呼叫之間**SQLFetchScroll**並**SQLFetch**。<br />-   **SQLFetch**傳回書籤，如果繫結資料行 0。<br />-   **SQLFetch**可以呼叫以傳回多個資料列。<br />-驅動程式不會傳回 SQLSTATE 01S01 （資料列中的錯誤），表示呼叫提取資料列時發生錯誤**SQLFetch**。|  
|**SQLFetchScroll**|傳回指定的資料列集。 以下是實作詳細資料：<br /><br /> -驅動程式會擷取 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性中的資料列集大小。<br />-驅動程式會擷取 sql_attr_row_status_ptr 設定陳述式屬性中的資料列狀態陣列的位址。<br />-驅動程式會擷取從 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性擷取緩衝區的資料列的位址。<br />-應用程式可以混合使用呼叫之間**SQLFetchScroll**並**SQLFetch**。<br />-驅動程式不會傳回 SQLSTATE 01S01 （資料列中的錯誤），表示呼叫提取資料列時發生錯誤**SQLFetchScroll**。|  
|**SQLSetPos**|執行各種定位的作業。 以下是實作詳細資料：<br /><br /> -此功能可呼叫陳述式狀態 S6 或 S7 中。 如需詳細資訊，請參閱 <<c0> [ 陳述式轉換](../../../odbc/reference/appendixes/statement-transitions.md)中附錄 b:狀態轉換資料表。<br />-如果這呼叫在陳述式的狀態 S5 或 S6，驅動程式會擷取資料列集大小從 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性和資料列狀態陣列，從 sql_attr_row_status_ptr 設定陳述式屬性的位址。<br />-如果這呼叫陳述式狀態 S7 中，驅動程式擷取資料列集大小 SQL_ROWSET_SIZE 陳述式屬性和資料列狀態陣列，從位址*RowStatusArray*引數**SQLExtendedFetch**。<br />-驅動程式會傳回 SQLSTATE 01S01 （資料列中的錯誤） 只是用來表示呼叫提取資料列時發生錯誤**SQLSetPos**狀態 S7 中呼叫函式時執行大量作業。 若要保留回溯相容性，如果 SQLSTATE 01S01 （資料列中的錯誤） 由**SQLSetPos**，驅動程式管理員不會根據 「 順序的狀態記錄 」 中所述的規則錯誤佇列中排序狀態記錄一節[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。<br />-如果驅動程式應該使用 ODBC *2.x*呼叫的應用程式**SQLSetPos**具有*作業*SQL_ADD 引數，此驅動程式必須支援**SQLSetPos**具有*作業*SQL_ADD 引數。|
