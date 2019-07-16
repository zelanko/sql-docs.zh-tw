---
title: SQL 轉換為 C：日期時間間隔 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056866"
---
# <a name="sql-to-c-day-time-intervals"></a>SQL 轉換為 C：日期時間間隔

日期時間間隔的 ODBC SQL 資料類型的識別碼，如下所示：

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

下表顯示 ODBC C SQL 資料的日期時間間隔可能會轉換成的資料類型。 如需資料行和資料表中的詞彙說明，請參閱 <<c0> [ 轉換將資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。

|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|所有日期時間 C 間隔類型|不會被截斷尾端的欄位部分<br /><br /> 截斷尾端的欄位部分<br /><br /> 開頭有效位數不是目標的夠大，無法容納來自來源的資料|Data<br /><br /> 截斷的資料<br /><br /> 未定義|資料長度<br /><br /> 資料長度<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT[b] SQL_C_UTINYINT[b] SQL_C_USHORT[b] SQL_C_SHORT[b] SQL_C_SLONG[b] SQL_C_ULONG[b] SQL_C_NUMERIC[b] SQL_C_BIGINT[b]|間隔精確度是單一欄位，而不會截斷轉換資料<br /><br /> 間隔有效位數的單一欄位而且被截斷的小數<br /><br /> 間隔精確度是單一欄位和整個截斷<br /><br /> 未單一欄位間隔有效位數。|Data<br /><br /> 截斷的資料<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料類型的大小<br /><br /> 資料長度<br /><br /> 資料長度<br /><br /> C 資料類型的大小|n/a<br /><br /> 01S07<br /><br /> 22003<br /><br /> 07006|  
|SQL_C_BINARY|資料的位元組長度 < = *Columnsize*<br /><br /> 資料的位元組長度 > *Columnsize*|Data<br /><br /> 未定義|資料長度<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_CHAR|字元的位元組長度 < *Columnsize*<br /><br /> （相對於小數） 的整數位數 < *Columnsize*<br /><br /> 整體 （而不是小數） 數 > = *Columnsize*|Data<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料類型的大小<br /><br /> C 資料類型的大小<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|字元長度 < *Columnsize*<br /><br /> （相對於小數） 的整數位數 < *Columnsize*<br /><br /> 整體 （而不是小數） 數 > = *Columnsize*|Data<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料類型的大小<br /><br /> C 資料類型的大小<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
  
 [a] 的日期時間間隔 SQL 型別被可轉換成任何日期時間間隔 C 類型。  
  
 [b] 如果間隔有效位數的單一欄位 （其中一天、 小時、 分鐘或秒），間隔 SQL 型別被可轉換成任何精確數值 （SQL_C_STINYINT、 SQL_C_UTINYINT、 SQL_C_USHORT、 SQL_C_SHORT、 SQL_C_SLONG、 SQL_C_ULONG、 或 SQL_C_NUMERIC）。  
  
預設間隔 SQL 型別轉換為對應的 C 間隔資料類型。 應用程式再繫結資料行或參數 （或設定 SQL_DESC_DATA_PTR 欄位 ARD 適當記錄中） 以指向初始化 SQL_INTERVAL_STRUCT 結構 (或將指標傳遞給SQL_INTERVAL_STRUCT結構*TargetValuePtr*呼叫中的引數**SQLGetData**)。  
  
下列範例示範如何將資料從傳輸 SQL_INTERVAL_DAY_TO_MINUTE 類型的資料行到 SQL_INTERVAL_STRUCT 結構，它會回傳成 DAY_TO_HOUR 間隔。  

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
