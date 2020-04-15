---
title: 描述符與桌面資料庫驅動程式 ( A)微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], descriptors
- Jet-based ODBC drivers [ODBC], descriptors
- descriptors [ODBC], Jet-supported descriptor fields
- ODBC desktop database drivers [ODBC], descriptors
ms.assetid: 9ae2d9b5-365f-4f0a-9116-defe9498b401
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ef79855f71d23e5a884822371f1894eb83442a9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303509"
---
# <a name="descriptors-and-desktop-database-drivers"></a>描述項和桌面資料庫驅動程式
描述符是一種數據結構,用於保存有關列數據或動態參數的資訊。 **SQLGetDescField**可用於檢索下面列出的受支援的描述符。 實現參數描述符 (IPD) 不會自動填充,因為**SQLDescribeParam**不受支援。 也不支援透過 Jet (如 SQL_DESC_BASE_TABLE_NAME) 不可用的描述符位。  
  
 有關 Jet 支援的描述符位元的詳細資訊,請參閱 Microsoft *Jet 資料庫引擎程式者指南*。  
  
 有關描述符的詳細資訊,請參閱*ODBC 程式師參考*中的「描述符」下的主題。  
  
|描述字欄位|支援層級|  
|-----------------------|-------------------|  
|SQL_DESC_ALLOC_TYPE|支援|  
|SQL_DESC_ARRAY_SIZE|僅支援 ARD|  
|SQL_DESC_ARRAY_STATUS_PTR|支援|  
|SQL_DESC_BIND_OFFSET_PTR|支援|  
|SQL_DESC_BIND_TYPE|支援|  
|SQL_DESC_COUNT|支援|  
|SQL_DESC_ROWS_PROCESSED_PTR|僅支援 ARD|  
|SQL_DESC_AUTO_UNIQUE_VALUE|支援|  
|SQL_DESC_BASE_COLUMN_NAME|支援(新)|  
|SQL_DESC_BASE_TABLE_NAME|支援(新)|  
|SQL_DESC_CASE_SENSITIVE|始終 FALSE|  
|SQL_DESC_CATALOG_NAME|不支援|  
|SQL_DESC_CONCISE_TYPE|支援|  
|SQL_DESC_DATA_PTR|支援|  
|SQL_DESC_DATETIME_INTERVAL_CODE|支援|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|支援 INTERVAL C 類型|  
|SQL_DESC_DISPLAY_SIZE|支援|  
|SQL_DESC_FIXED_PREC_SCALE|支援(真為錢)|  
|SQL_DESC_INDICATOR_PTR|支援|  
|SQL_DESC_LABEL|支援|  
|SQL_DESC_LENGTH|支援|  
|SQL_DESC_LITERAL_PREFIX|支援|  
|SQL_DESC_LITERAL_SUFFIX|支援|  
|SQL_DESC_LOCAL_TYPE_NAME|不支援 (傳回 EMPTY 字串)|  
|SQL_DESC_NAME|支援|  
|SQL_DESC_NULLABLE|支援<br /><br /> **注意**在 Jet 4.0 之前的版本中不受支援|  
|SQL_DESC_NUM_PREC_RADIX|支援|  
|SQL_DESC_OCTET_LENGTH|支援|  
|SQL_DESC_OCTET_LENGTH_PTR|支援|  
|SQL_DESC_PARAMETER_TYPE|只輸入參數|  
|SQL_DESC_PRECISION|支援|  
|SQL_DESC_SCALE|支援|  
|SQL_DESC_SCHEMA_NAME|不支援|  
|SQL_DESC_SEARCHABLE|支援|  
|SQL_DESC_TABLE_NAME|不支援|  
|SQL_DESC_TYPE|支援|  
|SQL_DESC_TYPE_NAME|支援|  
|SQL_DESC_UNNAMED|支援|  
|SQL_DESC_UNSIGNED|支援|  
|SQL_DESC_UPDATABLE|支援|
