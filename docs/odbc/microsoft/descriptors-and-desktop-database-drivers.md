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
manager: craigg
ms.openlocfilehash: 17058af1d7f0ab1e35c2d6b31c0337daed4c9e01
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240391"
---
# <a name="descriptors-and-desktop-database-drivers"></a>描述項和桌面資料庫驅動程式
描述元是保留資料行的資料或將動態參數的相關資訊的資料結構。 **SQLGetDescField**可用來擷取支援下面所列的描述元。 實作參數描述項 (IPD) 不會自動填入因為**SQLDescribeParam**不支援。 描述項欄位，便無法透過 Jet （例如 SQL_DESC_BASE_TABLE_NAME) 也不支援。  
  
 如需有關支援 Jet 的描述項欄位的詳細資訊，請參閱*Microsoft Jet Database Engine 程式設計人員指南*。  
  
 詳細描述項的詳細資訊，請參閱底下 「 描述 」 的主題，在*ODBC 程式設計人員參考*。  
  
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
|SQL_DESC_BASE_COLUMN_NAME|（新） 支援|  
|SQL_DESC_BASE_TABLE_NAME|（新） 支援|  
|SQL_DESC_CASE_SENSITIVE|永遠為 FALSE|  
|SQL_DESC_CATALOG_NAME|不支援|  
|SQL_DESC_CONCISE_TYPE|支援|  
|SQL_DESC_DATA_PTR|支援|  
|SQL_DESC_DATETIME_INTERVAL_CODE|支援|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|支援 C 間隔類型|  
|SQL_DESC_DISPLAY_SIZE|支援|  
|SQL_DESC_FIXED_PREC_SCALE|支援 (TRUE money)|  
|SQL_DESC_INDICATOR_PTR|支援|  
|SQL_DESC_LABEL|支援|  
|SQL_DESC_LENGTH|支援|  
|SQL_DESC_LITERAL_PREFIX|支援|  
|SQL_DESC_LITERAL_SUFFIX|支援|  
|SQL_DESC_LOCAL_TYPE_NAME|不支援 （傳回空字串）|  
|SQL_DESC_NAME|支援|  
|SQL_DESC_NULLABLE|支援<br /><br /> **請注意**前面 Jet 4.0 的版本中不支援|  
|SQL_DESC_NUM_PREC_RADIX|支援|  
|SQL_DESC_OCTET_LENGTH|支援|  
|SQL_DESC_OCTET_LENGTH_PTR|支援|  
|SQL_DESC_PARAMETER_TYPE|只有輸入的參數|  
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
