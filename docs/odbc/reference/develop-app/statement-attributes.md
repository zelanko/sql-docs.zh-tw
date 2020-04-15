---
title: 語句屬性 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299641"
---
# <a name="statement-attributes"></a>陳述式屬性
語句屬性是語句的特徵。 例如,是否使用書籤以及使用哪種游標與語句的結果集是語句屬性。  
  
 語句屬性使用**SQLSetStmtAttr**及其當前設置使用**SQLGetStmtAttr**進行設置。 沒有要求應用程式設置任何語句屬性;因此,應用程式可以設置任何語句屬性。所有語句屬性都有預設值,其中一些屬性特定於驅動程式。  
  
 可以設置語句屬性時,取決於屬性本身。 在執行語句之前,必須設置SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR和SQL_ATTR_USE_BOOKMARKS語句屬性。 可以隨時設置SQL_ATTR_ASYNC_ENABLE和SQL_ATTR_NOSCAN語句屬性,但在再次使用語句之前不會應用。 可以隨時設置SQL_ATTR_MAX_LENGTH、SQL_ATTR_MAX_ROWS和SQL_ATTR_QUERY_TIMEOUT語句屬性,但在再次使用語句之前是否應用這些屬性是特定於驅動程式的。 可以隨時設置剩餘的語句屬性。  
  
> [!NOTE]  
>  通過調用**SQLSetConnect Attr**在連接級別設置語句屬性的能力已在 ODBC 3 中棄用。*x*. . ODBC 3.*x*應用程式不應在連接級別設置語句屬性。 ODBC 3.*x*驅動程式僅需要支援此功能,如果它們應該與 ODBC 2 配合使用。*x*應用程式。 有關詳細資訊,請參閱附錄 G 中的[SQLSetConnectOption 映射](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md):向後相容性的驅動程式指南。  
>   
>  這是一個例外,SQL_ATTR_METADATA_ID和SQL_ATTR_ASYNC_ENABLE屬性,它們既是連接屬性,也是語句屬性,可以在連接級別或語句級別設置。  
>   
>  ODBC 3 中引入的語句屬性均未。*x(SQL_ATTR_METADATA_ID*除外)可以在連接級別設置。  
  
 有關詳細資訊,請參閱[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)函數說明。
