---
description: 適用於 ODBC 3.x 應用程式的區塊資料指標、可捲動的資料指標和回溯相容性
title: ODBC 3.x 的區塊和可滾動資料指標相容性 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96645f91d52f4141aacf4f2e171ef809a639f73c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476830"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>適用於 ODBC 3.x 應用程式的區塊資料指標、可捲動的資料指標和回溯相容性
**SQLFetchScroll**和**SQLExtendedFetch**的存在都代表 ODBC 在應用程式開發介面 (API) （應用程式所呼叫的函式集合）之間的第一個明確分割，而服務提供者介面 (SPI) ，也就是驅動程式所執行的一組函數。 需要此分割以*平衡 odbc 3.x 中的*需求，這會使用**SQLFetchScroll**來配合標準，並與使用**SQLExtendedFetch***的 odbc 2.x 相容。*  
  
 *ODBC 3.X* API 是應用程式呼叫的函式集合，其中包含**SQLFetchScroll**和相關的語句屬性。 *ODBC 3.X* SPI 是驅動程式所執行的一組函數，包括**SQLFetchScroll**、 **SQLExtendedFetch**和相關的語句屬性。 由於 ODBC 不會在 API 與 SPI 之間正式強制執行這項分割， *因此 ODBC 3.x* 應用程式可能會呼叫 **SQLExtendedFetch** 和相關的語句屬性。 不過 *，ODBC 3.x* 應用程式沒有理由這麼做。 如需 Api 和 SPIs 的詳細資訊，請參閱 [ODBC 架構](../../../odbc/reference/odbc-architecture.md)簡介。  
  
 如*需 odbc 3.X*驅動程式管理員如何將呼叫對應至 odbc 2.X 和 odbc 3.x*驅動程式，* *以及 odbc 3.x* *驅動程式應*針對區塊和可滾動資料指標執行哪些函數和語句屬性的詳細資訊，請參閱附錄 G：驅動程式在附錄 G 中[的](../../../odbc/reference/appendixes/what-the-driver-does.md)作用：提供回溯相容性的驅動程式方針。  
  
 下表摘要 *說明 ODBC 3.x* 應用程式應該搭配區塊和可滾動資料指標使用的函數和語句屬性。 它也會列出 ODBC 2.x*與 odbc 3.x*之間的變更 *，而 odbc* 3.x 應用程式應該要知道才能*與 odbc 2.x* *驅動程式相容*。  
  
