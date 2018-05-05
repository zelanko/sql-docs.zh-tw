---
title: 陳述式屬性 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement attributes
- statement attributes [ODBC]
ms.assetid: 4c59cd8e-a713-4095-9065-20d5bdeafe43
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7fe7fd9cb7436470b8eba9984a4427a9e43e8490
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="statement-attributes"></a>陳述式屬性
陳述式屬性是陳述式的特性。 例如，使用書籤和什麼種類的設定資料指標使用陳述式的結果陳述式屬性。  
  
 陳述式屬性設定**SQLSetStmtAttr**和其目前的設定擷取**SQLGetStmtAttr**。 沒有需要應用程式設定的任何陳述式屬性;陳述式的所有屬性都有預設值，其中有些是驅動程式專屬。  
  
 當陳述式屬性可以設定取決於屬性本身。 必須先設定陳述式屬性 SQL_ATTR_CONCURRENCY、 SQL_ATTR_CURSOR_TYPE、 SQL_ATTR_SIMULATE_CURSOR 和 SQL_ATTR_USE_BOOKMARKS 陳述式。 SQL_ATTR_ASYNC_ENABLE 和 SQL_ATTR_NOSCAN 的陳述式屬性可以在任何時間設定，但會再次使用陳述式時才會套用。 SQL_ATTR_MAX_LENGTH、 SQL_ATTR_MAX_ROWS 和 sql_attr_query_timeout 時陳述式屬性可以設定在任何時間，但很它們會套用之前的陳述式會再次使用特定驅動程式。 剩餘的陳述式屬性可以在任何時間設定。  
  
> [!NOTE]  
>  能夠在連接層級設定陳述式屬性，藉由呼叫**SQLSetConnectAttr** ODBC 3 中已被取代。*x*。 ODBC 3。*x*應用程式應該永遠不會設定在連接層級的陳述式屬性。 ODBC 3。*x*驅動程式只需要支援這項功能，如果應使用 ODBC 2。*x*應用程式。 如需詳細資訊，請參閱[SQLSetConnectOption 對應](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)中附錄 g： 驅動程式的指導方針回溯相容性。  
>   
>  這個例外狀況是 SQL_ATTR_METADATA_ID 和 SQL_ATTR_ASYNC_ENABLE 」 屬性，也就是連接屬性和陳述式屬性，然後您可以將在連接層級或陳述式層級。  
>   
>  沒有在 ODBC 3 引入的陳述式屬性。*x* （除了 SQL_ATTR_METADATA_ID) 可以設定在連接層級。  
  
 如需詳細資訊，請參閱[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)函式描述。
