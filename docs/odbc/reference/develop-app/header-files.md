---
description: 標頭檔
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec8eede80f88f10e0b1ca43696e75dddec121ffe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476650"
---
# <a name="header-files"></a>標頭檔
Sql .h 標頭檔包含核心 ODBC 介面一致性層級中之函式和功能的原型。 Sqlext.h .h 標頭檔包含層級1和層級 2 API 一致性層級中的函式和功能原型。 Sqltypes .h 標頭檔包含 SQL 資料類型的類型定義和指標。  
  
 標頭檔全都包含 **#define**ODBCVER，應用程式或驅動程式可以設定為針對不同版本的 ODBC 進行編譯。  
  
 為了與 ISO CLI 保持一致，並開啟群組 CLI，標頭檔包含在呼叫 **SQLGetInfo**時所使用之資訊類型的別名。 在下表中，"ODBC name" 資料行指出 odbc [API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)中資訊類型的 odbc 名稱。 資料行「標頭檔中的別名」表示 ISO CLI 和 Open Group CLI 中使用的名稱。 這些資訊清單名稱的實際數值在 ODBC 和標準 Cli 中都相同。 這些別名可讓符合標準的應用程式或驅動程式 *使用 ODBC 3.x* 標頭檔進行編譯。  
  
 這些別名包含 ODBC 名稱中的縮寫，以便更容易理解名稱。 「最大值」會展開為「最大值」、「LEN」到「長度」、「MULT」為「多」、「OJ」、「OUTER_JOIN」和「TXN」為「交易」。  
  
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
