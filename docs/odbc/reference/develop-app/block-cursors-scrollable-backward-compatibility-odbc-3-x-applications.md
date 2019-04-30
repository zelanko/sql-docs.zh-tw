---
title: 區塊及可捲動資料指標相容性，適用於 ODBC 3.x |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- SQLExtendedFetch function [ODBC], block cursors
- cursors [ODBC], compatibility issues
- SQLFetchScroll function [ODBC], block cursors
ms.assetid: 82f6cf68-cfde-4417-9788-d6382ca14bf8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0bc45169a3c5eee2e23f581a66d5232c22e89b0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199266"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>適用於 ODBC 3.x 應用程式的區塊資料指標、可捲動的資料指標和回溯相容性
兩者的存在**SQLFetchScroll**並**SQLExtendedFetch**表示 ODBC 之間應用程式發展介面 (API)，也就是函式集分割成先清除應用程式呼叫和服務提供者介面 (SPI)，也就是函式集驅動程式實作。 這種分割，才能在 ODBC 3 需求之間取得平衡。*x*，它會使用**SQLFetchScroll**，以符合標準，並使其相容於 ODBC 2。*x*，它會使用**SQLExtendedFetch**。  
  
 ODBC 3 *.x* API，這是一組函式應用程式會呼叫，包括**SQLFetchScroll**和相關的陳述式屬性。 ODBC 3 *.x* SPI，這是集合的函式，驅動程式會實作，包括**SQLFetchScroll**， **SQLExtendedFetch**，以及相關的陳述式屬性。 因為 ODBC 不會正式強制這種分割之間的 API 和 SPI，就可以針對 ODBC 3 *.x*應用程式呼叫**SQLExtendedFetch**和相關的陳述式屬性。 不過，沒有理由針對 ODBC 3 *.x*應用程式，若要這樣做。 如需 Api 和 Spi 的詳細資訊，請參閱 < 簡介[ODBC 架構](../../../odbc/reference/odbc-architecture.md)。  
  
 如需 ODBC 3。*x*驅動程式管理員將呼叫對應至 ODBC 2。*x*和 ODBC 3。*x*驅動程式和函式和陳述式屬性 ODBC 3。*x*驅動程式應該實作的區塊，可捲動資料指標，請參閱[驅動程式的用途](../../../odbc/reference/appendixes/what-the-driver-does.md)在 < 附錄 g:為了與舊版相容的驅動程式指導方針。  
  
 下表摘要說明哪些函式和陳述式屬性 ODBC 3。*x*應用程式應該使用區塊與可捲動資料指標。 它也會列出 ODBC 2 之間的變更。*x*和 ODBC 3。*x*此區域中的 ODBC 3。*x*可與 ODBC 2 相容，應用程式應該要注意。*x*驅動程式。  
  
