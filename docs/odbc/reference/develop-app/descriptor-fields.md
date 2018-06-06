---
title: 描述項欄位 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], fields
- header fields [ODBC]
- record fields [ODBC]
ms.assetid: f38623c8-fdd4-4601-b1f0-97c593d31177
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cddf01c0ef40b582410773ba109c2d1c23ee1e7a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="descriptor-fields"></a>描述項欄位
項目中包含*標頭*和*記錄*完整地描述資料行或參數的欄位。  
  
 描述元包含下列標頭欄位的單一複本。 變更標頭欄位，會影響所有的資料行或參數。  
  
|||  
|-|-|  
|SQL_DESC_ALLOC_TYPE|SQL_DESC_BIND_TYPE|  
|SQL_DESC_ARRAY_SIZE|SQL_DESC_COUNT|  
|SQL_DESC_ARRAY_STATUS_PTR|SQL_DESC_ROWS_PROCESSED_PTR|  
|SQL_DESC_BIND_OFFSET_PTR||  
  
 描述元包含零或多個描述項記錄。 每一筆記錄描述的資料行或參數，根據描述元的類型。 新的資料行或參數繫結，會將新的記錄加入描述元。 解除繫結資料行或參數時，記錄移除時從描述項。 每一筆記錄會包含下列欄位的單一複本：  
  
|||  
|-|-|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_DESC_LOCAL_TYPE_NAME|  
|SQL_DESC_BASE_COLUMN_NAME|SQL_DESC_NAME|  
|SQL_DESC_BASE_TABLE_NAME|SQL_DESC_NULLABLE|  
|SQL_DESC_CASE_SENSITIVE|SQL_DESC_OCTET_LENGTH|  
|SQL_DESC_CATALOG_NAME|SQL_DESC_OCTET_LENGTH_PTR|  
|SQL_DESC_CONCISE_TYPE|SQL_DESC_PARAMETER_TYPE|  
|SQL_DESC_DATA_PTR|SQL_DESC_PRECISION|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQL_DESC_SCALE|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQL_DESC_SCHEMA_NAME|  
|SQL_DESC_DISPLAY_SIZE|SQL_DESC_SEARCHABLE|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_DESC_TABLE_NAME|  
|SQL_DESC_INDICATOR_PTR|SQL_DESC_TYPE|  
|SQL_DESC_LABEL|SQL_DESC_TYPE_NAME|  
|SQL_DESC_LENGTH|SQL_DESC_UNNAMED|  
|SQL_DESC_LITERAL_PREFIX|SQL_DESC_UNSIGNED|  
|SQL_DESC_LITERAL_SUFFIX|SQL_DESC_UPDATABLE|  
  
 許多陳述式屬性會對應至標頭欄位的描述元。 設定這些屬性，透過呼叫**SQLSetStmtAttr**呼叫以設定對應的描述項標頭欄位和**SQLSetDescField**有相同的效果。 同樣適用於**SQLGetStmtAttr**和**SQLGetDescField**，這兩種擷取相同的資訊。 呼叫陳述式函式，而不是描述元函式的優點不一定要擷取的描述項控制代碼。  
  
 設定陳述式屬性，即可設定下列標頭欄位：  
  
|||  
|-|-|  
|SQL_DESC_ARRAY_SIZE|SQL_DESC_BIND_TYPE|  
|SQL_DESC_ARRAY_STATUS_PTR|SQL_DESC_ROWS_PROCESSED_PTR|  
|SQL_DESC_BIND_OFFSET_PTR||  
  
 此章節包含下列主題。  
  
-   [記錄計數](../../../odbc/reference/develop-app/record-count.md)  
  
-   [繫結描述項記錄](../../../odbc/reference/develop-app/bound-descriptor-records.md)  
  
-   [延遲的欄位](../../../odbc/reference/develop-app/deferred-fields.md)  
  
-   [一致性檢查](../../../odbc/reference/develop-app/consistency-check.md)
