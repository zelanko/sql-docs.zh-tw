---
title: ODBC 3.x 的區塊和可滾動游標相容性 |Microsoft Docs
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
ms.openlocfilehash: 7d12906f8dec0bfb12fc861c067e6e615e758a3b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68134994"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>適用於 ODBC 3.x 應用程式的區塊資料指標、可捲動的資料指標和回溯相容性
**SQLFetchScroll**和**SQLExtendedFetch**兩者都代表應用程式開發介面（API）之間的第一次明確分割，也就是應用程式所呼叫的函式集，以及服務提供者介面（SPI），這是驅動程式所執行的一組函數。 需要進行這項分割，以平衡 ODBC 3.x 中的*需求，這*會使用**SQLFetchScroll**來配合標準，並與使用**SQLExtendedFetch***的 odbc 2.x 相容。*  
  
 *ODBC 3.X* API，這是應用程式所呼叫的一組函式，包括**SQLFetchScroll**和相關的語句屬性。 *ODBC 3.X* SPI，這是驅動程式所實作用的一組函式，包括**SQLFetchScroll**、 **SQLExtendedFetch**和相關的語句屬性。 因為 ODBC 不會在 API 與 SPI 之間正式地強制執行這種分割，所以 ODBC 3.x*應用程式*可能會呼叫**SQLExtendedFetch**和相關的語句屬性。 不過 *，ODBC 3.x*應用程式沒有理由這麼做。 如需 Api 和 SPIs 的詳細資訊，請參閱[ODBC 架構](../../../odbc/reference/odbc-architecture.md)簡介。  
  
 如*需 odbc 3.X 驅動程式管理員*如何將呼叫對應*至 ODBC* 2.x 和 odbc 3.x 驅動程式，*以及 odbc 3.x* *驅動程式應*針對區塊和可滾動資料指標來執行哪些函式和語句屬性的詳細資訊，請參閱附錄 G：驅動程式方針中的[驅動程式](../../../odbc/reference/appendixes/what-the-driver-does.md)在回溯相容性中的功能。  
  
 下表摘要*說明 ODBC 3.x*應用程式應該搭配區塊和可滾動資料指標使用的函數和語句屬性。 它也會*列出在此*區域中，odbc 3.x 應用程式必須知道才能*與 odbc* 2.x*驅動程式相容*的 odbc *2.x 和 odbc* 3.x 之間的變更。  
  
