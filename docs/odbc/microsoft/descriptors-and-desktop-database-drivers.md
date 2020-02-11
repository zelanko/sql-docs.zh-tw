---
title: 描述項和桌面資料庫驅動程式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c0096dad8fbb4cf9847385759702e39ac074c4c6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68112054"
---
# <a name="descriptors-and-desktop-database-drivers"></a>描述項和桌面資料庫驅動程式
描述項是保存資料行資料或動態參數相關資訊的資料結構。 **SQLGetDescField**可以用來抓取下面所列的支援描述元。 不會自動填入實參數描述項（IPD），因為不支援**SQLDescribeParam** 。 也不支援透過 Jet （例如 SQL_DESC_BASE_TABLE_NAME）提供的描述項欄位。  
  
 如需有關 Jet 支援的描述項欄位的詳細資訊，請參閱《 *Microsoft Jet 資料庫引擎程式設計人員指南》*。  
  
 如需描述項的詳細資訊，請參閱 ODBC 程式設計*人員參考*中的「描述元」底下的主題。  
  
|描述項欄位|支援層級|  
|-----------------------|-------------------|  
|SQL_DESC_ALLOC_TYPE|支援|  
|SQL_DESC_ARRAY_SIZE|僅支援 ARD|  
|SQL_DESC_ARRAY_STATUS_PTR|支援|  
|SQL_DESC_BIND_OFFSET_PTR|支援|  
|SQL_DESC_BIND_TYPE|支援|  
|SQL_DESC_COUNT|支援|  
|SQL_DESC_ROWS_PROCESSED_PTR|僅支援 ARD|  
|SQL_DESC_AUTO_UNIQUE_VALUE|支援|  
|SQL_DESC_BASE_COLUMN_NAME|支援（新）|  
|SQL_DESC_BASE_TABLE_NAME|支援（新）|  
|SQL_DESC_CASE_SENSITIVE|一律為 FALSE|  
|SQL_DESC_CATALOG_NAME|不支援|  
|SQL_DESC_CONCISE_TYPE|支援|  
|SQL_DESC_DATA_PTR|支援|  
|SQL_DESC_DATETIME_INTERVAL_CODE|支援|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|支援間隔 C 類型|  
|SQL_DESC_DISPLAY_SIZE|支援|  
|SQL_DESC_FIXED_PREC_SCALE|支援（TRUE 代表 money）|  
|SQL_DESC_INDICATOR_PTR|支援|  
|SQL_DESC_LABEL|支援|  
|SQL_DESC_LENGTH|支援|  
|SQL_DESC_LITERAL_PREFIX|支援|  
|SQL_DESC_LITERAL_SUFFIX|支援|  
|SQL_DESC_LOCAL_TYPE_NAME|不支援（傳回空字串）|  
|SQL_DESC_NAME|支援|  
|SQL_DESC_NULLABLE|支援<br /><br /> **注意**在 Jet 4.0 之前的版本中不支援|  
|SQL_DESC_NUM_PREC_RADIX|支援|  
|SQL_DESC_OCTET_LENGTH|支援|  
|SQL_DESC_OCTET_LENGTH_PTR|支援|  
|SQL_DESC_PARAMETER_TYPE|僅輸入參數|  
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