|函式或<br /><br /> 陳述式屬性|註解|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|指向要使用的書籤**SQLFetchScroll**。<br /><br /> 當應用程式的 ODBC 2 中有設定這個。*x*驅動程式，這必須指向的固定長度書籤。|  
|SQL_ATTR_ROW_STATUS_PTR|指向資料列狀態陣列以填滿**SQLFetch**， **SQLFetchScroll**， **SQLBulkOperations**，以及**SQLSetPos**。<br /><br /> 如果應用程式會設定這個 ODBC 2。*x*驅動程式和呼叫**SQLBulkOperation**具有*作業*的呼叫之前，先 SQL_ADD **SQLFetchScroll**， **SQLFetch**，或**SQLExtendedFetch**，SQLSTATE HY011 （屬性現在無法設定） 會傳回。<br /><br /> 當應用程式呼叫**SQLFetch** ODBC 2。*x*驅動程式， **SQLFetch**會對應至**SQLExtendedFetch** ，因此會傳回此陣列中的值。|  
|SQL_ATTR_ROWS_FETCHED_PTR|指向的緩衝區**SQLFetch**並**SQLFetchScroll**傳回提取的資料列數目。<br /><br /> 當應用程式呼叫**SQLFetch** ODBC 2。*x*驅動程式， **SQLFetch**會對應至**SQLExtendedFetch** ，因此會傳回值，這個緩衝區中。|  
|SQL_ATTR_ROW_ARRAY_SIZE|設定資料列集大小。<br /><br /> 如果應用程式呼叫**SQLBulkOperations**具有*作業*的 ODBC 2 SQL_ADD。*x*驅動程式，SQL_ROWSET_SIZE 將用於呼叫，而不是使用 SQL_ATTR_ROW_ARRAY_SIZE，因為呼叫對應至**SQLSetPos**具有*作業*SQL_ADD，它會使用的SQL_ROWSET_SIZE。<br /><br /> 呼叫**SQLSetPos**具有*作業*SQL_ADD 的或是**SQLExtendedFetch**中的 ODBC 2。*x*驅動程式會使用 SQL_ROWSET_SIZE。<br /><br /> 呼叫**SQLFetch**或是**SQLFetchScroll**中的 ODBC 2。*x*驅動程式會使用 SQL_ATTR_ROW_ARRAY_SIZE。|  
|**SQLBulkOperations**|執行 插入 和 書籤的作業。 當**SQLBulkOperations**具有*作業*SQL_ADD 的呼叫中的 ODBC 2。*x*驅動程式，它會對應到**SQLSetPos**具有*作業*SQL_ADD。 以下是實作詳細資料：<br /><br /> -使用時的 ODBC 2。*x*驅動程式，應用程式必須使用只與相關聯隱含配置的 ARD *StatementHandle*; 它無法配置另一個 ARD 加入資料列，因為明確描述項作業不支援 ODBC 2。*x*驅動程式。 應用程式必須使用**SQLBindCol**未繫結至的 ARD **SQLSetDescField**或是**SQLSetDescRec**。<br />-當呼叫 ODBC 3。*x*驅動程式，應用程式可以呼叫**SQLBulkOperations**具有*作業*的呼叫之前，先 SQL_ADD **SQLFetch**或**SQLFetchScroll**。 當呼叫 ODBC 2。*x*驅動程式，應用程式必須呼叫**SQLFetchScroll**再呼叫**SQLBulkOperations** SQL_ADD 作業使用。|  
|**SQLFetch**|傳回下一個資料列集。 以下是實作詳細資料：<br /><br /> -當應用程式呼叫**SQLFetch** ODBC 2。*x*驅動程式，它會對應到**SQLExtendedFetch**。<br />-當應用程式呼叫**SQLFetch**在 ODBC 3。*x*驅動程式，它會傳回使用 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性指定的資料列數目。|  
|**SQLFetchScroll**|傳回指定的資料列集。 以下是實作詳細資料：<br /><br /> -當應用程式呼叫**SQLFetchScroll** ODBC 2。*x*驅動程式，它會傳回 SQLSTATE 01S01 （資料列中的錯誤） 之前套用至單一資料列的每個錯誤。 這只是因為會 ODBC 3 *.x*驅動程式管理員對應至**SQLExtendedFetch**並**SQLExtendedFetch**會傳回此 SQLSTATE。 當應用程式呼叫**SQLFetchScroll**在 ODBC 3。*x*驅動程式，它不會傳回 SQLSTATE 01S01 （資料列中的錯誤）。<br />-當應用程式呼叫**SQLFetchScroll** ODBC 2。*x*驅動程式搭配*Sqlfetchscroll*設定為要使用 SQL_FETCH_BOOKMARK， *FetchOffset*引數必須設定為 0。 SQLSTATE HYC00 如果位移為基礎的書籤提取會嘗試使用 ODBC 2，則會傳回 （未實作選擇性功能）。*x*驅動程式。|  
  
> [!NOTE]  
>  ODBC 3。*x*應用程式應該不會使用**SQLExtendedFetch**或 SQL_ROWSET_SIZE 陳述式屬性。 請改用**SQLFetchScroll**和 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性。 ODBC 3。*x*應用程式應該不會使用**SQLSetPos**具有*作業*SQL_ADD 的但應該使用**SQLBulkOperations**與*作業*SQL_ADD。
