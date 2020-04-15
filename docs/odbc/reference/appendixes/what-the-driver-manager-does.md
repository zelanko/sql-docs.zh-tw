---
title: 驅動程式管理員的作用 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07ab0784e6f6ad4487a02a179a5fa3be2617c930
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306559"
---
# <a name="what-the-driver-manager-does"></a>驅動程式管理員的用途
下表總結了 ODBC *3.x*驅動程式管理員如何將呼叫映射到 ODBC *2.x*和 ODBC *3.x*驅動程式。  
  
|功能或<br /><br /> 陳述式屬性|註解|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|指向書籤以與**SQLFetchScroll**一起使用。 以下是實現詳細資訊:<br /><br /> - 當應用程式在 ODBC *2.x*驅動程式中設定此參數時,ODBC *3.x*驅動程式管理器會快取它。 它引用指標並將值傳遞給**SQL 擴充提取***的 Fetch 偏移*參數中的 ODBC *2.x*驅動程式,而稍後應用程式呼叫**SQLFetchScroll。**<br />- 當應用程式在 ODBC *3.x*驅動程式中設定此驅動程式時,ODBC *3.x*驅動程式管理員將呼叫傳遞給驅動程式。|  
|SQL_ATTR_ROW_STATUS_PTR|指向由**SQLFetch、SQLFetchScroll、SQLBulk****操作**和**SQLSetPos**填充的**SQLFetch**行狀態陣列。 以下是實現詳細資訊:<br /><br /> - 當應用程式在 ODBC *2.x*驅動程式中設定此值時,ODBC *3.x*驅動程式管理器緩存其值。 當調用**SQLFetchScroll 或****SQLFetch**時,它將此值傳遞給**SQLAa 的 SQLAa** *參數*中的 ODBC *2.x*驅動程式。<br />- 當應用程式在 ODBC *3.x*驅動程式中設定此驅動程式時,ODBC *3.x*驅動程式管理員將呼叫傳遞給驅動程式。<br />- 在狀態 S6 中,如果應用程式設定SQL_ATTR_ROW_STATUS_PTR,然後調用**SQLBulk 操作**(操作SQL_ADD)或**SQLSetPos,** 而無需首先調用**SQLFetch**或**SQLFetchScroll,** 則傳回 SQLSTATE HY011(現在無法設置屬性)。 *Operation*|  
|SQL_ATTR_ROWS_FETCHED_PTR|指向**SQLFetch**和**SQLFetchScroll**傳回提取的行數的緩衝區。 以下是實現詳細資訊:<br /><br /> - 當應用程式在 ODBC *2.x*驅動程式中設定此值時,ODBC *3.x*驅動程式管理器緩存其值。 當應用程式呼叫**SQLFetch**或**SQLFetchScroll**時,它將此值傳遞給**SQL 擴充擷取**的*RowCountPtr*參數中的 ODBC *2.x*驅動程式。<br />- 當應用程式在 ODBC *3.x*驅動程式中設定此驅動程式時,ODBC *3.x*驅動程式管理員將呼叫傳遞給驅動程式。|  
|SQL_ATTR_ROW_ARRAY_SIZE|設置行集大小。 以下是實現詳細資訊:<br /><br /> - 當應用程式在 ODBC *2.x*驅動程式中設定此驅動程式時,ODBC *3.x*驅動程式管理器將其映射到SQL_ROWSET_SIZE語句屬性。<br />- 當應用程式在 ODBC *3.x*驅動程式中設定此驅動程式時,ODBC *3.x*驅動程式管理員將呼叫傳遞給驅動程式。<br />- 當使用 ODBC *3.x*驅動程式的應用程式呼叫**SQLSetScrollOptions**時,如果基礎驅動程式不支援**SQLSetScrollOptions,** 則SQL_ROWSET_SIZE設定為*RowsetSize*參數中的值。|  
|SQL_ROWSET_SIZE|設定**SQL 擴充擷取**在 ODBC *2.x*應用程式呼叫**SQL 擴充時**使用的行集大小。 以下是實現詳細資訊:<br /><br /> - 當應用程式設定此設定時,ODBC *3.x*驅動程式管理員將呼叫傳遞給驅動程式,而不考慮驅動程式版本。<br />- 當使用 ODBC *2.x*驅動程式的應用程式呼叫**SQLSetScrollOptions**時,SQL_ROWSET_SIZE設定為**RowsetSize**參數中的值。|  
|**SQLBulk 操作**|執行插入操作,或通過書籤操作更新、刪除或提取。 以下是實現詳細資訊:<br /><br /> - 當應用程式在 ODBC *2.x*驅動程式中呼叫**具有**SQL_ADD*操作時*,ODBC *3.x*驅動程式管理員將其映射到具有SQL_ADD*操作*的**SQLSetPos。**<br />- 當使用不支援**SQLSetPos**的 ODBC*Operation* *2.x*驅動程式 操作SQL_ADD時,ODBC *3.x*驅動程式管理員不會將**SQLSetPos**具有SQL_ADD*操作*映射到具有SQL_ADD*操作*的**SQLBulk 操作**。 這是因為**SQLBulk 操作**不能在狀態 S7 中調用,在 ODBC *2.x*中,這是可以調用**SQLSetPos**的唯一狀態。<br />- 如果應用程式在呼叫**SQLFetchScroll**之前在 ODBC *2.x*驅動程式中呼叫**SQLBulk 操作**,操作SQL_ADD,則 ODBC *Operation* *3.x*驅動程式管理器將返回錯誤。|  
|**SQL 延伸**|返回指定的行集。 除了剛才注意到的限制之外,ODBC *3.x*驅動程式管理器將呼叫傳遞給**SQLExtendedFetch**的驅動程式,而不管驅動程式版本如何。|  
|**SQLFetch**|返回下一個行集。 以下是實現詳細資訊:<br /><br /> - 當應用程式在 ODBC *2.x*驅動程式中呼叫**SQLFetch**時,ODBC *3.x*驅動程式管理員將其映射到**SQL 擴充 。** **SQL 擴展取得**的*提取方向*參數設定為SQL_FETCH_NEXT。 驅動程式管理員使用*rowStatusArray*參數的SQL_ATTR_ROW_STATUS_PTR語句屬性的緩存值和*RowCountPtr*參數SQL_ATTR_ROWS_FETCHED_PTR語句屬性的緩存值。<br />- ODBC *3.x*應用程式可以在 ODBC *2.x*驅動程式中混合對**SQLFetch**和**SQLFetchScroll**的呼叫,因為當應用程式在 ODBC *2.x*驅動程式中呼叫 SQLFetch 時,ODBC *3.x*驅動程式管理器將**SQLFetch**映射到**SQLExtendedFetch。**<br />- 如果 ODBC *2.x*驅動程式不支援**SQLExtendedFetch,** 則當應用程式在該驅動程式中呼叫 SQL 提取時,ODBC *3.x*驅動程式管理員不會將**SQLFetch**或**SQLFetchScroll**映射到**SQL 擴充取得**。 如果應用程式嘗試將SQL_ATTR_ROW_ARRAY_SIZE設置為大於 1 的值,則傳回 SQLSTATE HYC00(未實現可選功能)。<br />- 除了剛才注意到的限制之外,ODBC *3.x*驅動程式管理員將呼叫傳遞給**SQLFetch**的驅動程式,而不管驅動程式版本如何。|  
|**SQLFetchScroll**|返回指定的行集。 以下是實現詳細資訊:<br /><br /> - 當應用程式在 ODBC *2.x*驅動程式中呼叫**SQLFetchScroll**時,ODBC *3.x*驅動程式管理員將其映射到**SQL 延伸 。** 它使用*rowStatusArray*參數的 SQL_ATTR_ROW_STATUS_PTR 語句屬性的緩存值和*RowCountPtr*參數的SQL_ATTR_ROWS_FETCHED_PTR語句屬性的緩存值。 如果*SQLFetchScroll***SQLFetchScroll**中的 Fetch 方向參數SQL_FETCH_BOOKMARK,它將使用*fetchOffset*參數的SQL_ATTR_FETCH_BOOKMARK_PTR語句屬性的緩存值,如果**SQLFetchScroll**的*FetchOffset*參數不是 0,則傳回錯誤。<br />- 當應用程式在 ODBC *3.x*驅動程式中呼叫此呼叫時,ODBC *3.x*驅動程式管理員將呼叫傳遞給驅動程式。|  
|**SQLSetPos**|執行各種定位操作。 無論驅動程式版本如何,ODBC *3.x*驅動程式管理員都會將對**SQLSetPos**的調用傳遞給驅動程式。|  
|**SQLSetScroll 選項**|當驅動程式管理器對應**SQLSetScrollOption 的應用程式 SQLSetScrollOption**時,使用不支援**SQLSetScrollOption**的 ODBC *3.x*驅動程式時,驅動程式管理器將SQL_ROWSET_SIZE語句選項(而不是SQL_ATTR_ROW_ARRAY_SIZE語句屬性)設置為**SQLSetScrollOption**中的*RowsetSize*參數。 因此,當調用**SQLFetch**或**SQLFetchScroll**獲取多行時,應用程式無法使用**SQLSetScrollOptions。** 它只能在調用**SQLExtendedFetch**獲取多行時使用。|
