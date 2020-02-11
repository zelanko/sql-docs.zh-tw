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
ms.openlocfilehash: 2d20f2535038b13eac0b8d5ca20dfa77bfc12588
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68139031"
---
# <a name="header-files"></a>標頭檔
Sql .h 標頭檔包含核心 ODBC 介面一致性層級中函數和功能的原型。 Sqlext.h 標頭檔包含層級1和層級 2 API 一致性層級中函式和功能的原型。 Sqltypes 標頭檔包含 SQL 資料類型的類型定義和指標。  
  
 標頭檔全都包含 **#define**ODBCVER，可讓應用程式或驅動程式設定為針對不同版本的 ODBC 進行編譯。  
  
 為了配合 ISO CLI 和 Open Group CLI，標頭檔會包含呼叫**SQLGetInfo**時所使用之資訊類型的別名。 在下表中，"ODBC name" 資料行指出[ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)中資訊類型的 odbc 名稱。 「標頭檔中的別名」欄位指出 ISO CLI 和 Open Group CLI 中使用的名稱。 這些資訊清單名稱的實際數值在 ODBC 和標準 Cli 中都相同。 這些別名可讓符合標準的應用程式或驅動程式，*以 ODBC 3.x*標頭檔進行編譯。  
  
 這些別名包括 ODBC 名稱中的縮寫擴充，讓名稱更容易瞭解。 「最大值」會展開為「最大值」、「LEN」到「長度」、「MULT」到「多」、「OJ」到「OUTER_JOIN」，以及「TXN」至「交易」。  
  
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
