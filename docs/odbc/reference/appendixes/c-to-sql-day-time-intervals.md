---
description: C 到 SQL：日期時間間隔
title: C 到 SQL：日期時間間隔 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- day-time intervals [ODBC]
- data conversions from C to SQL types [ODBC], day-time intervals
- converting data from c to SQL types [ODBC], day-time intervals
- intervals [ODBC], converting
ms.assetid: f9ee1ddb-dec7-4f78-b6e2-5ba34e7d6f59
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aba5bb40a34f100cf33d5c07fb6e796b227904dc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499991"
---
# <a name="c-to-sql-day-time-intervals"></a>C 到 SQL：日期時間間隔
日期時間間隔 ODBC C 資料類型的識別碼如下：  
  
 SQL_C_INTERVAL_DAY  
  
 SQL_C_INTERVAL_HOUR  
  
 SQL_C_INTERVAL_MINUTE  
  
 SQL_C_INTERVAL_SECOND  
  
 SQL_C_INTERVAL_DAY_TO_HOUR  
  
 SQL_C_INTERVAL_DAY_TO_MINUTE  
  
 SQL_C_INTERVAL_DAY_TO_SECOND  
  
 SQL_C_INTERVAL_HOUR_TO_MINUTE  
  
 SQL_C_INTERVAL_HOUR_TO_SECOND  
  
 SQL_C_INTERVAL_MINUTE_TO_SECOND  
  
 下表顯示 ODBC SQL 資料類型，可以轉換的間隔 C 資料。 如需資料表中的資料行和詞彙的說明，請參閱將 [資料從 C 轉換成 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 類型識別碼|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR [a]<br /><br /> SQL_VARCHAR [a]<br /><br /> SQL_LONGVARCHAR [a]|資料行位元組長度 >= 字元位元組長度<br /><br /> 資料行位元組長度 < 字元位元組長度 [a]<br /><br /> 資料值不是有效的間隔常值|n/a<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR [a]<br /><br /> SQL_WVARCHAR [a]<br /><br /> SQL_WLONGVARCHAR [a]|資料行字元長度 >= 字元的資料長度<br /><br /> 資料行字元長度 < 資料的字元長度 [a]<br /><br /> 資料值不是有效的間隔常值|n/a<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT [b]<br /><br /> SQL_SMALLINT [b] SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b] SQL_NUMERIC [b]<br /><br /> SQL_DECIMAL [b]|單一欄位間隔的轉換未產生整數的截斷<br /><br /> 轉換導致整個數位截斷|n/a<br /><br /> 22003|  
|SQL_INTERVAL_DAY<br /><br /> SQL_INTERVAL_HOUR<br /><br /> SQL_INTERVAL_MINUTE<br /><br /> SQL_INTERVAL_SECOND<br /><br /> SQL_INTERVAL_DAY_TO_HOUR<br /><br /> SQL_INTERVAL_DAY_TO_MINUTE<br /><br /> SQL_INTERVAL_DAY_TO_SECOND<br /><br /> SQL_INTERVAL_HOUR_TO_MINUTE<br /><br /> SQL_INTERVAL_HOUR_TO_SECOND<br /><br /> SQL_INTERVAL_MINUTE_TO_SECOND|已轉換資料值，但未截斷任何欄位<br /><br /> 轉換期間截斷了一或多個資料值欄位|n/a<br /><br /> 22015|  
  
 [a] 所有 C 間隔資料類型都可以轉換成字元資料類型。  
  
 [b] 如果間隔結構中的類型欄位使間隔是單一欄位 (SQL_DAY、SQL_HOUR、SQL_MINUTE 或 SQL_SECOND) ，則間隔 C 類型可以轉換成任何精確數值 (SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、SQL_BIGINT、SQL_DECIMAL 或 SQL_NUMERIC) 。  
  
 間隔 C 類型的預設轉換是對應的日期時間間隔 SQL 類型。  
  
 從 interval C 資料類型轉換資料時，驅動程式會忽略長度/指標值，並假設資料緩衝區的大小是 interval C 資料類型的大小。 長度/指標值會傳遞至**SQLPutData**中的*StrLen_or_Ind*引數，以及在**SQLBindParameter**中使用*StrLen_or_IndPtr*引數指定的緩衝區。 資料緩衝區會以**SQLPutData**中的*DataPtr*引數和**SQLBindParameter**中的*ParameterValuePtr*引數來指定。  
  
 下列範例示範如何將儲存在 SQL_INTERVAL_STRUCT 結構中的間隔 C 資料傳送至資料庫資料行。 間隔結構包含 DAY_TO_SECOND 間隔;它會儲存在 SQL_INTERVAL_DAY_TO_MINUTE 類型的資料庫資料行中。  
  
```  
SQL_INTERVAL_STRUCT is;  
SQLINTEGER cbValue;  
  
// Initialize the interval struct to contain the DAY_TO_SECOND  
// interval "154 days, 22 hours, 44 minutes, and 10 seconds"  
is.intval.day_second.day      = 154;  
is.intval.day_second.hour     = 22;  
is.intval.day_second.minute   = 44;  
is.intval.day_second.second   = 10;  
is.interval_sign              = SQL_FALSE;  
  
// Bind the dynamic parameter  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_INTERVAL_DAY_TO_SECOND,  
                  SQL_INTERVAL_DAY_TO_MINUTE, 0, 0, &is,  
                  sizeof(SQL_INTERVAL_STRUCT), &cbValue);  
  
// Execute an insert statement; "interval_column" is a column  
// whose data type is SQL_INTERVAL_DAY_TO_MINUTE.  
SQLExecDirect(hstmt,"INSERT INTO table(interval_column) VALUES (?)",SQL_NTS);  
```