|函數或<br /><br /> 陳述式屬性|註解|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|指向要與**SQLFetchScroll**搭配使用的書簽。<br /><br /> 當應用程式*在 ODBC 2.x*驅動程式中設定此項時，這必須指向固定長度的書簽。|  
|SQL_ATTR_ROW_STATUS_PTR|指向**SQLFetch**、 **SQLFetchScroll**、 **SQLBulkOperations**和**SQLSetPos**所填入的資料列狀態陣列。<br /><br /> 如果應用程式*在 ODBC 2.x*驅動程式中設定此項，並在呼叫**SQLFetchScroll**、 **SQLFetch**或**SQLExtendedFetch**之前，使用*SQL_ADD 的作業來呼叫* **SQLBulkOperation** ，則會傳回 SQLSTATE HY011 （無法立即設定屬性）。<br /><br /> 當應用程式*在 ODBC 2.x*驅動程式中呼叫**SQLFetch**時， **SQLFetch**會對應到**SQLExtendedFetch** ，因此會傳回此陣列中的值。|  
|SQL_ATTR_ROWS_FETCHED_PTR|指向緩衝區，其中**SQLFetch**和**SQLFetchScroll**會傳回所提取的資料列數目。<br /><br /> 當應用程式*在 ODBC 2.x*驅動程式中呼叫**SQLFetch**時， **SQLFetch**會對應到**SQLExtendedFetch** ，因此會傳回這個緩衝區中的值。|  
|SQL_ATTR_ROW_ARRAY_SIZE|設定資料列集大小。<br /><br /> 如果應用程式*在 ODBC 2.x 驅動程式中*使用*SQL_ADD 的作業*來呼叫**SQLBulkOperations** ，SQL_ROWSET_SIZE 將用於呼叫，而不是 SQL_ATTR_ROW_ARRAY_SIZE，因為呼叫會對應至**SQLSetPos** ，其作業會使用** SQL_ROWSET_SIZE 來進行 SQL_ADD 作業。<br /><br /> 在*ODBC 2.x*驅動程式中使用 SQL_ADD**或 SQLExtendedFetch** *的作業來呼叫* **SQLSetPos** ，會使用 SQL_ROWSET_SIZE。<br /><br /> 在*ODBC 2.x*驅動程式中呼叫**SQLFetch**或**SQLFetchScroll**會使用 SQL_ATTR_ROW_ARRAY_SIZE。|  
|**SQLBulkOperations**|執行插入和書簽作業。 在*ODBC 2.x*驅動程式中呼叫*SQL_ADD 的作業* **SQLBulkOperations**時，它會對應至**SQLSetPos** ，並*SQL_ADD 的作業*。 以下是執行詳細資料：<br /><br /> -*使用 ODBC 2.x*驅動程式時，應用程式必須只使用與*StatementHandle*相關聯的隱含配置 ARD;它無法配置另一個 ARD 來加入資料列，*因為 ODBC 2.x*驅動程式中不支援明確描述項作業。 應用程式必須使用**SQLBindCol**來系結至 ARD，而非**SQLSetDescField**或**SQLSetDescRec**。<br />-*呼叫 ODBC 3.x*驅動程式時，應用程式可以呼叫具有 SQL_ADD*作業的* **SQLBulkOperations** ，然後再呼叫**SQLFetch**或**SQLFetchScroll**。 呼叫*ODBC 2.x*驅動程式時，應用程式必須先呼叫**SQLFetchScroll** ，才能呼叫具有 SQL_ADD 之作業的**SQLBulkOperations** 。|  
|**SQLFetch**|傳回下一個資料列集。 以下是執行詳細資料：<br /><br /> -當應用程式*在 ODBC 2.x*驅動程式中呼叫**SQLFetch**時，它會對應至**SQLExtendedFetch**。<br />-當應用程式*在 ODBC 3.x*驅動程式中呼叫**SQLFetch**時，它會傳回使用 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性所指定的資料列數目。|  
|**SQLFetchScroll**|傳回指定的資料列集。 以下是執行詳細資料：<br /><br /> -當應用程式*在 ODBC 2.x*驅動程式中呼叫**SQLFetchScroll**時，它會在套用至單一資料列的每個錯誤之前，傳回 SQLSTATE 01S01 （資料列中的錯誤）。 這只是*因為 ODBC 3.X*驅動程式管理員會將此對應到**SQLExtendedFetch** ，而**SQLExtendedFetch**會傳回此 SQLSTATE。 當應用程式*在 ODBC 3.x*驅動程式中呼叫**SQLFetchScroll**時，它絕對不會傳回 SQLSTATE 01S01 （資料列中的錯誤）。<br />-當應用程式在*FetchOrientation*設為 SQL_FETCH_BOOKMARK*的 ODBC 2.x 驅動程式中*呼叫**SQLFetchScroll**時， *FetchOffset*引數必須設定為0。 如果嘗試*使用 ODBC 2.x*驅動程式來提取以位移為基礎的書簽，則會傳回 SQLSTATE HYC00 （未實作為選擇性功能）。|  
  
> [!NOTE]  
>  ODBC *3.x*應用程式不應使用**SQLExtendedFetch**或 SQL_ROWSET_SIZE 語句屬性。 相反地，它們應該使用**SQLFetchScroll**和 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性。 ODBC *3.x*應用程式不應使用**SQLSetPos**與*SQL_ADD 的作業*，但應使用**SQLBulkOperations**搭配*SQL_ADD 的作業*。
