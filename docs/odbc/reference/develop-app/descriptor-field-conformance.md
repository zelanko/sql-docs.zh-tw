---
title: "描述項欄位一致性 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptor field conformance levels [ODBC]
- conformance levels [ODBC], descriptor field
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 6c29d93b-696c-4960-bff3-4d6bc41bc513
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 049208450144fdd1c1d3b902093517627486ccf9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="descriptor-field-conformance"></a>描述項欄位一致性
下表指出每個 ODBC 描述項標頭欄位，這是妥善定義的一致性層級。  
  
|函數|一致性層級|  
|--------------|-----------------------|  
|SQL_DESC_ALLOC_TYPE|核心|  
|SQL_DESC_ARRAY_SIZE|核心|  
|SQL_DESC_ARRAY_STATUS_PTR|Core (for APD、 ipr 資料庫和 IRD）;（適用於 ARD) 層級 1|  
|SQL_DESC_BIND_OFFSET_PTR|核心|  
|SQL_DESC_BIND_TYPE|核心|  
|SQL_DESC_COUNT|核心|  
|SQL_DESC_ROWS_PROCESSED_PTR|核心|  
  
 下表指出每個 ODBC 描述項記錄欄位，這是妥善定義的一致性層級。  
  
|函數|一致性層級|  
|--------------|-----------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|層級 2|  
|SQL_DESC_BASE_COLUMN_NAME|核心|  
|SQL_DESC_BASE_TABLE_NAME|層級 1|  
|SQL_DESC_CASE_SENSITIVE|核心|  
|SQL_DESC_CATALOG_NAME|層級 2|  
|SQL_DESC_CONCISE_TYPE|核心|  
|SQL_DESC_DATA_PTR|核心|  
|SQL_DESC_DATETIME_INTERVAL_ 程式碼|核心 [1]|  
|SQL_DESC_DATETIME_INTERVAL_ 有效位數|核心 [1]|  
|SQL_DESC_DISPLAY_SIZE|核心|  
|SQL_DESC_FIXED_PREC_SCALE|核心|  
|SQL_DESC_INDICATOR_PTR|核心|  
|SQL_DESC_LABEL|層級 2|  
|SQL_DESC_LENGTH|核心|  
|SQL_DESC_LITERAL_PREFIX|核心|  
|SQL_DESC_LITERAL_SUFFIX|核心|  
|SQL_DESC_LOCAL_TYPE_NAME|核心|  
|SQL_DESC_NAME|核心|  
|SQL_DESC_NULLABLE|核心|  
|SQL_DESC_OCTET_LENGTH|核心|  
|SQL_DESC_OCTET_LENGTH_PTR|核心|  
|SQL_DESC_PARAMETER_TYPE|核心/層級 2 [2]|  
|SQL_DESC_PRECISION|核心|  
|SQL_DESC_ROWVER|層級 1|  
|SQL_DESC_SCALE|核心|  
|SQL_DESC_SCHEMA_NAME|層級 1|  
|SQL_DESC_SEARCHABLE|核心|  
|SQL_DESC_TABLE_NAME|層級 1|  
|SQL_DESC_TYPE|核心|  
|SQL_DESC_TYPE_NAME|核心|  
|SQL_DESC_UNNAMED|核心|  
|SQL_DESC_UNSIGNED|核心|  
|SQL_DESC_UPDATABLE|核心|  
  
 [只有當驅動程式支援適用的資料類型需要 1] 支援這些記錄的欄位。  
  
 [2] 的核心層級的一致性，驅動程式必須支援 SQL_PARAM_INPUT。 層級 2 介面一致性，驅動程式也必須支援 SQL_PARAM_INPUT_OUTPUT 和 SQL_PARAM_OUTPUT。

