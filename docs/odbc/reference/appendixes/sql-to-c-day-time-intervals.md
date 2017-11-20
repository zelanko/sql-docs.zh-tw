---
title: "SQL 到 c： 日期時間間隔 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from SQL to C types [ODBC], day-time intervals
- day-time intervals [ODBC]
- data conversions from SQL to C types [ODBC], day-time intervals
- intervals [ODBC], converting
ms.assetid: 8ea84d69-2292-4128-89a0-f184f68abb98
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cf87c74d4b2667daa032e814bae3655b83a46c31
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sql-to-c-day-time-intervals"></a>SQL 到 c： 日期時間間隔
日期時間間隔 ODBC SQL 資料類型的識別項是：  
  
 SQL_INTERVAL_DAY  
  
 SQL_INTERVAL_DAY_TO_MINUTE  
  
 SQL_INTERVAL_HOUR  
  
 SQL_INTERVAL_DAY_TO_SECOND  
  
 SQL_INTERVAL_MINUTE  
  
 SQL_INTERVAL_HOUR_TO_MINUTE  
  
 SQL_INTERVAL_SECOND  
  
 SQL_INTERVAL_HOUR_TO_SECOND  
  
 SQL_INTERVAL_DAY_TO_HOUR  
  
 SQL_INTERVAL_MINUTE_TO_SECOND  
  
 下表顯示 ODBC C 資料類型可能會轉換日期時間間隔的 SQL 資料。 如需的資料行和資料表中的詞彙說明，請參閱[轉換資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|所有的日期時間 C 間隔類型|不會被截斷尾端欄位部分<br /><br /> 截斷尾端欄位部分<br /><br /> 開頭有效位數不是目標的不夠大，無法保存資料來源|data<br /><br /> 截斷的資料<br /><br /> 未定義|資料長度<br /><br /> 資料長度<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT [b] SQL_C_UTINYINT [b] SQL_C_USHORT [b] SQL_C_SHORT [b] SQL_C_SLONG [b] SQL_C_ULONG [b] SQL_C_NUMERIC [b] SQL_C_BIGINT [b]|間隔有效位數的單一欄位，而不會截斷轉換資料<br /><br /> 間隔有效位數是單一欄位，並截斷小數<br /><br /> 間隔精確度是單一欄位與遭到截斷整個<br /><br /> 間隔精確度不是單一欄位|data<br /><br /> 截斷的資料<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料類型的大小<br /><br /> 資料長度<br /><br /> 資料長度<br /><br /> C 資料類型的大小|n/a<br /><br /> 01S07<br /><br /> 22003<br /><br /> 07006|  
|SQL_C_BINARY|資料的位元組長度 < = *Columnsize*<br /><br /> 資料的位元組長度 > *Columnsize*|data<br /><br /> 未定義|資料長度<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_CHAR|字元位元組長度 < *Columnsize*<br /><br /> （相對於小數） 的整數位數 < *Columnsize*<br /><br /> （相對於小數） 的整數位數 > = *Columnsize*|data<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料類型的大小<br /><br /> C 資料類型的大小<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
_C_WCHAR|字元長度 < *Columnsize*<br /><br /> （相對於小數） 的整數位數 < *Columnsize*<br /><br /> （相對於小數） 的整數位數 > = *Columnsize*|data<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料類型的大小<br /><br /> C 資料類型的大小<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
  
 [a] 的一天時間間隔 SQL 型別可以轉換成任何一天時間間隔 C 類型。  
  
 [b] 如果間隔有效位數 （其中日、 小時、 分鐘或秒） 的單一欄位，間隔 SQL 型別可以轉換成任何 （SQL_C_STINYINT、 SQL_C_UTINYINT、 SQL_C_USHORT、 SQL_C_SHORT、 SQL_C_SLONG、 SQL_C_ULONG、 或 SQL_C_NUMERIC） 的精確數值。  
  
 SQL 類型的間隔預設值轉換為對應 C 間隔資料型別。 應用程式再將繫結資料行或參數 （或設定 SQL_DESC_DATA_PTR 欄位 ARD 適當記錄中） 以指向初始化 SQL_INTERVAL_STRUCT 結構 (或將指標傳遞至SQL_INTERVAL_STRUCT結構*TargetValuePtr*呼叫中的引數**SQLGetData**)。  
  
 下列範例會示範如何將資料從傳輸 SQL_INTERVAL_DAY_TO_MINUTE 類型的資料行成為 SQL_INTERVAL_STRUCT 結構，它會以 DAY_TO_HOUR 間隔。  
  
```  
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

