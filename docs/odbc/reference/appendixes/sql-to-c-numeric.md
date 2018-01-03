---
title: "SQL 到 c： 數值 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data conversions from SQL to C types [ODBC], numeric
- numeric data type [ODBC], converting
- converting data from SQL to C types [ODBC], numeric
ms.assetid: 76f8b5d5-4bd0-4dcb-a90a-698340e0d36e
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3f09af0c145da9d435bce70619a5388f1cecb581
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sql-to-c-numeric"></a>SQL 到 c： 數字
針對數值的 ODBC SQL 資料類型的識別項是：  
  
 SQL_DECIMAL  
  
 SQL_BIGINT  
  
 SQL_NUMERIC  
  
 SQL_REAL  
  
 SQL_TINYINT  
  
 SQL_FLOAT  
  
 SQL_SMALLINT  
  
 SQL_DOUBLE SQL_INTEGER  
  
 下表顯示 ODBC C 資料類型可能會轉換數字的 SQL 資料。 如需的資料行和資料表中的詞彙說明，請參閱[轉換資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|字元位元組長度 < *Columnsize*<br /><br /> （相對於小數） 的整數位數 < *Columnsize*<br /><br /> （相對於小數） 的整數位數 > = *Columnsize*|data<br /><br /> 截斷的資料<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|字元長度 < *Columnsize*<br /><br /> （相對於小數） 的整數位數 < *Columnsize*<br /><br /> （相對於小數） 的整數位數 > = *Columnsize*|data<br /><br /> 截斷的資料<br /><br /> 未定義|以字元為單位的資料長度<br /><br /> 以字元為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_NUMERIC|資料轉換，而不會截斷 [a]<br /><br /> 資料截斷的小數數字 [a] 的轉換<br /><br /> 轉換的資料會導致遺失 （而不是小數） 的整數位數 [a]|data<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料類型的大小<br /><br /> C 資料類型的大小<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> 22003|  
_C_FLOAT<br /><br /> SQL_C_DOUBLE|資料範圍內的數字轉換的資料類型是 [a]<br /><br /> 資料超出範圍的數字轉換的資料類型 [a]|data<br /><br /> 未定義|C 資料類型的大小<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_BIT|資料是 0 或 1，[a]<br /><br /> 資料是大於 0，小於 2，且不等於 1，[a]<br /><br /> 資料是小於 0 或大於或等於 2，[a]|data<br /><br /> 截斷的資料<br /><br /> 未定義|1 [b]<br /><br /> 1 [b]<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_BINARY|資料的位元組長度 < = *Columnsize*<br /><br /> 資料的位元組長度 > *Columnsize*|data<br /><br /> 未定義|資料長度<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_INTERVAL_MONTH [c] [c] SQL_C_INTERVAL_YEAR SQL_C_INTERVAL_DAY [c] [c] SQL_C_INTERVAL_HOUR SQL_C_INTERVAL_MINUTE [c] SQL_C_INTERVAL_SECOND [c]|不會被截斷的資料<br /><br /> 截斷的小數秒數部分<br /><br /> 截斷的數字的整數部分|data<br /><br /> 截斷的資料<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> 22015|  
_C_INTERVAL_YEAR_TO_MONTH SQL_C_INTERVAL_DAY_TO_HOUR SQL_C_INTERVAL_DAY_TO_MINUTE SQL_C_INTERVAL_DAY_TO_SECOND SQL_C_INTERVAL_HOUR_TO_MINUTE SQL_C_INTERVAL_HOUR_TO_SECOND|截斷的數字的整數部分|未定義|未定義|22015|  
  
 [a] 的值*Columnsize*會忽略這項轉換。 驅動程式假設大小 **TargetValuePtr*是 C 資料類型的大小。  
  
 [b] 這是對應的 C 資料類型的大小。  
  
 [只為精確數值資料類型 （SQL_DECIMAL、 SQL_NUMERIC、 SQL_TINYINT、 SQL_SMALLINT、 SQL_INTEGER 和 SQL_BIGINT） 支援 c] 這個轉換。 不支援的近似數值資料類型 （SQL_REAL、 SQL_FLOAT 或 SQL_DOUBLE）。  
  
## <a name="sqlcnumeric-and-sqlsetdescfield"></a>SQL_C_NUMERIC 和 SQLSetDescField  
 [SQLSetDescField 函數](../../../odbc/reference/syntax/sqlsetdescfield-function.md)，才能執行手動的繫結 SQL_C_NUMERIC 值。 （請注意，在 ODBC 3.0 加入 SQLSetDescField）。若要執行手動的繫結，您必須先取得描述項控制代碼。  
  
```  
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
