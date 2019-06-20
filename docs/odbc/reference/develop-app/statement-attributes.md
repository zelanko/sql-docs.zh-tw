---
title: 陳述式屬性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement attributes
- statement attributes [ODBC]
ms.assetid: 4c59cd8e-a713-4095-9065-20d5bdeafe43
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0e669f02eeb76ba529c75851ce8bf6ff9a7831a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149094"
---
# <a name="statement-attributes"></a>陳述式屬性
陳述式屬性是陳述式的特性。 例如，使用書籤和什麼種類的資料指標來使用陳述式的結果集中是否是陳述式屬性。  
  
 陳述式屬性都設有**SQLSetStmtAttr**和其目前的設定擷取**SQLGetStmtAttr**。 不需要應用程式設定的任何陳述式屬性;所有的陳述式屬性都有預設值，其中有些是驅動程式特有。  
  
 當陳述式屬性可以設定取決於本身的屬性。 在執行陳述式之前，必須設定 SQL_ATTR_CONCURRENCY、 SQL_ATTR_CURSOR_TYPE、 SQL_ATTR_SIMULATE_CURSOR 和 SQL_ATTR_USE_BOOKMARKS 的陳述式屬性。 SQL_ATTR_ASYNC_ENABLE 和 SQL_ATTR_NOSCAN 的陳述式屬性可以設定在任何時間，但會再次使用陳述式之前，不會套用。 SQL_ATTR_MAX_LENGTH、 SQL_ATTR_MAX_ROWS 和 SQL_ATTR_QUERY_TIMEOUT 陳述式屬性可以設定在任何時間，但很是否會套用之前的陳述式就會再次使用特定驅動程式。 剩餘的陳述式屬性可以設定在任何時間。  
  
> [!NOTE]  
>  能夠在連接層級設定陳述式屬性，藉由呼叫**SQLSetConnectAttr** ODBC 3 中已被取代。*x*。 ODBC 3。*x*應用程式應該永遠不會設定在連接層級的陳述式屬性。 ODBC 3。*x*驅動程式只需要支援這項功能，如果應該使用 ODBC 2。*x*應用程式。 如需詳細資訊，請參閱 < [SQLSetConnectOption 對應](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)在 < 附錄 g:為了與舊版相容的驅動程式指導方針。  
>   
>  這個例外狀況是 SQL_ATTR_METADATA_ID 和 SQL_ATTR_ASYNC_ENABLE 屬性，這是連接屬性和陳述式屬性，而且在連接層級或陳述式層級設定。  
>   
>  沒有在 ODBC 3 引入的陳述式屬性。*x* （除了 SQL_ATTR_METADATA_ID) 可以設定在連接層級。  
  
 如需詳細資訊，請參閱 < [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)函式描述。
