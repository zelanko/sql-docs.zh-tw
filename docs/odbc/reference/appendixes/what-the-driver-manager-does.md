---
title: 驅動程式管理員會 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], backward compatibility
- compatibility [ODBC], driver manager
- ODBC driver manager [ODBC]
- backward compatibility [ODBC], driver manager
ms.assetid: 57f65c38-d9ee-46c8-9051-128224a582c6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f29a40db8b35b5915de1889996e7953b1a8ad3f8
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794076"
---
# <a name="what-the-driver-manager-does"></a>驅動程式管理員的用途
下表摘要說明如何 ODBC *3.x*驅動程式管理員將呼叫對應至 ODBC *2.x*和 ODBC *3.x*驅動程式。  
  
|函式或<br /><br /> 陳述式屬性|註解|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|指向要使用的書籤**SQLFetchScroll**。 以下是實作詳細資料：<br /><br /> -當應用程式在 ODBC 中設定這*2.x*驅動程式，ODBC *3.x*驅動程式管理員會快取它。 它會取值指標，並將值傳遞至 ODBC *2.x*中的驅動程式*FetchOffset*引數**SQLExtendedFetch**當**SQLFetchScroll**應用程式更新版本呼叫。<br />-當應用程式在 ODBC 中設定這*3.x*驅動程式，ODBC *3.x*驅動程式管理員會將傳遞至驅動程式呼叫。|  
|SQL_ATTR_ROW_STATUS_PTR|指向資料列狀態陣列以填滿**SQLFetch**， **SQLFetchScroll**， **SQLBulkOperations**，以及**SQLSetPos**。 以下是實作詳細資料：<br /><br /> -當應用程式在 ODBC 中設定這*2.x*驅動程式，ODBC *3.x*驅動程式管理員會快取其值。 將此值傳遞至 ODBC *2.x*中的驅動程式*RowStatusArray*引數**SQLExtendedFetch**當**SQLFetchScroll**或**SQLFetch**呼叫。<br />-當應用程式在 ODBC 中設定這*3.x*驅動程式，ODBC *3.x*驅動程式管理員會將傳遞至驅動程式呼叫。<br />-處於 S6，如果應用程式設定 sql_attr_row_status_ptr 設定，然後呼叫**SQLBulkOperations** (使用*作業*SQL_ADD 的) 或**SQLSetPos**但是未先呼叫**SQLFetch**或是**SQLFetchScroll**，SQLSTATE HY011 （屬性現在無法設定） 會傳回。|  
|SQL_ATTR_ROWS_FETCHED_PTR|指向的緩衝區**SQLFetch**並**SQLFetchScroll**傳回提取的資料列數目。 以下是實作詳細資料：<br /><br /> -當應用程式在 ODBC 中設定這*2.x*驅動程式，ODBC *3.x*驅動程式管理員會快取其值。 將此值傳遞至 ODBC *2.x*中的驅動程式*RowCountPtr*引數**SQLExtendedFetch**當**SQLFetch**或**SQLFetchScroll**稱為應用程式。<br />-當應用程式在 ODBC 中設定這*3.x*驅動程式，ODBC *3.x*驅動程式管理員會將傳遞至驅動程式呼叫。|  
|SQL_ATTR_ROW_ARRAY_SIZE|設定資料列集大小。 以下是實作詳細資料：<br /><br /> -當應用程式在 ODBC 中設定這*2.x*驅動程式，ODBC *3.x*驅動程式管理員將它對應至 SQL_ROWSET_SIZE 陳述式屬性。<br />-當應用程式在 ODBC 中設定這*3.x*驅動程式，ODBC *3.x*驅動程式管理員會將傳遞至驅動程式呼叫。<br />-當應用程式使用 ODBC *3.x*驅動程式呼叫**SQLSetScrollOptions**，SQL_ROWSET_SIZE 設定中的值為*RowsetSize*引數如果基礎驅動程式不支援**SQLSetScrollOptions**。|  
|SQL_ROWSET_SIZE|設定所使用的資料列集大小**SQLExtendedFetch**當**SQLExtendedFetch** ODBC 呼叫*2.x*應用程式。 以下是實作詳細資料：<br /><br /> -當應用程式設定，ODBC *3.x*驅動程式管理員會傳遞至驅動程式時，驅動程式版本不限的呼叫。<br />-當應用程式使用 ODBC *2.x*驅動程式呼叫**SQLSetScrollOptions**，SQL_ROWSET_SIZE 設定中的值為**RowsetSize**引數。|  
|**SQLBulkOperations**|執行插入作業或更新、 刪除或書籤作業所擷取。 以下是實作詳細資料：<br /><br /> -當應用程式呼叫**SQLBulkOperations**具有*作業*SQL_ADD ODBC 中的*2.x*驅動程式，ODBC *3.x*驅動程式管理員將它對應到**SQLSetPos**具有*作業*SQL_ADD。<br />-使用 ODBC 時*2.x*不支援的驅動程式**SQLSetPos**具有*作業*的 SQL_ADD，ODBC *3.x*驅動程式管理員不會對應**SQLSetPos**與*作業*的 SQL_ADD 來**SQLBulkOperations**具有*作業*的 SQL（_A)。 這是因為**SQLBulkOperations**不能呼叫狀態 S7 中，供在 ODBC *2.x*是唯一的狀態，在其中**SQLSetPos**可能呼叫。<br />-如果應用程式會呼叫**SQLBulkOperations**具有*作業*SQL_ADD ODBC 中的*2.x*驅動程式，然後再呼叫**SQLFetchScroll**，ODBC *3.x*驅動程式管理員會傳回錯誤。|  
|**SQLExtendedFetch**|傳回指定的資料列集。 除了另有註明，只是限制 ODBC *3.x*驅動程式管理員會將傳遞至呼叫**SQLExtendedFetch**驅動程式，不論哪個版本的驅動程式。|  
|**SQLFetch**|傳回下一個資料列集。 以下是實作詳細資料：<br /><br /> -當應用程式呼叫**SQLFetch** ODBC 中*2.x* ODBC 驅動程式*3.x*驅動程式管理員將它對應至**SQLExtendedFetch**。 *Sqlfetchscroll*引數**SQLExtendedFetch**設 SQL_FETCH_NEXT。 驅動程式管理員會使用快取的 sql_attr_row_status_ptr 設定陳述式屬性的值*RowStatusArray*引數和 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性的快取的值*RowCountPtr*引數。<br />-ODBC *3.x*應用程式可以混合使用呼叫**SQLFetch**並**SQLFetchScroll** ODBC 中*2.x*驅動程式因為 ODBC *3.x*驅動程式管理員會將對應**SQLFetch**要**SQLExtendedFetch**當應用程式中的 ODBC 呼叫它*2.x*驅動程式。<br />-如果 ODBC *2.x*驅動程式不支援**SQLExtendedFetch**，ODBC *3.x*驅動程式管理員不會對應**SQLFetch**或**SQLFetchScroll**要**SQLExtendedFetch**當應用程式的驅動程式中呼叫它。 如果應用程式會嘗試將 SQL_ATTR_ROW_ARRAY_SIZE 設定為值大於 1，SQLSTATE HYC00 （選擇性功能未實作） 會傳回。<br />-除了對於另有註明，只是限制 ODBC *3.x*驅動程式管理員會將傳遞至呼叫**SQLFetch**驅動程式，不論哪個版本的驅動程式。|  
|**SQLFetchScroll**|傳回指定的資料列集。 以下是實作詳細資料：<br /><br /> -當應用程式呼叫**SQLFetchScroll** ODBC 中*2.x* ODBC 驅動程式*3.x*驅動程式管理員將它對應至**SQLExtendedFetch**。 它會使用快取的 sql_attr_row_status_ptr 設定陳述式屬性的值*RowStatusArray*引數和 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性的快取的值*RowCountPtr*引數。 如果*Sqlfetchscroll*中的引數**SQLFetchScroll**是要使用 SQL_FETCH_BOOKMARK，它會使用快取的 SQL_ATTR_FETCH_BOOKMARK_PTR 陳述式屬性的值*FetchOffset*引數，並傳回錯誤，如果*FetchOffset*引數**SQLFetchScroll**是不是 0。<br />-當應用程式中的 ODBC 呼叫這*3.x*驅動程式，ODBC *3.x*驅動程式管理員會將傳遞至驅動程式呼叫。|  
|**SQLSetPos**|執行各種定位的作業。 ODBC *3.x*驅動程式管理員會將傳遞至呼叫**SQLSetPos**驅動程式，不論哪個版本的驅動程式。|  
|**SQLSetScrollOptions**|當驅動程式管理員會將對應**SQLSetScrollOptions**應用程式使用 ODBC *3.x*不支援的驅動程式**SQLSetScrollOptions**，驅動程式管理員設定 SQL_ROWSET_SIZE 陳述式選項，而不是 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性， *RowsetSize*中的引數**SQLSetScrollOption**。 如此一來， **SQLSetScrollOptions**呼叫擷取多個資料列時無法由應用程式**SQLFetch**或是**SQLFetchScroll**。 它可以用於擷取多個資料列呼叫時，才**SQLExtendedFetch**。|
