---
title: 標頭檔 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8e6d0806a7c3eabd1c6f4cd1836308eba99a6d5a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47656736"
---
# <a name="header-files"></a>標頭檔
Sql.h 標頭檔包含原型的函式和核心 ODBC 介面一致性層級中的功能。 Sqlext.h 標頭檔包含原型的函式和中的層級 1 和層級 2 API 一致性層級的功能。 Sqltypes.h 標頭檔包含類型定義與 SQL 資料類型的指標。  
  
 所有包含的標頭檔 **#define**，ODBCVER，應用程式或驅動程式可以設定要編譯的不同版本的 ODBC。  
  
 若要對齊與 ISO CLI 和開啟群組 CLI，請在標頭檔包含對呼叫中使用的資訊類型的別名**SQLGetInfo**。 下表中，「 ODBC 名稱 」 的資料行表示中的資訊類型的 ODBC 名稱[ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)。 資料行 」 標頭檔中的別名"表示使用 ISO CLI 和開啟群組 CLI 中的名稱。 這些資訊清單名稱的實際數值是相同的 ODBC 和標準 Cli。 這些別名啟用符合標準的應用程式或驅動程式使用 ODBC 3 編譯 *.x*標頭檔。  
  
 這些別名在 ODBC 名稱中包含縮寫的展開，使名稱更容易了解。 "MAX"已擴充成"MAXIMUM"、"LEN 」 到 「 長度 」，「 多 」"MULTIPLE"，"OJ"到"OUTER_JOIN 」，和 「 交易 」 到 「 交易 」。  
  
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
