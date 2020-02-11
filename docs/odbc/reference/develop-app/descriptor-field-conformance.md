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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67952340"
---
# <a name="descriptor-field-conformance"></a>描述項欄位一致性
下表指出每個 ODBC 描述元標頭欄位的一致性層級，這是妥善定義的。  
  
|函式|一致性層級|  
|--------------|-----------------------|  
|SQL_DESC_ALLOC_TYPE|核心|  
|SQL_DESC_ARRAY_SIZE|核心|  
|SQL_DESC_ARRAY_STATUS_PTR|Core （適用于 APD、IPR 和 IRD）;層級1（適用于 ARD）|  
|SQL_DESC_BIND_OFFSET_PTR|核心|  
|SQL_DESC_BIND_TYPE|核心|  
|SQL_DESC_COUNT|核心|  
|SQL_DESC_ROWS_PROCESSED_PTR|核心|  
  
 下表指出每個「ODBC 描述項記錄」欄位的一致性層級，這是妥善定義的。  
  
|函式|一致性層級|  
|--------------|-----------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|層級 2|  
|SQL_DESC_BASE_COLUMN_NAME|核心|  
|SQL_DESC_BASE_TABLE_NAME|層級 1|  
|SQL_DESC_CASE_SENSITIVE|核心|  
|SQL_DESC_CATALOG_NAME|層級 2|  
|SQL_DESC_CONCISE_TYPE|核心|  
|SQL_DESC_DATA_PTR|核心|  
|SQL_DESC_DATETIME_INTERVAL_ 程式碼|核心 [1]|  
|SQL_DESC_DATETIME_INTERVAL_ 精確度|核心 [1]|  
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
  
 [1] 只有在驅動程式支援適用的資料類型時，才需要支援這些記錄欄位。  
  
 [2] 針對核心層級的一致性，驅動程式必須支援 SQL_PARAM_INPUT。 針對層級2介面一致性，驅動程式也必須支援 SQL_PARAM_INPUT_OUTPUT 和 SQL_PARAM_OUTPUT。
