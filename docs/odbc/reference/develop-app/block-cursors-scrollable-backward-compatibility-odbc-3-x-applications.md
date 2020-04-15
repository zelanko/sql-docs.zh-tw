---
title: ODBC 3.x 的塊和可滾動游標相容性 |微軟文件
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
ms.openlocfilehash: c526eff6e19014c923f05ad91551a7d7c66f5294
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306339"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>適用於 ODBC 3.x 應用程式的區塊資料指標、可捲動的資料指標和回溯相容性
**SQLFetchScroll**和**SQLExtendedFetch**的存在代表了在 ODBC 中,應用程式程式設計介面 (API) 和服務提供者介面 (SPI) 之間的第一個明確拆分,這是驅動程式實現的函數集。 這種拆分是需要平衡使用**SQLFetchScroll**的 ODBC *3.x*中的需求,以便與標準保持一致,並與使用**SQLDbFetch**的 ODBC *2.x*相容。  
  
 ODBC *3.x* API 是應用程式呼叫的功能集,包括**SQLFetchScroll**和相關語句屬性。 ODBC *3.x* SPI 是驅動程式實現的函數集,包括**SQLFetchScroll、SQL****擴展獲取**和相關語句屬性。 由於 ODBC 未正式強制 API 和 SPI 之間的此拆分,因此 ODBC *3.x*應用程式可以呼叫**SQLExtendedFetch**和相關語句屬性。 但是,ODBC *3.x*應用程式沒有理由這樣做。 有關 API 和 API 的詳細資訊,請參閱[ODBC 體系結構](../../../odbc/reference/odbc-architecture.md)的簡介。  
  
 有關 ODBC *3.x*驅動程式管理器如何映射對 ODBC *2.x*和 ODBC *3.x*驅動程式的調用的資訊,以及 ODBC *3.x*驅動程式應實現哪些功能和語句,以便塊和可滾動游標,請參閱驅動程式在附錄 G[中的作用](../../../odbc/reference/appendixes/what-the-driver-does.md):向後相容性的驅動程式指南。  
  
 下表總結了 ODBC *3.x*應用程式應使用塊和可滾動游標的功能和語句屬性。 它還列出了 ODBC *2.x*和 ODBC *3.x*在這一領域的變化,ODBC *3.x*應用程式應瞭解與 ODBC *2.x*驅動程式相容。  
  
|功能或<br /><br /> 陳述式屬性|註解|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|指向書籤以與**SQLFetchScroll**一起使用。<br /><br /> 當應用程式在 ODBC *2.x*驅動程式中設置此設置時,這必須指向固定長度的書籤。|  
|SQL_ATTR_ROW_STATUS_PTR|指向由**SQLFetch、SQLFetchScroll、SQLBulk****操作**和**SQLSetPos**填充的**SQLFetch**行狀態陣列。<br /><br /> 如果應用程式在 ODBC *2.x*驅動程式中設定此內容,並在調用**SQLFetchScroll、SQLFetch**或**SQLFetch****SQL 擴展獲取**之前調用**SQLBulk** SQL_ADD*操作*,則傳回 SQLSTATE HY011(現在無法設置屬性)。<br /><br /> 當應用程式在 ODBC *2.x*驅動程式中呼叫**SQLFetch**時 **,SQLFetch**將映射到**SQLExtendedFetch,** 因此傳回此陣列中的值。|  
|SQL_ATTR_ROWS_FETCHED_PTR|指向**SQLFetch**和**SQLFetchScroll**傳回提取的行數的緩衝區。<br /><br /> 當應用程式在 ODBC *2.x*驅動程式中呼叫**SQLFetch**時 **,SQLFetch**將映射到**SQLExtendedFetch,** 因此在此緩衝區中傳回一個值。|  
|SQL_ATTR_ROW_ARRAY_SIZE|設置行集大小。<br /><br /> 如果應用程式在 ODBC *2.x*驅動程式中使用 SQL_ADD*操作*調用**SQLBulk 操作**,則SQL_ROWSET_SIZE將用於呼叫,而不是SQL_ATTR_ROW_ARRAY_SIZE,因為呼叫映射到**SQLSetPos,** 操作SQL_ADD使用SQL_ROWSET_SIZE。 *Operation*<br /><br /> 在 ODBC *2.x*驅動程式中使用 SQL_ADD或**SQL 擴展提取***的操作*調用**SQLSetPos**使用SQL_ROWSET_SIZE。<br /><br /> 在 ODBC *2.x*驅動程式中調用**SQLFetch**或**SQLFetchScroll**使用SQL_ATTR_ROW_ARRAY_SIZE。|  
|**SQLBulk 操作**|執行插入和書籤操作。 在 ODBC *2.x*驅動程式中呼叫具有SQL_ADD*操作*的**SQLBulk 操作**時,它將映射到具有SQL_ADD*操作*的**SQLSetPos。** 以下是實現詳細資訊:<br /><br /> - 使用 ODBC *2.x*驅動程式時,應用程式必須僅使用與*語句句柄*關聯的隱式分配的 ARD。它不能為添加行分配另一個 ARD,因為 ODBC *2.x*驅動程式不支援顯式描述符操作。 應用程式必須使用**SQLBindCol**繫結到 ARD,而不是**SQLSetDescField**或**SQLSetDescRec**。<br />- 呼叫 ODBC *3.x*驅動程式時,應用程式可以在調用**SQLFetch**或**SQLFetchScroll**之前調用**SQLBulk** *操作*,操作SQL_ADD。 呼叫 ODBC *2.x*驅動程式時,應用程式必須在呼叫**SQLBulk 操作**SQL_ADD之前調用**SQLFetchScroll。**|  
|**SQLFetch**|返回下一個行集。 以下是實現詳細資訊:<br /><br /> - 當應用程式在 ODBC *2.x*驅動程式中呼叫**SQLFetch**時,它將映射到**SQL 延伸取得**。<br />- 當應用程式在 ODBC *3.x*驅動程式中調用**SQLFetch**時,它將返回使用SQL_ATTR_ROW_ARRAY_SIZE語句屬性指定的行數。|  
|**SQLFetchScroll**|返回指定的行集。 以下是實現詳細資訊:<br /><br /> - 當應用程式在 ODBC *2.x*驅動程式中調用**SQLFetchScroll**時,它將在應用於單個行的每個錯誤之前返回 SQLSTATE 01S01(行中的錯誤)。 它之所以這樣做,只是因為 ODBC *3.x*驅動程式管理器將其映射到**SQL 擴展獲取****,SQL 擴展獲取**返回此 SQLSTATE。 當應用程式在 ODBC *3.x*驅動程式中調用**SQLFetchScroll**時,它永遠不會返回 SQLSTATE 01S01(行中的錯誤)。<br />- 當應用程式在 ODBC *2.x*驅動程式中呼叫**SQLFetchScroll,** 其中*Fetch 方向*設定為SQL_FETCH_BOOKMARK時,必須將*FetchOffset 參數*設定為 0。 如果嘗試使用 ODBC *2.x*驅動程式獲取基於偏移的書籤,則返回 SQLSTATE HYC00(未實現可選功能)。|  
  
> [!NOTE]  
>  ODBC *3.x*應用程式不應使用**SQLExtendedFetch**或SQL_ROWSET_SIZE語句屬性。 相反,他們應該使用**SQLFetchScroll**和SQL_ATTR_ROW_ARRAY_SIZE語句屬性。 ODBC *3.x*應用程式不應將**SQLSetPos**與SQL_ADD*操作*一起使用,而應將**SQLBulk 操作**與SQL_ADD操作一起*使用*。
