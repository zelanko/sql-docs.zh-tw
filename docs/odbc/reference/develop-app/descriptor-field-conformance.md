---
title: 描述項欄位一致性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptor field conformance levels [ODBC]
- conformance levels [ODBC], descriptor field
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 6c29d93b-696c-4960-bff3-4d6bc41bc513
author: MightyPen
ms.author: genemi
ms.openlocfilehash: afdb1f18ad641224d13373436dd58f1919a3d280
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952340"
---
# <a name="descriptor-field-conformance"></a>描述項欄位一致性
下表指出每個 ODBC 描述項標頭欄位，這是妥善定義的一致性層級。  
  
|函數|一致性層級|  
|--------------|-----------------------|  
|SQL_DESC_ALLOC_TYPE|Core|  
|SQL_DESC_ARRAY_SIZE|Core|  
|SQL_DESC_ARRAY_STATUS_PTR|Core (for APD、 ipr 資料庫和 IRD）;（適用於 ARD) 層級 1|  
|SQL_DESC_BIND_OFFSET_PTR|Core|  
|SQL_DESC_BIND_TYPE|Core|  
|SQL_DESC_COUNT|Core|  
|SQL_DESC_ROWS_PROCESSED_PTR|Core|  
  
 下表指出每個 ODBC 描述項記錄欄位，這是妥善定義的一致性層級。  
  
|函數|一致性層級|  
|--------------|-----------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|層級 2|  
|SQL_DESC_BASE_COLUMN_NAME|Core|  
|SQL_DESC_BASE_TABLE_NAME|層級 1|  
|SQL_DESC_CASE_SENSITIVE|Core|  
|SQL_DESC_CATALOG_NAME|層級 2|  
|SQL_DESC_CONCISE_TYPE|Core|  
|SQL_DESC_DATA_PTR|Core|  
|SQL_DESC_DATETIME_INTERVAL_ 程式碼|Core[1]|  
|SQL_DESC_DATETIME_INTERVAL_ PRECISION|Core[1]|  
|SQL_DESC_DISPLAY_SIZE|Core|  
|SQL_DESC_FIXED_PREC_SCALE|Core|  
|SQL_DESC_INDICATOR_PTR|Core|  
|SQL_DESC_LABEL|層級 2|  
|SQL_DESC_LENGTH|Core|  
|SQL_DESC_LITERAL_PREFIX|Core|  
|SQL_DESC_LITERAL_SUFFIX|Core|  
|SQL_DESC_LOCAL_TYPE_NAME|Core|  
|SQL_DESC_NAME|Core|  
|SQL_DESC_NULLABLE|Core|  
|SQL_DESC_OCTET_LENGTH|Core|  
|SQL_DESC_OCTET_LENGTH_PTR|Core|  
|SQL_DESC_PARAMETER_TYPE|核心/層級 2 [2]|  
|SQL_DESC_PRECISION|Core|  
|SQL_DESC_ROWVER|層級 1|  
|SQL_DESC_SCALE|Core|  
|SQL_DESC_SCHEMA_NAME|層級 1|  
|SQL_DESC_SEARCHABLE|Core|  
|SQL_DESC_TABLE_NAME|層級 1|  
|SQL_DESC_TYPE|Core|  
|SQL_DESC_TYPE_NAME|Core|  
|SQL_DESC_UNNAMED|Core|  
|SQL_DESC_UNSIGNED|Core|  
|SQL_DESC_UPDATABLE|Core|  
  
 [只有當驅動程式支援適用於資料類型時，才需要 1] 支援這些記錄的欄位。  
  
 [2] 的核心層級的一致性，此驅動程式必須支援 SQL_PARAM_INPUT。 層級 2 介面一致性，SQL_PARAM_INPUT_OUTPUT 和 SQL_PARAM_OUTPUT，也必須支援此驅動程式。
