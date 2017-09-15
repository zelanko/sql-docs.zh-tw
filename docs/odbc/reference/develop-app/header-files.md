---
title: "標頭檔 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- header files [ODBC]
ms.assetid: b4a03273-5e30-4d7b-826e-02f8f28ba078
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8cec0dc5105addb28606a12c99dd2d77b0a48a64
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="header-files"></a>標頭檔
標頭檔 Sql.h 包含原型函式和核心 ODBC 介面一致性層級中的功能。 Sqlext.h 標頭檔包含原型函式和中的層級 1 和層級 2 API 的一致性層級的功能。 Sqltypes.h 標頭檔包含類型定義與 SQL 資料類型的指標。  
  
 所有包含的標頭檔**#define**，ODBCVER 應用程式或驅動程式可以設定為針對不同版本的 ODBC 編譯。  
  
 若要對齊與 ISO CLI 和開啟群組 CLI，標頭檔包含對呼叫中使用的資訊類型的別名**SQLGetInfo**。 下表中的資料行 [ODBC 名稱] 表示中的資訊類型的 ODBC 名稱[ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)。 資料行 」 標頭檔中的別名"表示 ISO CLI 和開啟群組 CLI 所使用的名稱。 這些資訊清單名稱的實際數值是相同的 ODBC 和標準 Cli。 這些別名啟用符合標準的應用程式或驅動程式使用 ODBC 3 編譯*.x*標頭檔。  
  
 這些別名 ODBC 名稱中包含縮寫的展開，使名稱更容易了解。 "MAX"已擴充 「 最大值 」，「 長度 」 成 「 長度 」、 「 MULT 」 與 「 多個 「"OJ"至"OUTER_JOIN"，"TXN 」 到 「 交易 」。  
  
|ODBC 名稱|標頭檔中的別名|  
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
