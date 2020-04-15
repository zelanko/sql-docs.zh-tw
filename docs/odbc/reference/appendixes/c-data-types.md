---
title: C 資料類型 :微軟文件
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
- C buffers [ODBC]
ms.assetid: b681d260-3dbb-47df-a616-4910d727add7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 979bfe85e1e78b55718e1f12fdcfcc7583097bb4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292298"
---
# <a name="c-data-types"></a>C 資料類型
ODBC C 資料類型指示用於在應用程式中儲存數據的 C 緩衝區的數據類型。  
  
 所有驅動程式必須支援所有 C 資料類型。 這是必需的,因為所有驅動程式都必須支援它們支援的所有 C 類型,並且所有驅動程式都至少支援一個字元 SQL 類型。 由於字元 SQL 類型可以轉換為和從所有 C 類型,因此所有驅動程式都必須支援所有 C 類型。  
  
 C 數據類型在**SQLBindCol**和**SQLGetData**函數中指定,這些函數帶有*TargetType*參數,在**SQLBind 參數**函數中使用*ValueType*參數指定。 還可以通過調用**SQLSetDescField**來設置 ARD 或 APD 的SQL_DESC_CONCISE_TYPE欄位,或者使用*Type*參數(如果需要*的子類型*參數)調用**SQLSetDescRec**和設置為 ARD 或 APD 句柄*的描述符處理*參數來指定它。  
  
 下表列出了 C 資料類型的有效類型識別碼。 該表還列出了對應於每個識別符的 ODBC C 數據類型以及此數據類型的定義。  
  
|C 類型識別碼|ODBC C 型定義|C 類型|  
|-----------------------|--------------------|------------|  
|SQL_C_CHAR|SQLCHAR ||unsigned char *|  
|SQL_C_WCHAR|SQLWCHAR ||wchar_t *|  
|SQL_C_SSHORT[j]|SQLSMALLINT|short int|  
|SQL_C_USHORT[j]|SQLUSMALLINT|unsigned short int|  
|SQL_C_SLONG[j]|SQLINTEGER|long int|  
|SQL_C_ULONG[j]|SQLUINTEGER|unsigned long int|  
|SQL_C_FLOAT|SQLREAL|FLOAT|  
|SQL_C_DOUBLE|SQLDOUBLE,SQLFLOAT|double|  
|SQL_C_BIT|SQLCHAR|unsigned char|  
|SQL_C_STINYINT[j]|SQLSCHAR|signed char|  
|SQL_C_UTINYINT[j]|SQLCHAR|unsigned char|  
|SQL_C_SBIGINT|SQLBIGINT|_int64[h]|  
|SQL_C_UBIGINT|SQLUBIGINT|無符號_int64[h]|  
|SQL_C_BINARY|SQLCHAR ||unsigned char *|  
|SQL_C_BOOKMARK[i]|書籤|無符號長 int_d_|  
|SQL_C_VARBOOKMARK|SQLCHAR ||unsigned char *|  
|所有 C 間隔資料類型|SQL_INTERVAL_STRUCT|請參閱本附錄後面的[C 間隔結構](../../../odbc/reference/appendixes/c-interval-structure.md)部分。|  
  
 **C 類型識別碼**SQL_C_TYPE_DATE[c]  
  
 **ODBC C 型定義**SQL_DATE_STRUCT  
  
 **C 類型**  
  
```  
struct tagDATE_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;    
} DATE_STRUCT;[a]  
```  
  
 **C 類型識別碼**SQL_C_TYPE_TIME[c]  
  
 **ODBC C 型定義**SQL_TIME_STRUCT  
  
 **C 類型**  
  
```  
struct tagTIME_STRUCT {  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
} TIME_STRUCT;[a]  
```  
  
 **C 類型識別碼**SQL_C_TYPE_TIMESTAMP[c]  
  
 **ODBC C 型定義**SQL_TIMESTAMP_STRUCT  
  
 **C 類型**  
  
```  
struct tagTIMESTAMP_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
   SQLUINTEGER fraction;[b]   
} TIMESTAMP_STRUCT;[a]  
```  
  
 **C 類型識別碼**SQL_C_NUMERIC  
  
 **ODBC C 型定義**SQL_NUMERIC_STRUCT  
  
 **C 類型**  
  
