---
title: 標題檔案 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- header files [ODBC]
ms.assetid: b4a03273-5e30-4d7b-826e-02f8f28ba078
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 62364d828e7b1f1ed8c70cae7ae1fc7dc3bc33fc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300188"
---
# <a name="header-files"></a>標頭檔
Sql.h 標頭檔包含核心 ODBC 介面一致性級別中函數和功能的原型。 Sqlext.h 標頭檔包含等級 1 和 2 級 API 一致性級別中函數和功能的原型。 Sqltype.h 標頭檔包含 SQL 資料類型的類型定義和指示器。  
  
 標頭檔都包含一個 **#define**#defineODBCVER,應用程式或驅動程式可以設置為為不同版本的ODBC編譯。  
  
 要與 ISO CLI 和打開組 CLI 保持一致,標頭檔包含調用**SQLGetInfo**中使用的資訊類型的別名。 在下表中,"ODBC 名稱"列指示[ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)中資訊類型的 ODBC 名稱。 "標題檔案中的別名"一欄指示在 ISO CLI 和開放組 CLI 中使用的名稱。 這些清單名稱的實際數值在 ODBC 和標準 CL 中都是相同的。 這些別名使符合標準的應用程式或驅動程式能夠使用 ODBC *3.x*標頭檔進行編譯。  
  
 這些別名包括 ODBC 名稱中縮寫的擴展,以便名稱更容易理解。 "MAX"擴展到"最大","LEN"擴展到"長度","MULT"到"多","OJ"擴展到"OUTER_JOIN","TXN"擴展到"交易"。  
  
|ODBC 名稱|標題檔案的別名|  
|---------------|--------------------------|  
|SQL_MAX_CATALOG_NAME_LEN|SQL_MAXIMUM_CATALOG_NAME_LENGTH|  
|SQL_MAX_COLUMN_NAME_LEN|SQL_MAXIMUM_COLUMN_NAME_LENGTH|  
|SQL_MAX_COLUMNS_IN_GROUP_BY|SQL_MAXIMUM_COLUMNS_IN_GROUP_BY|  
|SQL_MAX_COLUMNS_IN_ORDER_BY|SQL_MAXIMUM_COLUMNS_IN_ORDER_BY|  
|SQL_MAX_COLUMNS_IN_SELECT|SQL_MAXIMUM_COLUMNS_IN_SELECT|  
|SQL_MAX_COLUMNS_IN_TABLE|SQL_MAXIMUM_COLUMNS_IN_TABLE|  
|SQL_MAX_CONCURRENT_ACTIVITIES|SQL_MAXIMUM_CONCURRENT_ACTIVITIES|  
|SQL_MAX_CURSOR_NAME_LEN|SQL_MAXIMUM_CURSOR_NAME_LENGTH|  
|SQL_MAX_DRIVER_CONNECTIONS|SQL_MAXIMUM_DRIVER_CONNECTIONS|  
|SQL_MAX_IDENTIFIER_LEN|SQL_MAXIMUM_IDENTIFIER_LENGTH|  
|SQL_MAX_SCHEMA_NAME_LEN|SQL_MAXIMUM_SCHEMA_NAME_LENGTH|  
|SQL_MAX_STATEMENT_LEN|SQL_MAXIMUM_STATEMENT_LENGTH|  
|SQL_MAX_TABLE_NAME_LEN|SQL_MAXIMUM_TABLE_NAME_LENGTH|  
|SQL_MAX_TABLES_IN_SELECT|SQL_MAXIMUM_TABLES_IN_SELECT|  
|SQL_MAX_USER_NAME_LEN|SQL_MAXIMUM_USER_NAME_LENGTH|  
|SQL_MULT_RESULT_SETS|SQL_MULTIPLE_RESULT_SETS|  
|SQL_OJ_CAPABILITIES|SQL_OUTER_JOIN_CAPABILITIES|  
|SQL_TXN_CAPABLE|SQL_TRANSACTION_CAPABLE|  
|SQL_TXN_ISOLATION_OPTION|SQL_TRANSACTION_ISOLATION_OPTION|
