---
title: "驅動程式管理員會 |Microsoft 文件"
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
- driver manager [ODBC], backward compatibility
- compatibility [ODBC], driver manager
- ODBC driver manager [ODBC]
- backward compatibility [ODBC], driver manager
ms.assetid: 57f65c38-d9ee-46c8-9051-128224a582c6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 64c6fb04fe5c5c693da4982e1c12194bc7e42f98
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="what-the-driver-manager-does"></a>驅動程式管理員的功用為何
下表摘要說明如何 ODBC 3*.x*驅動程式管理員將呼叫對應至 ODBC 2。*x*而 ODBC 3.<placeholder>x<*.x*驅動程式。  
  
|函式或<br /><br /> 陳述式屬性|註解|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|指向要使用的書籤**SQLFetchScroll**。 以下是實作詳細資料：<br /><br /> -當應用程式設定在 ODBC 2。*x*驅動程式，而 ODBC 3*.x*驅動程式管理員會快取它。 它會取值指標，並將值傳遞給 ODBC 2。*x*驅動程式*FetchOffset*引數的**SQLExtendedFetch**時**SQLFetchScroll**應用程式稍後呼叫。<br />-當應用程式設定在 ODBC 3*.x*驅動程式，而 ODBC 3*.x*驅動程式管理員會傳遞至驅動程式呼叫。|  
|SQL_ATTR_ROW_STATUS_PTR 設定|指向資料列狀態陣列填入**SQLFetch**， **SQLFetchScroll**， **SQLBulkOperations**，和**SQLSetPos**。 以下是實作詳細資料：<br /><br /> -當應用程式設定在 ODBC 2。*x*驅動程式，而 ODBC 3*.x*驅動程式管理員會快取它的值。 將此值傳遞至 ODBC 2。*x*驅動程式*RowStatusArray*引數的**SQLExtendedFetch**時**SQLFetchScroll**或**SQLFetch**呼叫。<br />-當應用程式設定在 ODBC 3*.x*驅動程式，而 ODBC 3*.x*驅動程式管理員會傳遞至驅動程式呼叫。<br />-在狀態 S6，如果應用程式設定 sql_attr_row_status_ptr 設定，然後呼叫**SQLBulkOperations** (與*作業*的 SQL_ADD) 或**SQLSetPos**情況下先呼叫**SQLFetch**或**SQLFetchScroll**，SQLSTATE HY011 （屬性現在無法設定） 會傳回。|  
|SQL_ATTR_ROWS_FETCHED_PTR|指向的緩衝區**SQLFetch**和**SQLFetchScroll**傳回提取的資料列數目。 以下是實作詳細資料：<br /><br /> -當應用程式設定在 ODBC 2。*x*驅動程式，而 ODBC 3*.x*驅動程式管理員會快取它的值。 將此值傳遞至 ODBC 2。*x*驅動程式*RowCountPtr*引數的**SQLExtendedFetch**時**SQLFetch**或**SQLFetchScroll**呼叫應用程式。<br />-當應用程式設定在 ODBC 3*.x*驅動程式，而 ODBC 3*.x*驅動程式管理員會傳遞至驅動程式呼叫。|  
|SQL_ATTR_ROW_ARRAY_SIZE|設定資料列集大小。 以下是實作詳細資料：<br /><br /> -當應用程式設定在 ODBC 2。*x*驅動程式，而 ODBC 3*.x*驅動程式管理員將其對應至 SQL_ROWSET_SIZE 陳述式屬性。<br />-當應用程式設定在 ODBC 3*.x*驅動程式，而 ODBC 3*.x*驅動程式管理員會傳遞至驅動程式呼叫。<br />-當應用程式使用 ODBC 3*.x*驅動程式呼叫**SQLSetScrollOptions**，SQL_ROWSET_SIZE 設定中的值為*RowsetSize*引數如果基礎驅動程式不支援**SQLSetScrollOptions**。|  
|SQL_ROWSET_SIZE|設定所使用的資料列集大小**SQLExtendedFetch**時**SQLExtendedFetch**呼叫 ODBC 2*.x*應用程式。 以下是實作詳細資料：<br /><br /> -當應用程式設定這個項目，ODBC 3*.x*驅動程式管理員會傳遞至驅動程式時，驅動程式版本不限的呼叫。<br />-當應用程式使用 ODBC 2。*x*驅動程式呼叫**SQLSetScrollOptions**，SQL_ROWSET_SIZE 設定中的值為**RowsetSize**引數。|  
|**SQLBulkOperations**|執行插入作業或更新、 刪除或書籤作業所擷取。 以下是實作詳細資料：<br /><br /> -當應用程式呼叫**SQLBulkOperations**與*作業*的 ODBC 2 SQL_ADD。*x*驅動程式，而 ODBC 3*.x*驅動程式管理員將它對應到**SQLSetPos**與*作業*SQL_ADD。<br />-時使用的 ODBC 2。*x*不支援的驅動程式**SQLSetPos**與*作業*SQL_ADD，ODBC 3 的*.x*驅動程式管理員不會對應**SQLSetPos**與*作業*的 SQL_ADD 至**SQLBulkOperations**與*作業*SQL_ADD。 這是因為**SQLBulkOperations**無法呼叫狀態 S7，哪些中的 ODBC 2。*x*是唯一的狀態，在其中**SQLSetPos**無法呼叫。<br />-如果應用程式呼叫**SQLBulkOperations**與*作業*的 ODBC 2 SQL_ADD。*x*驅動程式，然後再呼叫**SQLFetchScroll**，ODBC 3*.x*驅動程式管理員會傳回錯誤。|  
|**SQLExtendedFetch**|傳回指定的資料列集。 除了限制另有註明，只要 ODBC 3*.x*驅動程式管理員會傳遞至呼叫**SQLExtendedFetch**驅動程式，不論哪個版本的驅動程式。|  
|**SQLFetch**|傳回下一個資料列集。 以下是實作詳細資料：<br /><br /> -當應用程式呼叫**SQLFetch** ODBC 2。*x*驅動程式，而 ODBC 3*.x*驅動程式管理員將它對應到**SQLExtendedFetch**。 *Sqlfetchscroll*引數的**SQLExtendedFetch**設 SQL_FETCH_NEXT。 驅動程式管理員會使用快取的 SQL_ATTR_ROW_STATUS_PTR 陳述式屬性的值*RowStatusArray*引數和 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性的快取的值*RowCountPtr*引數。<br />-ODBC 3*.x*應用程式可以混合呼叫**SQLFetch**和**SQLFetchScroll** ODBC 2。*x*驅動程式因為 ODBC 3*.x*驅動程式管理員會將對應**SQLFetch**至**SQLExtendedFetch**當應用程式的 ODBC 2 中呼叫它。*x*驅動程式。<br />-如果 ODBC 2。*x*驅動程式不支援**SQLExtendedFetch**，ODBC 3*.x*驅動程式管理員未對應**SQLFetch**或**SQLFetchScroll**至**SQLExtendedFetch**當應用程式的驅動程式中呼叫它。 如果應用程式會嘗試將 SQL_ATTR_ROW_ARRAY_SIZE 設定為大於 1，SQLSTATE HYC00 （選擇性功能未實作） 會傳回。<br />-除了用於另有註明，只限制 ODBC 3*.x*驅動程式管理員會傳遞至呼叫**SQLFetch**驅動程式，不論哪個版本的驅動程式。|  
|**SQLFetchScroll**|傳回指定的資料列集。 以下是實作詳細資料：<br /><br /> -當應用程式呼叫**SQLFetchScroll** ODBC 2。*x*驅動程式，而 ODBC 3*.x*驅動程式管理員將它對應到**SQLExtendedFetch**。 它會使用快取的 SQL_ATTR_ROW_STATUS_PTR 陳述式屬性的值*RowStatusArray*引數和 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性的快取的值*RowCountPtr*引數。 如果*Sqlfetchscroll*引數中的**SQLFetchScroll**是要使用 SQL_FETCH_BOOKMARK，它會使用快取的 SQL_ATTR_FETCH_BOOKMARK_PTR 陳述式屬性的值*FetchOffset*引數，並傳回錯誤，如果*FetchOffset*引數的**SQLFetchScroll**是不是 0。<br />-當應用程式會呼叫在 ODBC 3*.x*驅動程式，而 ODBC 3*.x*驅動程式管理員會傳遞至驅動程式呼叫。|  
|**SQLSetPos**|執行各種定位的作業。 ODBC 3*.x*驅動程式管理員會傳遞至呼叫**SQLSetPos**驅動程式，不論哪個版本的驅動程式。|  
|**SQLSetScrollOptions**|當驅動程式管理員會將對應**SQLSetScrollOptions**應用程式使用 ODBC 3*.x*不支援的驅動程式**SQLSetScrollOptions**，驅動程式管理員設定 SQL_ROWSET_SIZE 陳述式選項，而不將 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性， *RowsetSize*引數中的**SQLSetScrollOption**。 如此一來， **SQLSetScrollOptions**不可由應用程式在呼叫提取多個資料列時， **SQLFetch**或**SQLFetchScroll**。 它可以用於擷取多個資料列呼叫時，只有**SQLExtendedFetch**。|

