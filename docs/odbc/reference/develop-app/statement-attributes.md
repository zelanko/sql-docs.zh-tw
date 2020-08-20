---
description: 陳述式屬性
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
ms.openlocfilehash: 8e2106a952bfdd7945d5d11ddde39138d0c82a14
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476350"
---
# <a name="statement-attributes"></a>陳述式屬性
語句屬性是語句的特性。 例如，是否要使用書簽，以及要搭配語句結果集使用的資料指標類型是語句屬性。  
  
 語句屬性是使用 **SQLSetStmtAttr** 所設定，並以 **SQLGetStmtAttr**抓取其目前的設定。 應用程式不需要設定任何語句屬性;所有的語句屬性都有預設值，其中有些是驅動程式特定的。  
  
 當語句屬性可以設定時，取決於屬性本身。 在執行語句之前，必須先設定 SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR 和 SQL_ATTR_USE_BOOKMARKS 語句屬性。 您可以隨時設定 SQL_ATTR_ASYNC_ENABLE 和 SQL_ATTR_NOSCAN 語句屬性，但在再次使用語句之前，都不會套用。 您可以隨時設定 SQL_ATTR_MAX_LENGTH、SQL_ATTR_MAX_ROWS 和 SQL_ATTR_QUERY_TIMEOUT 語句屬性，但它是在再次使用語句之前，是否要套用的驅動程式專用屬性。 您可以隨時設定其餘的語句屬性。  
  
> [!NOTE]  
>  藉由呼叫 **SQLSetConnectAttr** 在連接層級設定語句屬性的能力，在 ODBC 3 中已經被取代。*x*。 ODBC 3。*x* 應用程式絕對不應該在連接層級設定語句屬性。 ODBC 3。*x* 驅動程式只有在使用 ODBC 2 時，才需要支援此功能。*x* 應用程式。 如需詳細資訊，請參閱附錄 G：適用于回溯相容性的驅動程式指導方針中的 [SQLSetConnectOption 對應](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) 。  
>   
>  例外狀況是 SQL_ATTR_METADATA_ID 和 SQL_ATTR_ASYNC_ENABLE 屬性，它們都是連接屬性和語句屬性，而且可以在連接層級或語句層級設定。  
>   
>  ODBC 3 中未引進任何語句屬性。*x* (但 SQL_ATTR_METADATA_ID) 可以在連接層級設定。  
  
 如需詳細資訊，請參閱 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) 函數描述。
