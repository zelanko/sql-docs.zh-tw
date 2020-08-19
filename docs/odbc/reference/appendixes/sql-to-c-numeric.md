---
description: SQL 到 C：數值
title: SQL 到 C：數值 |Microsoft Docs
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
ms.openlocfilehash: d48706eddabc71f28c84fae5623a8c9e440d8506
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429560"
---
# <a name="sql-to-c-numeric"></a>SQL 到 C：數值

數值 ODBC SQL 資料類型的識別碼如下：

- SQL_DECIMAL  
- SQL_BIGINT  
- SQL_NUMERIC  
- SQL_REAL  
- SQL_TINYINT  
- SQL_FLOAT  
- SQL_SMALLINT  
- SQL_DOUBLE SQL_INTEGER  

下表顯示可轉換數值 SQL 資料的 ODBC C 資料類型。 如需資料表中的資料行和詞彙的說明，請參閱將 [資料從 SQL 轉換成 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  

|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|字元位元組長度 < *BufferLength*<br /><br /> 相對於小數) 位數 < *BufferLength*的整體 (數目<br /><br /> 整個 (的數目，而不是小數) 位數 >= *BufferLength*|資料<br /><br /> 截斷的資料<br /><br /> 未定義|資料的長度（以位元組為單位）<br /><br /> 資料的長度（以位元組為單位）<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|字元長度 < *BufferLength*<br /><br /> 相對於小數) 位數 < *BufferLength*的整體 (數目<br /><br /> 整個 (的數目，而不是小數) 位數 >= *BufferLength*|資料<br /><br /> 截斷的資料<br /><br /> 未定義|資料的長度（以字元為單位）<br /><br /> 資料的長度（以字元為單位）<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_NUMERIC|未截斷的資料轉換 [a]<br /><br /> 以截斷小數數位 [a] 轉換的資料<br /><br /> 轉換資料會導致整個 (遺失，而不是小數) 位數 [a]|資料<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料類型的大小<br /><br /> C 資料類型的大小<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE|資料在轉換數位的資料類型範圍內 [a]<br /><br /> 資料超出要轉換數位的資料類型範圍 [a]|資料<br /><br /> 未定義|C 資料類型的大小<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_BIT|資料為0或 1 [a]<br /><br /> 資料大於0、小於2，且不等於 1 [a]<br /><br /> 資料小於0或大於或等於 2 [a]|資料<br /><br /> 截斷的資料<br /><br /> 未定義|1 [b]<br /><br /> 1 [b]<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_BINARY|資料 <的位元組長度 = *BufferLength*<br /><br /> 資料 > *BufferLength*的位元組長度|資料<br /><br /> 未定義|資料的長度<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_INTERVAL_MONTH [c] SQL_C_INTERVAL_YEAR [c] SQL_C_INTERVAL_DAY [c] SQL_C_INTERVAL_HOUR [c] SQL_C_INTERVAL_MINUTE [c] SQL_C_INTERVAL_SECOND [c]|未截斷資料<br /><br /> 小數秒部分已截斷<br /><br /> 截斷的數位的整個部分|資料<br /><br /> 截斷的資料<br /><br /> 未定義|資料的長度（以位元組為單位）<br /><br /> 資料的長度（以位元組為單位）<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_INTERVAL_YEAR_TO_MONTH SQL_C_INTERVAL_DAY_TO_HOUR SQL_C_INTERVAL_DAY_TO_MINUTE SQL_C_INTERVAL_DAY_TO_SECOND SQL_C_INTERVAL_HOUR_TO_MINUTE SQL_C_INTERVAL_HOUR_TO_SECOND|截斷的數位的整個部分|未定義|未定義|22015|  
  
 [a] 此轉換會忽略 *BufferLength* 的值。 驅動程式會假設 **TargetValuePtr* 的大小是 C 資料類型的大小。  
  
 [b] 這是對應 C 資料類型的大小。  
  
 [c] 只有精確數值資料類型才支援這項轉換 (SQL_DECIMAL、SQL_NUMERIC、SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER 和 SQL_BIGINT) 。 近似的數值資料類型 (SQL_REAL、SQL_FLOAT 或 SQL_DOUBLE) 並不支援。  

## <a name="sql_c_numeric-and-sqlsetdescfield"></a>SQL_C_NUMERIC 和 SQLSetDescField

 需要 [SQLSetDescField 函數](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 才能以 SQL_C_NUMERIC 值執行手動系結。  (請注意，SQLSetDescField 已加入 ODBC 3.0 中。 ) 若要執行手動系結，您必須先取得描述項控制碼。  

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
