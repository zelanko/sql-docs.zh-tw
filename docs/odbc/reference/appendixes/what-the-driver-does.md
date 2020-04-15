---
title: 驅動程式的作用 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301389"
---
# <a name="what-the-driver-does"></a>驅動程式的用途
下表總結了 ODBC *3.x*驅動程式應該為塊和可滾動遊標實現的功能和語句屬性。  
  
|功能或<br /><br /> 陳述式屬性|註解|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR|設置由**SQLFetch**和**SQLFetchScroll**填充的行狀態陣列的位址。 如果在語句狀態 S6 中調用**SQLSetPos,** 則**SQLSetPos**也會填充此陣列。 如果在狀態 S7 中調用**SQLSetPos,** 則此陣列不會填充,但**SQL 擴展 Fetch**的*RowStatusArray*參數指向的陣列將填充。 有關詳細資訊,請參閱附錄 B[中的語句轉換](../../../odbc/reference/appendixes/statement-transitions.md):ODBC 狀態轉換表。|  
|SQL_ATTR_ROWS_FETCHED_PTR|設置**SQLFetch**和**SQLFetchScroll**傳回提取的行數的緩衝區的位址。 如果調用**SQLExtendedFetch,** 則不會填充此緩衝區,但*RowCountPtr*參數指向獲取的行數。|  
|SQL_ATTR_ROW_ARRAY_SIZE|設置**SQLFetch**和**SQLFetchScroll**使用的行集大小。|  
|SQL_ROWSET_SIZE|設定**SQL 擴充取得**使用的行集大小。 如果 ODBC *3.x*驅動程式想要與呼叫**SQLExtendedFetch**或**SQLSetPos**的 ODBC *2.x*應用程式一起工作,則實現此目的。|  
|**SQLBulk 操作**|如果 ODBC *3.x*驅動程式應與使用**SQLSetPos**的具有SQL_ADD操作的 ODBC *2.x*應用程式一*起工作*,則驅動程式除了使用 SQL_ADD*操作*的**SQLBulk 操作**外,還必須支援具有SQL_ADD*操作*的**SQLSetPos。**|  
|**SQL 延伸**|返回指定的行集。 如果 ODBC *3.x*驅動程式想要與呼叫**SQLExtendedFetch**或**SQLSetPos**的 ODBC *2.x*應用程式一起工作,則實現此目的。 以下是實現詳細資訊:<br /><br /> - 驅動程式從SQL_ROWSET_SIZE語句屬性的值檢索列集大小。<br />- 驅動程式從*RowStatusArray*參數檢索行狀態陣列的位址,而不是SQL_ATTR_ROW_STATUS_PTR語句屬性。 對**SQL 擴充取得**的呼叫中的*RowStatusArray*參數不能為空指標。 (請注意,在 ODBC *3.x*中,SQL_ATTR_ROW_STATUS_PTR 語句屬性可以是空指標。<br />- 驅動程式從*RowCountPtr*參數檢索行獲取緩衝區的位址,而不是SQL_ATTR_ROWS_FETCHED_PTR語句屬性。<br />- 驅動程式傳回 SQLSTATE 01S01(行中的錯誤),以指示在呼叫**SQLExtendedFetch**獲取行時發生了錯誤。 ODBC *3.x*驅動程式應僅在調用**SQLAtFetch**時返回 SQLSTATE 01S01(行中的錯誤),而不是調用**SQLFetch**或**SQLFetchScroll**時返回 SQLSTATE 01S01(行中的錯誤)。 為了保持向後相容性,當 SQLAaS01(行中的錯誤)由**SQLExtendedFetch**返回時,驅動程式管理器不會根據[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)的「狀態記錄序列」部分中所述的規則對錯誤佇列中的狀態記錄進行排序。|  
|**SQLFetch**|返回下一個行集。 以下是實現詳細資訊:<br /><br /> - 驅動程式從SQL_ATTR_ROW_ARRAY_SIZE語句屬性的值檢索列集大小。<br />- 驅動程式從SQL_ATTR_ROW_STATUS_PTR語句屬性檢索行狀態陣列的位址。<br />- 驅動程式從SQL_ATTR_ROWS_FETCHED_PTR語句屬性檢索行提取緩衝區的位址。<br />- 應用程式可以在**SQLFetchScroll**和**SQLFetch**之間混合調用。<br />-   如果綁定列**0,SQLFetch**將返回書籤。<br />-   可以調用**SQLFetch**來返回多行。<br />- 驅動程式不返回 SQLSTATE 01S01(行中的錯誤),以指示在調用**SQLFetch**獲取行時發生了錯誤。|  
|**SQLFetchScroll**|返回指定的行集。 以下是實現詳細資訊:<br /><br /> - 驅動程式從SQL_ATTR_ROW_ARRAY_SIZE語句屬性檢索行集大小。<br />- 驅動程式從SQL_ATTR_ROW_STATUS_PTR語句屬性檢索行狀態陣列的位址。<br />- 驅動程式從SQL_ATTR_ROWS_FETCHED_PTR語句屬性檢索行提取緩衝區的位址。<br />- 應用程式可以在**SQLFetchScroll**和**SQLFetch**之間混合調用。<br />- 驅動程式不返回 SQLSTATE 01S01(行中的錯誤),以指示在調用**SQLFetchScroll**獲取行時發生了錯誤。|  
|**SQLSetPos**|執行各種定位操作。 以下是實現詳細資訊:<br /><br /> - 這可以在語句狀態 S6 或 S7 中調用。 有關詳細資訊,請參閱附錄 B[中的語句轉換](../../../odbc/reference/appendixes/statement-transitions.md):ODBC 狀態轉換表。<br />- 如果在語句狀態 S5 或 S6 中呼叫此選項,驅動程式將從SQL_ATTR_ROWS_FETCHED_PTR語句屬性和行狀態陣列的位址從SQL_ATTR_ROW_STATUS_PTR語句屬性中檢索列集大小。<br />- 如果在語句狀態 S7 中呼叫此選項,驅動程式將從 SQL_ROWSET_SIZE 語句屬性和從**SQL 延長獲取**的*RowStatusArray*參數中檢索列集大小。<br />- 驅動程式傳回 SQLSTATE 01S01(行中的錯誤),只是為了指示在呼叫**SQLSetPos**以在狀態 S7 中調用函數時獲取行以執行批量操作時發生了錯誤。 為了保持向後相容性,如果**SQLSetPos**返回 SQLSTATE 01S01(行中的錯誤),驅動程式管理器不會根據[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)的「狀態記錄序列」部分中所述的規則對錯誤佇列中的狀態記錄進行排序。<br />- 如果驅動程式應使用呼叫**SQLSetPos**的 ODBC *2.x*應用程式,*操作*參數為 SQL_ADD,則驅動程式必須支援**SQLSetPos,***操作*參數為 SQL_ADD。|
