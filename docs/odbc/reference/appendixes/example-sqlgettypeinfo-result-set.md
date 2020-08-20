---
description: SQLGetTypeInfo 結果集範例
title: 範例 SQLGetTypeInfo 結果集 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2420713e0adb7f0b7c983243b4021ebbe9b141c0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466208"
---
# <a name="example-sqlgettypeinfo-result-set"></a>SQLGetTypeInfo 結果集範例
應用程式會呼叫 **SQLGetTypeInfo** 來判斷資料來源所支援的資料類型，以及這些資料類型的特性。 下錶針對支援 SQL_CHAR、SQL_LONGVARCHAR、SQL_DECIMAL、SQL_REAL、SQL_DATETIME、SQL_INTERVAL_YEAR 和 SQL_INTERVAL_DAY_TO_SECOND 的資料來源，顯示 **SQLGetTypeInfo** 所傳回的範例結果集。  
  
|TYPE_NAME|DATA_TYPE|COLUMN_SIZE|LITERAL_PREFIX|LITERAL_SUFFIX|CREATE_PARAMS|NULLABLE|  
|----------------|----------------|------------------|---------------------|---------------------|--------------------|--------------|  
|字元集|SQL_CHAR|255|"'"|"'"|長短|SQL_TRUE|  
|"text"|SQL_LONGVARCHAR|2147483647|"'"|"'"|\<Null>|SQL_TRUE|  
|表示|SQL_DECIMAL|28|\<Null>|\<Null>|降低<br />尺規|SQL_TRUE|  
|即時|SQL_REAL|7|\<Null>|\<Null>|\<Null>|SQL_TRUE|  
|datetime|SQL_TYPE_TIMESTAMP|23|"'"|"'"|\<Null>|SQL_TRUE|  
|「間隔年份 ( # A1 TO YEAR」|SQL_INTERVAL_YEAR|9|"'"|"'"|降低|SQL_TRUE|  
|「間隔日 ( # A1 到分數 (5) 」|SQL_INTERVAL_DAY_TO_SECOND|24|"'"|"'"|降低|SQL_TRUE|  
  
|DATA_TYPE|CASE_SENSITIVE|可搜尋|UNSIGNED_ATTRIBUTE|FIXED_PREC_SCALE|AUTO_UNIQUE_VALUE|LOCAL_TYPE_NAME|  
|----------------|---------------------|----------------|-------------------------|------------------------|-------------------------|-----------------------|  
|**SQL_CHAR**|SQL_FALSE|SQL_SEARCHABLE|\<Null>|SQL_FALSE|\<Null>|字元集|  
|**SQL_LONGVARCHAR**|SQL_FALSE|SQL_PRED_CHAR|\<Null>|SQL_FALSE|\<Null>|"text"|  
|**SQL_DECIMAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|表示|  
|**SQL_REAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|即時|  
|**SQL_TYPE_TIMESTAMP**|SQL_FALSE|SQL_SEARCHABLE|\<Null>|SQL_FALSE|\<Null>|datetime|  
|**SQL_INTERVAL_YEAR**|SQL_FALSE|SQL_SEARCHABLE|\<Null>|SQL_FALSE|\<Null>|「間隔年份 ( # A1 TO YEAR」|  
|**SQL_INTERVAL_DAY_TO_SECOND**|SQL_FALSE|SQL_PRED_BASIC|\<Null>|SQL_FALSE|\<Null>|「間隔日 ( # A1 到分數 (5) 」|  
  
|DATA_TYPE|MINIMUM_SCALE|MAXIMUM_SCALE|SQL_DATA_TYPE|SQL_DATETIME_SUB|NUM_PREC_RADIX|INTERVAL_PRECISION|  
|----------------|--------------------|--------------------|---------------------|------------------------|----------------------|-------------------------|  
|**SQL_CHAR**|\<Null>|\<Null>|SQL_CHAR|\<Null>|\<Null>|\<Null>|  
|**SQL_LONGVARCHAR**|\<Null>|\<Null>|SQL_LONGVARCHAR|\<Null>|\<Null>|\<Null>|  
|**SQL_DECIMAL**|0|28|SQL_DECIMAL|\<Null>|10|\<Null>|  
|**SQL_REAL**|\<Null>|\<Null>|SQL_REAL|\<Null>|10|\<Null>|  
|**SQL_TYPE_TIMESTAMP**|3|3|SQL_DATETIME|SQL_CODE_TIMESTAMP|\<Null>|12|  
|**SQL_INTERVAL_YEAR**|0|0|SQL_INTERVAL|SQL_CODE_INTERVALYEAR|\<Null>|9|  
|**SQL_INTERVAL_DAY_TO_SECOND**|5|5|SQL_INTERVAL|SQL_CODE_INTERVALDAY_TO_SECOND|\<Null>|9|
