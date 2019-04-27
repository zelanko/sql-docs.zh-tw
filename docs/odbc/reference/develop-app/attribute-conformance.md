---
title: 屬性一致性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
- conformance levels [ODBC], attribute
- attribute conformance levels [ODBC]
ms.assetid: 34fea100-10f9-46d5-bc50-3aa867b70f24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 44f1311d98f37412454ad2352366492a8d5a1768
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62672525"
---
# <a name="attribute-conformance"></a>屬性一致性
下表指出這是妥善定義的每個 ODBC 環境屬性的一致性層級。  
  
|函數|一致性層級|  
|--------------|-----------------------|  
|SQL_ATTR_CONNECTION_POOLING|--[1]|  
|SQL_ATTR_CP_MATCH|--[1]|  
|SQL_ATTR_ODBC_VER|核心|  
|SQL_ATTR_OUTPUT_NTS|--[1]|  
  
 [1] 這是選用的功能，並因此不是一致性層級的一部分。  
  
 下表指出這是妥善定義的每個 ODBC 連接屬性的一致性層級。  
  
|函數|一致性層級|  
|--------------|-----------------------|  
|SQL_ATTR_ACCESS_MODE|核心|  
|SQL_ATTR_ASYNC_ENABLE|層級 1/層級 2 [1]|  
|SQL_ATTR_AUTO_IPD|層級 2|  
|SQL_ATTR_AUTOCOMMIT|層級 1|  
|SQL_ATTR_CONNECTION_DEAD|層級 1|  
|SQL_ATTR_CONNECTION_TIMEOUT|層級 2|  
|SQL_ATTR_CURRENT_CATALOG|層級 2|  
|SQL_ATTR_LOGIN_TIMEOUT|層級 2|  
|SQL_ATTR_ODBC_CURSORS|核心|  
|SQL_ATTR_PACKET_SIZE|層級 2|  
|SQL_ATTR_QUIET_MODE|核心|  
|SQL_ATTR_TRACE|核心|  
|SQL_ATTR_TRACEFILE|核心|  
|SQL_ATTR_TRANSLATE_LIB|核心|  
|SQL_ATTR_TRANSLATE_OPTION|核心|  
|SQL_ATTR_TXN_ISOLATION|層級 1/層級 2 [2]|  
  
 [1] 的應用程式支援連接層級非同步 （所需的層級 1） 必須支援此屬性設定為 SQL_TRUE，藉由呼叫**SQLSetConnectAttr**; 屬性不需要可為其預設值以外的值透過值**SQLSetStmtAttr**。 支援陳述式層級非同步 （所需的層級 2） 的應用程式必須支援將這個屬性設定為 SQL_TRUE，使用其中一個函式。  
  
 [2] 的層級 1 介面一致性，此驅動程式必須支援除了驅動程式定義的預設值的一個值 (可透過呼叫**SQLGetInfo** SQL_DEFAULT_TXN_ISOLATION 選項)。 層級 2 介面一致性，驅動程式也必須支援 sql_txn_serializable 的情況。  
  
 下表指出這是妥善定義的每個 ODBC 陳述式屬性的一致性層級。  
  
|函數|一致性層級|  
|--------------|-----------------------|  
|SQL_ATTR_APP_PARAM_DESC|核心|  
|SQL_ATTR_APP_ROW_DESC|核心|  
|SQL_ATTR_ASYNC_ENABLE|層級 1/層級 2 [1]|  
|SQL_ATTR_CONCURRENCY|層級 1/層級 2 [2]|  
|SQL_ATTR_CURSOR_SCROLLABLE|層級 1|  
|SQL_ATTR_CURSOR_SENSITIVITY|層級 2|  
|SQL_ATTR_CURSOR_TYPE|Core/Level 2[3]|  
|SQL_ATTR_ENABLE_AUTO_IPD|層級 2|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|層級 2|  
|SQL_ATTR_IMP_PARAM_DESC|核心|  
|SQL_ATTR_IMP_ROW_DESC|核心|  
|SQL_ATTR_KEYSET_SIZE|層級 2|  
|SQL_ATTR_MAX_LENGTH|層級 1|  
|SQL_ATTR_MAX_ROWS|層級 1|  
|SQL_ATTR_METADATA_ID|核心|  
|SQL_ATTR_NOSCAN|核心|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|核心|  
|SQL_ATTR_PARAM_BIND_TYPE|核心|  
|SQL_ATTR_PARAM_OPERATION_PTR|核心|  
|SQL_ATTR_PARAM_STATUS_PTR|核心|  
|SQL_ATTR_PARAMS_PROCESSED_PTR|核心|  
|SQL_ATTR_PARAMSET_SIZE|核心|  
|SQL_ATTR_QUERY_TIMEOUT|層級 2|  
|SQL_ATTR_RETRIEVE_DATA|層級 1|  
|SQL_ATTR_ROW_ARRAY_SIZE|核心|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR|核心|  
|SQL_ATTR_ROW_BIND_TYPE|核心|  
|SQL_ATTR_ROW_NUMBER|層級 1|  
|SQL_ATTR_ROW_OPERATION_PTR|層級 1|  
|SQL_ATTR_ROW_STATUS_PTR|核心|  
|SQL_ATTR_ROWS_FETCHED_PTR|核心|  
|SQL_ATTR_SIMULATE_CURSOR|層級 2|  
|SQL_ATTR_USE_BOOKMARKS|層級 2|  
  
 [1] 的應用程式支援連接層級非同步 （所需的層級 1） 必須支援此屬性設定為 SQL_TRUE，藉由呼叫**SQLSetConnectAttr**; 屬性不需要可為其預設值以外的值透過值**SQLSetStmtAttr**。 支援陳述式層級非同步 （所需的層級 2） 的應用程式必須支援將這個屬性設定為 SQL_TRUE，使用其中一個函式。  
  
 [2] 的層級 2 介面一致性，驅動程式必須支援 SQL_CONCUR_READ_ONLY 和至少一個其他的值。  
  
 [3] 的層級 1 介面一致性，驅動程式必須支援 SQL_CURSOR_FORWARD_ONLY 和至少一個其他的值。 層級 2 介面一致性，驅動程式必須支援此文件中定義的所有值。
