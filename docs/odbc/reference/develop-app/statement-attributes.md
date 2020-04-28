---
title: 語句屬性 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec24cc43e8c57e47ddda9f20fac1807f42453e84
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299641"
---
# <a name="statement-attributes"></a>陳述式屬性
語句屬性是語句的特性。 例如，是否要使用書簽，以及要搭配語句結果集使用的資料指標類型是語句屬性。  
  
 語句屬性是使用**SQLSetStmtAttr**來設定，而其目前的設定是使用**SQLGetStmtAttr**來抓取。 應用程式不需要設定任何語句屬性;所有語句屬性都有預設值，其中有些是特定驅動程式。  
  
 當語句屬性可以設定時，會視屬性本身而定。 在執行語句之前，必須先設定 SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR 和 SQL_ATTR_USE_BOOKMARKS 語句屬性。 SQL_ATTR_ASYNC_ENABLE 和 SQL_ATTR_NOSCAN 語句屬性可以在任何時間設定，但必須等到再次使用語句後才會套用。 SQL_ATTR_MAX_LENGTH、SQL_ATTR_MAX_ROWS 和 SQL_ATTR_QUERY_TIMEOUT 語句屬性可以隨時設定，但它是驅動程式特有的，不論是否在再次使用語句之前套用。 可以隨時設定其餘的語句屬性。  
  
> [!NOTE]  
>  藉由呼叫**SQLSetConnectAttr**在連接層級設定語句屬性的功能，已在 ODBC 3 中被取代。*x*。 ODBC 3。*x*應用程式絕對不應在連接層級設定語句屬性。 ODBC 3。*x*驅動程式只需要支援這種功能（如果它們應該與 ODBC 2 搭配使用的話）。*x*應用程式。 如需詳細資訊，請參閱附錄 G：驅動程式方針中的[SQLSetConnectOption 對應](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)，以取得回溯相容性。  
>   
>  唯一的例外是 SQL_ATTR_METADATA_ID 和 SQL_ATTR_ASYNC_ENABLE 屬性，這兩者都是連接屬性和語句屬性，而且可以在連接層級或語句層級設定。  
>   
>  未在 ODBC 3 中引進任何語句屬性。*x* （SQL_ATTR_METADATA_ID 除外）可以在連接層級設定。  
  
 如需詳細資訊，請參閱[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)函數描述。
