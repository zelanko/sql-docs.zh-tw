---
title: 描述符欄位 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], fields
- header fields [ODBC]
- record fields [ODBC]
ms.assetid: f38623c8-fdd4-4601-b1f0-97c593d31177
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94e70de7d237c2eca9aee81979cb19d5295561b5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305919"
---
# <a name="descriptor-fields"></a>描述項欄位
描述符包含完全描述列或參數*的標頭*和*記錄*欄位。  
  
 描述符包含以下標頭欄位的單個複本。 更改標題欄位會影響所有列或參數。  
  
|||  
|-|-|  
|SQL_DESC_ALLOC_TYPE|SQL_DESC_BIND_TYPE|  
|SQL_DESC_ARRAY_SIZE|SQL_DESC_COUNT|  
|SQL_DESC_ARRAY_STATUS_PTR|SQL_DESC_ROWS_PROCESSED_PTR|  
|SQL_DESC_BIND_OFFSET_PTR||  
  
 描述符包含零個或多個描述符記錄。 每個記錄描述一列或參數,具體取決於描述符的類型。 綁定新列或參數時,將新記錄添加到描述符中。 當列或參數未綁定時,將從描述符中刪除記錄。 每個紀錄包含以下欄位的單一副本:  
  
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
  
 許多語句屬性對應於描述符的標頭欄位。 通過調用**SQLSetStmtAttr**設定這些屬性,並透過呼叫**SQLSetDescField**設定相應的描述符標頭欄位具有相同的效果。 **SQLGetStmtAttr**和**SQLGetDescField**也是如此,它們檢索相同的資訊。 呼叫敘述函數而不是描述符函數的優點是不需要檢索描述符句柄。  
  
 可以通過設定語句屬性來設定以下標頭欄位:  
  
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