```  
struct tagSQL_NUMERIC_STRUCT {  
   SQLCHAR precision;  
   SQLSCHAR scale;  
   SQLCHAR sign[g];  
   SQLCHAR val[SQL_MAX_NUMERIC_LEN];[e], [f]   
} SQL_NUMERIC_STRUCT;  
```  
  
 **C 類型識別碼**SQL_C_GUID  
  
 **ODBC C 型定義**SQLGUID  
  
 **C 類型**  
  
```  
struct tagSQLGUID {  
   DWORD Data1;  
   WORD Data2;  
   WORD Data3;  
   BYTE Data4[8];  
} SQLGUID;[k]  
```  
  
 [a] 日期時間 C 數據類型中的年份、月份、天、小時、分鐘和第二個字段的值必須符合公曆的約束。 ( 請參考此附錄後面的[公曆約束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)。  
  
 [b] 分數位段的值是每秒十億分之一的數值,範圍從 0 到 999,999,999(1 小於 10 億)。 例如,半秒的分數位段的值為 500,000,000,000,000,000,千分之一秒(一毫秒)為 1,000,000,000,百萬分之一秒(一微秒)的值為 1,000,十億分之一秒(一納秒)為 1。  
  
 [c] 在ODBC 2中。*x*,C 日期、時間和時間戳數據類型SQL_C_DATE、SQL_C_TIME和SQL_C_TIMESTAMP。  
  
 [d] ODBC 3 *.x*應用程式應使用SQL_C_VARBOOKMARK,而不是SQL_C_BOOKMARK。 當 ODBC 3 *.x*應用程式與 ODBC 2 配合使用時。*x*驅動程式,ODBC 3 *.x*驅動程式管理員將SQL_C_VARBOOKMARK映射到SQL_C_BOOKMARK。  
  
 [e] 數位以縮放整數的形式存儲在SQL_NUMERIC_STRUCT結構的*val*欄位中,採用小端整模式(最左側字節是最不重要的位元組)。 例如,數位 10.001 基 10(比例為 4)將縮放為 100010 整數。 由於這是十六進位格式的 186AA,因此SQL_NUMERIC_STRUCT的值將是"AA 86 01 00 00 ...00",**由SQL_MAX_NUMERIC_LEN定義**#define字节数。  
  
 有關**SQL_NUMERIC_STRUCT**的詳細資訊,請參閱[HOWTO:使用SQL_NUMERIC_STRUCT檢索數字資料](retrieve-numeric-data-sql-numeric-struct-kb222831.md)。  
  
 [f] SQL_C_NUMERIC資料類型的精度和縮放欄位用於從應用程式輸入以及從驅動程式輸出到應用程式。 當驅動程式將數值寫入SQL_NUMERIC_STRUCT時,它將使用自己的特定於驅動程式的預設值作為*精度*欄位的值,它將在*縮放*欄位的應用程式描述符的SQL_DESC_SCALE欄位中使用該值(預設值為 0)。 應用程式可以通過設置應用程式描述符的SQL_DESC_PRECISION和SQL_DESC_SCALE欄位來提供其自己的精度和縮放值。  
  
 [g] 符號欄位為 1(如果為正),0(如果為負)。  
  
 [h] _int64可能無法由某些編譯器提供。  
  
 [i] _SQL_C_BOOKMARK已在 ODBC 3 *.x*中棄用。  
  
 [j] _SQL_C_SHORT、SQL_C_LONG 和 SQL_C_TINYINT已在 ODBC 中替換為已簽名和未簽名的類型:SQL_C_SSHORT和SQL_C_USHORT、SQL_C_SLONG和SQL_C_ULONG以及SQL_C_STINYINT和SQL_C_UTINYINT。 應與 ODBC 2 配合使用的 ODBC 3 *.x*驅動程式。*x*應用程式應支援SQL_C_SHORT、SQL_C_LONG和SQL_C_TINYINT,因為調用它們時,驅動程式管理器會將它們傳遞給驅動程式。  
  
 [k] SQL_C_GUID只能轉換為SQL_CHAR或SQL_WCHAR。  
  
 本節包含以下主題。  
  
-   [64 位元整數結構](../../../odbc/reference/appendixes/64-bit-integer-structures.md)  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 中的 C 資料類型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)
