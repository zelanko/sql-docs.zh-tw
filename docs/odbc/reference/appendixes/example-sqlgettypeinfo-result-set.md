---
title: 範例 SQLGetTypeInfo 結果集 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC], examples
- SQLGetTypeInfo function [ODBC], examples
- data types [ODBC], SQL data types
ms.assetid: dc1952cc-7581-4d69-9c72-7dc1cd370836
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 028b9be01439b122ff164aed68adb40eb1b4a46e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47662612"
---
# <a name="example-sqlgettypeinfo-result-set"></a>SQLGetTypeInfo 結果集範例
應用程式呼叫**SQLGetTypeInfo**來判斷哪些資料類型支援的資料來源和這些資料類型的特性。 下表顯示範例結果集所傳回**SQLGetTypeInfo**支援 SQL_CHAR、 SQL_LONGVARCHAR、 SQL_DECIMAL、 SQL_REAL，如果是 SQL_DATETIME、 SQL_INTERVAL_YEAR 和 SQL_INTERVAL_DAY_TO_SECOND 為資料來源。  
  
|TYPE_NAME|DATA_TYPE|COLUMN_SIZE|LITERAL_PREFIX|LITERAL_SUFFIX|CREATE_PARAMS|NULLABLE|  
|----------------|----------------|------------------|---------------------|---------------------|--------------------|--------------|  
|"char"|SQL_CHAR|255|"'"|"'"|「 長度 」|SQL_TRUE|  
|"text"|SQL_LONGVARCHAR|2147483647|"'"|"'"|\<空值 >|SQL_TRUE|  
|[十進位]|SQL_DECIMAL|28|\<空值 >|\<空值 >|「 有效位數，<br />調整 」|SQL_TRUE|  
|「 實際 」|SQL_REAL|7|\<空值 >|\<空值 >|\<空值 >|SQL_TRUE|  
|"datetime"|SQL_TYPE_TIMESTAMP|23|"'"|"'"|\<空值 >|SQL_TRUE|  
|「 年度的間隔 YEAR()"|SQL_INTERVAL_YEAR|9|"'"|"'"|「 精確度 」|SQL_TRUE|  
|「 以 FRACTION(5) 間隔 DAY()"|SQL_INTERVAL_DAY_TO_SECOND|24|"'"|"'"|「 精確度 」|SQL_TRUE|  
  
|DATA_TYPE|CASE_SENSITIVE|SEARCHABLE|UNSIGNED_ATTRIBUTE|FIXED_PREC_SCALE|AUTO_UNIQUE_VALUE|LOCAL_TYPE_NAME|  
|----------------|---------------------|----------------|-------------------------|------------------------|-------------------------|-----------------------|  
|**SQL_CHAR**|SQL_FALSE|SQL_SEARCHABLE|\<空值 >|SQL_FALSE|\<空值 >|"char"|  
|**SQL_LONGVARCHAR**|SQL_FALSE|SQL_PRED_CHAR|\<空值 >|SQL_FALSE|\<空值 >|"text"|  
|**SQL_DECIMAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|[十進位]|  
|**SQL_REAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|「 實際 」|  
|**SQL_TYPE_TIMESTAMP**|SQL_FALSE|SQL_SEARCHABLE|\<空值 >|SQL_FALSE|\<空值 >|"datetime"|  
|**SQL_INTERVAL_YEAR**|SQL_FALSE|SQL_SEARCHABLE|\<空值 >|SQL_FALSE|\<空值 >|「 年度的間隔 YEAR()"|  
TERVAL_DAY_TO_SECOND**|SQL_FALSE|SQL_PRED_BASIC|\<空值 >|SQL_FALSE|\<空值 >|「 以 FRACTION(5) 間隔 DAY()"|  
  
|DATA_TYPE|MINIMUM_SCALE|MAXIMUM_SCALE|SQL_DATA_TYPE|SQL_DATETIME_SUB|NUM_PREC_RADIX|INTERVAL_PRECISION|  
|----------------|--------------------|--------------------|---------------------|------------------------|----------------------|-------------------------|  
|**SQL_CHAR**|\<空值 >|\<空值 >|SQL_CHAR|\<空值 >|\<空值 >|\<空值 >|  
|**SQL_LONGVARCHAR**|\<空值 >|\<空值 >|SQL_LONGVARCHAR|\<空值 >|\<空值 >|\<空值 >|  
|**SQL_DECIMAL**|0|28|SQL_DECIMAL|\<空值 >|10|\<空值 >|  
|**SQL_REAL**|\<空值 >|\<空值 >|SQL_REAL|\<空值 >|10|\<空值 >|  
|**SQL_TYPE_TIMESTAMP**|3|3|SQL_DATETIME|SQL_CODE_TIMESTAMP|\<空值 >|12|  
|**SQL_INTERVAL_YEAR**|0|0|SQL_INTERVAL|SQL_CODE_INTERVALYEAR|\<空值 >|9|  
ERVAL_DAY_TO_SECOND**|5|5|SQL_INTERVAL|SQL_CODE_INTERVALDAY_TO_SECOND|\<空值 >|9|
