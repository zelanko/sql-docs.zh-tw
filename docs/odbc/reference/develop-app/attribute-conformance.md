---
description: 屬性一致性
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19c58dfe7f8c4219d134cd1662ce8d57b9c76de6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476900"
---
# <a name="attribute-conformance"></a>屬性一致性
下表指出每個 ODBC 環境屬性的一致性層級，這是妥善定義的。  
  
|函式|一致性層級|  
|--------------|-----------------------|  
|SQL_ATTR_CONNECTION_POOLING|--[1]|  
|SQL_ATTR_CP_MATCH|--[1]|  
|SQL_ATTR_ODBC_VER|核心|  
|SQL_ATTR_OUTPUT_NTS|--[1]|  
  
 [1] 這是選擇性功能，因此不屬於一致性層級。  
  
 下表指出每個 ODBC 連接屬性的一致性層級，其中定義完善。  
  
|函式|一致性層級|  
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
  
 [1] 支援層級 1) 所需之連接層級非同步 (的應用程式必須支援藉由呼叫 **SQLSetConnectAttr**將此屬性設定為 SQL_TRUE。屬性不需要透過 **SQLSetStmtAttr**來設定為預設值以外的值。 支援層級 2) 所需 (語句層級非同步應用程式，必須支援使用任一函數將此屬性設定為 SQL_TRUE。  
  
 [2] 針對層級1介面一致性，除了驅動程式定義的預設值之外，驅動程式還必須支援一個值 (可透過 SQL_DEFAULT_TXN_ISOLATION 選項) 來呼叫 **SQLGetInfo** 。 針對層級2介面一致性，驅動程式也必須支援 SQL_TXN_SERIALIZABLE。  
  
 下表指出每個 ODBC 語句屬性的一致性層級，這是妥善定義的。  
  
|函式|一致性層級|  
|--------------|-----------------------|  
|SQL_ATTR_APP_PARAM_DESC|核心|  
|SQL_ATTR_APP_ROW_DESC|核心|  
|SQL_ATTR_ASYNC_ENABLE|層級 1/層級 2 [1]|  
|SQL_ATTR_CONCURRENCY|層級 1/層級 2 [2]|  
|SQL_ATTR_CURSOR_SCROLLABLE|層級 1|  
|SQL_ATTR_CURSOR_SENSITIVITY|層級 2|  
|SQL_ATTR_CURSOR_TYPE|核心/層級 2 [3]|  
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
  
 [1] 支援層級 1) 所需之連接層級非同步 (的應用程式必須支援藉由呼叫 **SQLSetConnectAttr**將此屬性設定為 SQL_TRUE。屬性不需要透過 **SQLSetStmtAttr**來設定為預設值以外的值。 支援層級 2) 所需 (語句層級非同步應用程式，必須支援使用任一函數將此屬性設定為 SQL_TRUE。  
  
 [2] 針對層級2介面一致性，驅動程式必須支援 SQL_CONCUR_READ_ONLY 和至少一個其他值。  
  
 [3] 針對層級1介面一致性，驅動程式必須支援 SQL_CURSOR_FORWARD_ONLY 和至少一個其他值。 針對層級2介面一致性，驅動程式必須支援本檔中定義的所有值。
