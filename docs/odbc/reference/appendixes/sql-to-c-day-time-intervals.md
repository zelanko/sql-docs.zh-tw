---
title: SQL 到 C：日期時間間隔 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db39751059d84e4e3a7950acbbbcb7f1a2b0b00d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68056866"
---
# <a name="sql-to-c-day-time-intervals"></a>SQL 到 C：日期時間間隔

日期時間間隔 ODBC SQL 資料類型的識別碼如下：

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

下表顯示可以轉換日期時間間隔 SQL 資料的 ODBC C 資料類型。 如需資料表中的資料行和詞彙的說明，請參閱將[資料從 SQL 轉換成 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。

|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|所有日期時間 C 間隔類型|尾端欄位部分未截斷<br /><br /> 尾端欄位部分已截斷<br /><br /> 目標的前置精確度不夠大，無法保存來源的資料|資料<br /><br /> 截斷的資料<br /><br /> 未定義|資料的長度<br /><br /> 資料的長度<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT [b] SQL_C_UTINYINT [b] SQL_C_USHORT [b] SQL_C_SHORT [b] SQL_C_SLONG [b] SQL_C_ULONG [b] SQL_C_NUMERIC [b] SQL_C_BIGINT [b]|間隔精確度是單一欄位，而且資料已轉換而不截斷<br /><br /> 間隔精確度是單一欄位和截斷的小數<br /><br /> 間隔精確度是單一欄位，而全部截斷<br /><br /> 間隔精確度不是單一欄位|資料<br /><br /> 截斷的資料<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料類型的大小<br /><br /> 資料的長度<br /><br /> 資料的長度<br /><br /> C 資料類型的大小|n/a<br /><br /> 01S07<br /><br /> 22003<br /><br /> 07006|  
|SQL_C_BINARY|資料 <的位元組長度 = *BufferLength*<br /><br /> 資料 > *BufferLength*的位元組長度|資料<br /><br /> 未定義|資料的長度<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_CHAR|字元位元組長度 < *BufferLength*<br /><br /> < *BufferLength*的整體數目（相對於小數）位數<br /><br /> 整體數目（相對於小數）數位 >= *BufferLength*|資料<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料類型的大小<br /><br /> C 資料類型的大小<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|字元長度 < *BufferLength*<br /><br /> < *BufferLength*的整體數目（相對於小數）位數<br /><br /> 整體數目（相對於小數）數位 >= *BufferLength*|資料<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料類型的大小<br /><br /> C 資料類型的大小<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
  
 [a] 日期時間間隔 SQL 類型可以轉換成任何日期時間間隔 C 類型。  
  
 [b] 如果間隔精確度是單一欄位（一天、小時、分鐘或秒），間隔 SQL 類型就可以轉換成任何精確的數值（SQL_C_STINYINT、SQL_C_UTINYINT、SQL_C_USHORT、SQL_C_SHORT、SQL_C_SLONG、SQL_C_ULONG 或 SQL_C_NUMERIC）。  
  
Interval SQL 類型的預設轉換是對應的 C interval 資料類型。 然後，應用程式會系結資料行或參數（或將 ARD 的適當記錄中的 SQL_DESC_DATA_PTR 欄位）指向已初始化的 SQL_INTERVAL_STRUCT 結構（或在**SQLGetData**的呼叫中，將 SQL_ INTERVAL_STRUCT 結構的指標傳遞為*TargetValuePtr*引數）。  
  
下列範例示範如何從 SQL_INTERVAL_DAY_TO_MINUTE 類型的資料行，將資料傳送至 SQL_INTERVAL_STRUCT 結構，使其回到 DAY_TO_HOUR 的間隔。  

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
