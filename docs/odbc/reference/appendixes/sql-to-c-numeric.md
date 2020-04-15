---
title: SQL 到 C:數位 |微軟文件
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC], numeric
- numeric data type [ODBC], converting
- converting data from SQL to C types [ODBC], numeric
ms.assetid: 76f8b5d5-4bd0-4dcb-a90a-698340e0d36e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 36b24da4023a96b686742416b83bb5790e129278
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296408"
---
# <a name="sql-to-c-numeric"></a>SQL 到 C：數值

數位 ODBC SQL 資料類型的識別碼如下:

- SQL_DECIMAL  
- SQL_BIGINT  
- SQL_NUMERIC  
- SQL_REAL  
- SQL_TINYINT  
- SQL_FLOAT  
- SQL_SMALLINT  
- SQL_DOUBLESQL_INTEGER  

下表顯示了可轉換為數位 SQL 資料的 ODBC C 資料類型。 有關表中列與字語的說明,請參考[資料從 SQL 轉換為 C 資料型態](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  

|C 類型識別碼|測試|**目標價值Ptr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|字元位元組長度<*緩衝區長度*<br /><br /> *緩衝區長度*<整数(與小數)位數<br /><br /> >=*緩衝區長度*的整個(與小數)數字數|資料<br /><br /> 截斷的資料<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|字元長度<*緩衝區長度*<br /><br /> *緩衝區長度*<整数(與小數)位數<br /><br /> >=*緩衝區長度*的整個(與小數)數字數|資料<br /><br /> 截斷的資料<br /><br /> 未定義|字元中的資料長度<br /><br /> 字元中的資料長度<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_NUMERIC|在不截斷的情況下轉換的資料[a]<br /><br /> 使用小數數字截斷轉換的資料[a]<br /><br /> 資料轉換將導致整體數位(相對於小數)的丟失[a]|資料<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料型態大小<br /><br /> C 資料型態大小<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE|資料在要轉換數字的資料型態範圍內[a]<br /><br /> 資料不在要轉換數字的資料型態範圍之外[a]|資料<br /><br /> 未定義|C 資料型態大小<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_BIT|資料為 0 或 1[a]<br /><br /> 數據大於 0,小於 2,不等於 1[a]<br /><br /> 資料小於 0 或大於或等於 2[a]|資料<br /><br /> 截斷的資料<br /><br /> 未定義|1[b]<br /><br /> 1[b]<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_BINARY|資料<位元組長度 =*緩衝區長度*<br /><br /> >*緩衝區長度*的資料位元組長度|資料<br /><br /> 未定義|資料長度<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_INTERVAL_MONTH[c] SQL_C_INTERVAL_YEAR[c] SQL_C_INTERVAL_DAY[c] SQL_C_INTERVAL_HOUR[c] SQL_C_INTERVAL_MINUTE[c] SQL_C_INTERVAL_SECOND[c]|資料未截斷<br /><br /> 分段秒部分截斷<br /><br /> 截斷的整部份數字|資料<br /><br /> 截斷的資料<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_INTERVAL_YEAR_TO_MONTHSQL_C_INTERVAL_DAY_TO_HOURSQL_C_INTERVAL_DAY_TO_MINUTESQL_C_INTERVAL_HOUR_TO_MINUTESQL_C_INTERVAL_HOUR_TO_SECONDSQL_C_INTERVAL_DAY_TO_SECOND|截斷的整部份數字|未定義|未定義|22015|  
  
 [a] 此轉換將忽略*緩衝區長度*的值。 驅動程式假定 **目標價值Ptr*的大小是 C 資料類型的大小。  
  
 [b] 這是相應的 C 資料類型的大小。  
  
 [c] 僅支援精確數值數據類型(SQL_DECIMAL、SQL_NUMERIC、SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER和SQL_BIGINT) 轉換。 對於近似數值數據類型(SQL_REAL、SQL_FLOAT或SQL_DOUBLE),不支援它。  

## <a name="sql_c_numeric-and-sqlsetdescfield"></a>SQL_C_NUMERIC與 SQLSetDesc 欄位

 [SQLSetDescField 函數](../../../odbc/reference/syntax/sqlsetdescfield-function.md)需要執行具有SQL_C_NUMERIC值的手動綁定。 (請注意,SQLSetDescField 是在 ODBC 3.0 中添加的。要執行手動綁定,必須首先獲取描述符句柄。  

```cpp
if (fCType == SQL_C_NUMERIC) {   
   // special processing required for NUMERIC to get right scale & precision  
   // Modify the fields in the implicit application parameter descriptor  
   SQLHDESC hdesc=NULL;  
  
   // Use SQL_ATTR_APP_ROW_DESC for calls to SQLBindCol()  
   // Use SQL_ATTR_APP_PARAM_DESC for calls to SQLBindParameter()  
   //  
   // retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_APP_ROW_DESC, &hdesc, 0, NULL);  
   retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_APP_PARAM_DESC, &hdesc, 0, NULL);  
   if (!ODBC_CALL_SUCCESS(retcode)) {  
      printf ("\nSQLGetStmtAttr failed");  
      i = 1;  
      sqlstate[7] = '\0';  
      while (SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, sqlstate, &NativeError, wrkbuf, sizeof(wrkbuf), &len) != SQL_NO_DATA) {  
         printf("\niTestCase = %d Failed...Precision = %d, Scale = %d\nNativeError=%d, State=%s, \n  Message=%s",   
            iTestCase, Precision, Scale, NativeError, sqlstate, wrkbuf);  
         i++;  
      }  
      continue;  
   }  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_TYPE, (SQLPOINTER) SQL_C_NUMERIC, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_PRECISION, (SQLPOINTER)num.precision, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_SCALE, (SQLPOINTER)num.scale, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_DATA_PTR, (SQLPOINTER) &(num), sizeof(num));  
```
