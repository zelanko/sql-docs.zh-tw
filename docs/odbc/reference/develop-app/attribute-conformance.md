---
title: 屬性一致性 |微軟文件
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
ms.openlocfilehash: b2880a35f4bdc997cc037cdd0d60720267ff4a58
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306399"
---
# <a name="attribute-conformance"></a>屬性一致性
下表指示每個 ODBC 環境屬性的一致性級別,其中定義良好。  
  
|函式|一致性層級|  
|--------------|-----------------------|  
|SQL_ATTR_CONNECTION_POOLING|--[1]|  
|SQL_ATTR_CP_MATCH|--[1]|  
|SQL_ATTR_ODBC_VER|核心|  
|SQL_ATTR_OUTPUT_NTS|--[1]|  
  
 [1] 這是一個可選功能,因此不是一致性級別的一部分。  
  
 下表指示每個 ODBC 連接屬性的一致性級別,其中定義良好。  
  
|函式|一致性層級|  
|--------------|-----------------------|  
|SQL_ATTR_ACCESS_MODE|核心|  
|SQL_ATTR_ASYNC_ENABLE|等級 1/級別 2[1]|  
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
|SQL_ATTR_TXN_ISOLATION|等級 1/級別 2[2]|  
  
 [1] 支援連接級非同步(等級 1 需要)的應用程式必須支援透過呼叫**SQLSetConnectAttr**將此屬性設置為SQL_TRUE;屬性不必透過**SQLSetStmtAttr**將其預設值以外的值設置為該值。 支援語句級非同步(級別 2 需要)的應用程式必須支援使用任一函數將此屬性設置為SQL_TRUE。  
  
 [2] 對於級別 1 介面一致性,驅動程式除了支援驅動程式定義的預設值外還必須支援一個值(通過使用SQL_DEFAULT_TXN_ISOLATION選項調用**SQLGetInfo**可用)。 對於 2 級介面一致性,驅動程式還必須支援SQL_TXN_SERIALIZABLE。  
  
 下表指示每個 ODBC 語句屬性的一致性級別,其中定義良好。  
  
|函式|一致性層級|  
|--------------|-----------------------|  
|SQL_ATTR_APP_PARAM_DESC|核心|  
|SQL_ATTR_APP_ROW_DESC|核心|  
|SQL_ATTR_ASYNC_ENABLE|等級 1/級別 2[1]|  
|SQL_ATTR_CONCURRENCY|等級 1/級別 2[2]|  
|SQL_ATTR_CURSOR_SCROLLABLE|層級 1|  
|SQL_ATTR_CURSOR_SENSITIVITY|層級 2|  
|SQL_ATTR_CURSOR_TYPE|核心/級別 2[3]|  
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
  
 [1] 支援連接級非同步(等級 1 需要)的應用程式必須支援透過呼叫**SQLSetConnectAttr**將此屬性設置為SQL_TRUE;屬性不必透過**SQLSetStmtAttr**將其預設值以外的值設置為該值。 支援語句級非同步(級別 2 需要)的應用程式必須支援使用任一函數將此屬性設置為SQL_TRUE。  
  
 [2] 對於 2 級介面一致性,驅動程式必須支援SQL_CONCUR_READ_ONLY和至少一個其他值。  
  
 [3] 對於 1 級介面一致性,驅動程式必須支援SQL_CURSOR_FORWARD_ONLY和至少一個其他值。 對於級別 2 介面一致性,驅動程式必須支援本文檔中定義的所有值。
