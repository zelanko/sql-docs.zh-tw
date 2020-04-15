---
title: SQL 到 C:白天間隔 |微軟文件
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], day-time intervals
- day-time intervals [ODBC]
- data conversions from SQL to C types [ODBC], day-time intervals
- intervals [ODBC], converting
ms.assetid: 8ea84d69-2292-4128-89a0-f184f68abb98
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1318da5285ba2384dd23e4c235e698aa72c7658e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296468"
---
# <a name="sql-to-c-day-time-intervals"></a>SQL 到 C：日期時間間隔

白天間隔 ODBC SQL 資料類型的識別碼如下:

- SQL_INTERVAL_DAY
- SQL_INTERVAL_DAY_TO_MINUTE
- SQL_INTERVAL_HOUR
- SQL_INTERVAL_DAY_TO_SECOND
- SQL_INTERVAL_MINUTE
- SQL_INTERVAL_HOUR_TO_MINUTE
- SQL_INTERVAL_SECOND
- SQL_INTERVAL_HOUR_TO_SECOND
- SQL_INTERVAL_DAY_TO_HOUR
- SQL_INTERVAL_MINUTE_TO_SECOND

下表顯示了可以轉換為白天間隔 SQL 資料的 ODBC C 數據類型。 有關表中列與字語的說明,請參考[資料從 SQL 轉換為 C 資料型態](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。

|C 類型識別碼|測試|**目標價值Ptr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|所有 Zoccc|尾隨欄位部份未截斷<br /><br /> 尾隨欄位部份截斷<br /><br /> 目標的領先精度不足以儲存來自源的資料|資料<br /><br /> 截斷的資料<br /><br /> 未定義|資料長度<br /><br /> 資料長度<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT[b] SQL_C_UTINYINT[b] SQL_C_USHORT[b] SQL_C_SHORT[b] SQL_C_SLONG[b] SQL_C_ULONG[b] SQL_C_NUMERIC[b] SQL_C_BIGINT[b]|間隔精度是單個字段,數據在不截斷的情況下被轉換<br /><br /> 間隔精度為單個字段,並截斷小數<br /><br /> 間隔精度是單個字段,並截斷整個<br /><br /> 間隔精度不是單個字段|資料<br /><br /> 截斷的資料<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料型態大小<br /><br /> 資料長度<br /><br /> 資料長度<br /><br /> C 資料型態大小|n/a<br /><br /> 01S07<br /><br /> 22003<br /><br /> 07006|  
|SQL_C_BINARY|資料<位元組長度 =*緩衝區長度*<br /><br /> >*緩衝區長度*的資料位元組長度|資料<br /><br /> 未定義|資料長度<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_CHAR|字元位元組長度<*緩衝區長度*<br /><br /> *緩衝區長度*<整数(與小數)位數<br /><br /> >=*緩衝區長度*的整個(與小數)數字數|資料<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料型態大小<br /><br /> C 資料型態大小<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|字元長度<*緩衝區長度*<br /><br /> *緩衝區長度*<整数(與小數)位數<br /><br /> >=*緩衝區長度*的整個(與小數)數字數|資料<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料型態大小<br /><br /> C 資料型態大小<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
  
 [a] 日間間隔 SQL 類型可以轉換為任何日間間隔 C 類型。  
  
 [b] 如果間隔精度是單個字段(DAY、HOUR、MINUTE 或秒),則可以將間隔 SQL 類型轉換為任何精確數值(SQL_C_STINYINT、SQL_C_UTINYINT、SQL_C_USHORT、SQL_C_SHORT、SQL_C_SLONG、SQL_C_ULONG 或SQL_C_NUMERIC)。  
  
間隔 SQL 類型的預設轉換為相應的 C 間隔數據類型。 然後,應用程式綁定列或參數(或在ARD的適當記錄中設置SQL_DESC_DATA_PTR欄位),以指向初始化SQL_INTERVAL_STRUCT結構(或將指向SQL_INTERVAL_STRUCT結構的指標作為對**SQLGetData**調用中的*TargetValuePtr*參數)。  
  
下面的範例展示如何將資料從類型SQL_INTERVAL_DAY_TO_MINUTE列傳輸到SQL_INTERVAL_STRUCT結構中,以便以DAY_TO_HOUR間隔的形式返回。  

```cpp
SQL_INTERVAL_STRUCT is;  
SQLINTEGER    cbValue;  
SQLUINTEGER   days, hours;  
  
// Execute a select statement; "interval_column" is a column  
// whose data type is SQL_INTERVAL_DAY_TO_MINUTE.  
SQLExecDirect(hstmt, "SELECT interval_column FROM table", SQL_NTS);  
  
// Bind  
SQLBindCol(hstmt, 1, SQL_C_INTERVAL_DAY_TO_MINUTE, &is, sizeof(SQL_INTERVAL_STRUCT), &cbValue);  
  
// Fetch  
SQLFetch(hstmt);  
  
// Process data  
days = is.intval.day_second.day;  
hours = is.intval.day_second.hour;  
```