|函數或<br /><br /> 陳述式屬性|註解|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|指向要搭配 **SQLFetchScroll**使用的書簽。<br /><br /> 當應用程式 *在 ODBC 2.x* 驅動程式中設定此項時，這必須指向固定長度的書簽。|  
|SQL_ATTR_ROW_STATUS_PTR|指向以 **SQLFetch**、 **SQLFetchScroll**、 **SQLBulkOperations**和 **SQLSetPos**填滿的資料列狀態陣列。<br /><br /> 如果應用程式*在 ODBC 2.x*驅動程式中設定此項，並在呼叫**SQLFetchScroll**、 **SQLFetch**或**SQLExtendedFetch**之前呼叫**SQLBulkOperation** ，SQL_ADD 但現在無法設定 SQLSTATE HY011 (屬性) 會傳回。 *Operation*<br /><br /> 當應用程式*在 ODBC 2.x*驅動程式中呼叫**SQLFetch**時， **SQLFetch**會對應至**SQLExtendedFetch** ，因此會傳回這個陣列中的值。|  
|SQL_ATTR_ROWS_FETCHED_PTR|指向緩衝區，其中 **SQLFetch** 和 **SQLFetchScroll** 會傳回所提取的資料列數目。<br /><br /> 當應用程式*在 ODBC 2.x*驅動程式中呼叫**SQLFetch**時， **SQLFetch**會對應至**SQLExtendedFetch** ，因此會在此緩衝區中傳回值。|  
|SQL_ATTR_ROW_ARRAY_SIZE|設定資料列集大小。<br /><br /> 如果應用程式*在 ODBC 2.x*驅動程式中使用*SQL_ADD 的作業*來呼叫**SQLBulkOperations** ，SQL_ROWSET_SIZE 將用於呼叫，而不是 SQL_ATTR_ROW_ARRAY_SIZE，因為呼叫會對應至具有 SQL_ADD*作業的* **SQLSetPos** ，而該作業會使用 SQL_ROWSET_SIZE。<br /><br /> 在*ODBC 2.x*驅動程式中使用 SQL_ADD**或 SQLExtendedFetch**作業呼叫**SQLSetPos** *時，* 會使用 SQL_ROWSET_SIZE。<br /><br /> 在*ODBC 2.x*驅動程式中呼叫**SQLFetch**或**SQLFetchScroll**會使用 SQL_ATTR_ROW_ARRAY_SIZE。|  
|**SQLBulkOperations**|執行插入和書簽作業。 在*ODBC 2.x*驅動程式中呼叫 SQL_ADD 作業的**SQLBulkOperations**時，它會對應至具有 SQL_ADD*作業的* **SQLSetPos** 。 *Operation* 以下是執行詳細資料：<br /><br /> - *使用 ODBC 2.x 驅動程式時* ，應用程式必須只使用與 *StatementHandle*相關聯的隱含配置 ARD;它無法配置其他 ARD 來加入資料列， *因為 ODBC 2.x* 驅動程式不支援明確的描述項作業。 應用程式必須使用 **SQLBindCol** 來系結至 ARD，而不是 **SQLSetDescField** 或 **SQLSetDescRec**。<br />-*呼叫 ODBC 3.x*驅動程式時，應用程式可以呼叫具有 SQL_ADD*作業的* **SQLBulkOperations** ，然後再呼叫**SQLFetch**或**SQLFetchScroll**。 呼叫 *ODBC 2.x* 驅動程式時，應用程式必須先呼叫 **SQLFetchScroll** ，然後再使用 SQL_ADD 的作業來呼叫 **SQLBulkOperations** 。|  
|**SQLFetch**|傳回下一個資料列集。 以下是執行詳細資料：<br /><br /> -當應用程式*呼叫 ODBC 2.x*驅動程式中的**SQLFetch**時，它會對應至**SQLExtendedFetch**。<br />-當應用程式*呼叫 ODBC 3.x*驅動程式中的**SQLFetch**時，它會傳回以 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性指定的資料列數目。|  
|**SQLFetchScroll**|傳回指定的資料列集。 以下是執行詳細資料：<br /><br /> -當應用程式*呼叫 ODBC 2.x*驅動程式中的**SQLFetchScroll**時，它會在套用至單一資料列的每個錯誤之前，于資料列) 中傳回 SQLSTATE 01S01 (錯誤。 這是 *因為 ODBC 3.X* 驅動程式管理員會將此對應至 **SQLExtendedFetch** ，而 **SQLExtendedFetch** 會傳回這個 SQLSTATE。 當應用程式*在 ODBC 3.x*驅動程式中呼叫**SQLFetchScroll**時，它永遠不會在資料列) 中傳回 SQLSTATE 01S01 (錯誤。<br />-當應用程式在*FetchOrientation*設定為 SQL_FETCH_BOOKMARK*的 ODBC 2.x*驅動程式中呼叫**SQLFetchScroll**時， *FetchOffset*引數必須設定為0。 如果嘗試 *利用 ODBC 2.x* 驅動程式來提取以位移為基礎的書簽，則會傳回 SQLSTATE HYC00 (不會執行的選擇性功能) 。|  
  
> [!NOTE]  
>  ODBC *3.x* 應用程式不應使用 **SQLExtendedFetch** 或 SQL_ROWSET_SIZE 語句屬性。 相反地，它們應該使用 **SQLFetchScroll** 和 SQL_ATTR_ROW_ARRAY_SIZE 的語句屬性。 ODBC *3.x* 應用程式不應該使用 **SQLSetPos** 搭配 *SQL_ADD 的作業* ，但是應該使用 **SQLBulkOperations** 搭配 *SQL_ADD 的作業* 。
