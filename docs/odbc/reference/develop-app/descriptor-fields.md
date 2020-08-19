---
description: 描述項欄位
title: 描述項欄位 |Microsoft Docs
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
ms.openlocfilehash: 56ca1fa7d558101774d10c8daa530fa32f3f7d21
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476730"
---
# <a name="descriptor-fields"></a>描述項欄位
描述項包含的 *標頭* 和 *記錄* 欄位可完整描述資料行或參數。  
  
 描述項包含下列標頭欄位的單一複本。 變更標頭欄位會影響所有的資料行或參數。  

:::row:::
    :::column:::
        SQL_DESC_ALLOC_TYPE  
        SQL_DESC_ARRAY_SIZE  
        SQL_DESC_ARRAY_STATUS_PTR  
        SQL_DESC_BIND_OFFSET_PTR  
    :::column-end:::
    :::column:::
        SQL_DESC_BIND_TYPE  
        SQL_DESC_COUNT  
        SQL_DESC_ROWS_PROCESSED_PTR  
    :::column-end:::
:::row-end:::

 描述項包含零或多個描述項記錄。 每一筆記錄都會描述資料行或參數，端視描述項的類型而定。 系結新的資料行或參數時，會將新的記錄新增至描述項。 當資料行或參數未系結時，會從描述項中移除記錄。 每一筆記錄都包含下欄欄位的單一複本：  

:::row:::
    :::column:::
        SQL_DESC_AUTO_UNIQUE_VALUE  
        SQL_DESC_BASE_COLUMN_NAME  
        SQL_DESC_BASE_TABLE_NAME  
        SQL_DESC_CASE_SENSITIVE  
        SQL_DESC_CATALOG_NAME  
        SQL_DESC_CONCISE_TYPE  
        SQL_DESC_DATA_PTR  
        SQL_DESC_DATETIME_INTERVAL_CODE  
        SQL_DESC_DATETIME_INTERVAL_PRECISION  
        SQL_DESC_DISPLAY_SIZE  
        SQL_DESC_FIXED_PREC_SCALE  
        SQL_DESC_INDICATOR_PTR  
        SQL_DESC_LABEL  
        SQL_DESC_LENGTH  
        SQL_DESC_LITERAL_PREFIX  
        SQL_DESC_LITERAL_SUFFIX  
    :::column-end:::
    :::column:::
        SQL_DESC_LOCAL_TYPE_NAME  
        SQL_DESC_NAME  
        SQL_DESC_NULLABLE  
        SQL_DESC_OCTET_LENGTH  
        SQL_DESC_OCTET_LENGTH_PTR  
        SQL_DESC_PARAMETER_TYPE  
        SQL_DESC_PRECISION  
        SQL_DESC_SCALE  
        SQL_DESC_SCHEMA_NAME  
        SQL_DESC_SEARCHABLE  
        SQL_DESC_TABLE_NAME  
        SQL_DESC_TYPE  
        SQL_DESC_TYPE_NAME  
        SQL_DESC_UNNAMED  
        SQL_DESC_UNSIGNED  
        SQL_DESC_UPDATABLE  
    :::column-end:::
:::row-end:::

 許多語句屬性都對應至描述項的標頭欄位。 透過呼叫 **SQLSetStmtAttr** 來設定這些屬性，並藉由呼叫 **SQLSetDescField** 來設定對應的描述項標頭欄位具有相同的效果。 這同樣適用于 **SQLGetStmtAttr** 和 **SQLGetDescField**，這兩個都會抓取相同的資訊。 呼叫語句函式而不是描述項函式的優點是不需要抓取描述項控制碼。  
  
 您可以藉由設定語句屬性來設定下列標頭欄位：  

:::row:::
    :::column:::
        SQL_DESC_ARRAY_SIZE  
        SQL_DESC_ARRAY_STATUS_PTR  
        SQL_DESC_BIND_OFFSET_PTR  
    :::column-end:::
    :::column:::
        SQL_DESC_BIND_TYPE  
        SQL_DESC_ROWS_PROCESSED_PTR  
    :::column-end:::
:::row-end:::

 此章節包含下列主題。  
  
-   [記錄計數](../../../odbc/reference/develop-app/record-count.md)  
  
-   [繫結描述項記錄](../../../odbc/reference/develop-app/bound-descriptor-records.md)  
  
-   [延遲的欄位](../../../odbc/reference/develop-app/deferred-fields.md)  
  
-   [一致性檢查](../../../odbc/reference/develop-app/consistency-check.md)
