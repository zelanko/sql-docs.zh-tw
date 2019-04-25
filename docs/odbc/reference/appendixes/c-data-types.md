---
title: C 資料類型 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3f948b50fae0995e16024ac41d8dd891630d1dbe
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62447537"
---
# <a name="c-data-types"></a>C 資料類型
ODBC C 資料類型表示用來將資料儲存在應用程式的 C 緩衝區的資料類型。  
  
 所有驅動程式必須支援所有的 C 資料類型。 這是必要的因為所有的驅動程式必須支援所有的 C 類型的轉換它們所支援的 SQL 類型，而且所有驅動程式支援至少一個字元 SQL 類型。 與所有的 C 類型可以轉換字元 SQL 類型，因為所有的驅動程式必須支援所有的 C 類型。  
  
 中指定的 C 資料類型**SQLBindCol**並**SQLGetData**函式與*TargetType*引數和**SQLBindParameter**函式搭配*ValueType*引數。 您也可以指定藉由呼叫**SQLSetDescField**設定 ARD 或 APD，或藉由呼叫 SQL_DESC_CONCISE_TYPE 欄位**SQLSetDescRec**具有*型別*引數 （和*子類型*引數，如有需要) 和*DescriptorHandle*引數設定為 ARD 或 APD 的控點。  
  
 下表列出 C 資料類型的有效型別識別的項。 資料表也會列出對應至每個識別項，而這個資料型別定義的 ODBC C 資料類型。  
  
|C 類型識別碼|ODBC C typedef|C 類型|  
|-----------------------|--------------------|------------|  
|SQL_C_CHAR|SQLCHAR *|unsigned char *|  
|SQL_C_WCHAR|SQLWCHAR *|wchar_t *|  
|SQL_C_SSHORT[j]|SQLSMALLINT|short int|  
|SQL_C_USHORT[j]|SQLUSMALLINT|不帶正負號的 short int|  
|SQL_C_SLONG[j]|SQLINTEGER|long int|  
|SQL_C_ULONG[j]|SQLUINTEGER|不帶正負號的 long int|  
|SQL_C_FLOAT|SQLREAL|FLOAT|  
|SQL_C_DOUBLE|SQLDOUBLE SQLFLOAT|double|  
|SQL_C_BIT|SQLCHAR|不帶正負號的 char|  
|SQL_C_STINYINT[j]|SQLSCHAR|帶正負號的 char|  
|SQL_C_UTINYINT[j]|SQLCHAR|不帶正負號的 char|  
|SQL_C_SBIGINT|SQLBIGINT|_int64[h]|  
|SQL_C_UBIGINT|SQLUBIGINT|不帶正負號的 _int64 [h]|  
|SQL_C_BINARY|SQLCHAR *|unsigned char *|  
|SQL_C_BOOKMARK[i]|書籤|不帶正負號的 long int [d]|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned char *|  
|所有 C 間隔資料類型|SQL_INTERVAL_STRUCT|請參閱[C 間隔結構](../../../odbc/reference/appendixes/c-interval-structure.md)區段中的，稍後在本附錄中。|  
  
 **C 類型識別碼**SQL_C_TYPE_DATE [c]  
  
 **ODBC C typedef** SQL_DATE_STRUCT  
  
 **C 類型**  
  
```  
struct tagDATE_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;    
} DATE_STRUCT;[a]  
```  
  
 **C 類型識別碼**SQL_C_TYPE_TIME [c]  
  
 **ODBC C typedef** SQL_TIME_STRUCT  
  
 **C 類型**  
  
```  
struct tagTIME_STRUCT {  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
} TIME_STRUCT;[a]  
```  
  
 **C 類型識別碼**SQL_C_TYPE_TIMESTAMP [c]  
  
 **ODBC C typedef** SQL_TIMESTAMP_STRUCT  
  
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
  
 **ODBC C typedef** SQL_NUMERIC_STRUCT  
  
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
  
 **ODBC C typedef** SQLGUID  
  
 **C 類型**  
  
```  
struct tagSQLGUID {  
   DWORD Data1;  
   WORD Data2;  
   WORD Data3;  
   BYTE Data4[8];  
} SQLGUID;[k]  
```  
  
 [a] 的年、 月、 日、 小時、 分鐘和 datetime C 資料類型中的第二個欄位的值必須符合西曆的條件約束。 (請參閱[西曆的條件約束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)本附錄中的更新版本。)  
  
 [[分數] 欄位的 b] 的值為十億分之一秒的範圍從 0 到 999999999 (1 小於 1 億) 數目。 比方說，半秒的部分欄位的值是 500,000,000，第二個正確率為 （1 毫秒） 為 1000000，如第二個百萬分之一秒 （一微秒） 是 1000，至於十億分之一秒 （一奈秒） 為 1。  
  
 [c] 於 ODBC 2。*x*，C date、 time 和 timestamp 資料類型為 SQL_C_DATE、 SQL_C_TIME 和 SQL_C_TIMESTAMP。  
  
 [d] ODBC 3 *.x*應用程式應該使用 SQL_C_VARBOOKMARK，不 SQL_C_BOOKMARK。 當 ODBC 3 *.x*應用程式會使用 ODBC 2。*x*驅動程式，而 ODBC 3 *.x*驅動程式管理員會將 SQL_C_VARBOOKMARK 對應至 SQL_C_BOOKMARK。  
  
 [e] 的號碼儲存在*val* SQL_NUMERIC_STRUCT 結構做為縮放的整數，在小的位元組由小到大模式 （最小顯著性位元組的最左邊位元組） 的欄位。 比方說，是 4，小數位數的數字 10.001 基底為 10，縮放至 100010 的整數。 因為這是以十六進位格式的 186AA，SQL_NUMERIC_STRUCT 中的值會是 AA 86 01 00 00...00 」，與 SQL_MAX_NUMERIC_LEN 所定義的位元組數目 **#define**。  
  
 如需詳細資訊**SQL_NUMERIC_STRUCT**，請參閱[做法：擷取數值資料使用 SQL_NUMERIC_STRUCT](retrieve-numeric-data-sql-numeric-struct-kb222831.md)。  
  
 [SQL_C_NUMERIC 資料 f] 的有效位數和小數位數欄位輸入 areused 從應用程式的輸入和輸出的驅動程式需要應用程式。 當驅動程式會將數字的值寫入至 SQL_NUMERIC_STRUCT 時，它會使用它自己的驅動程式專屬的預設做為值*精確度*欄位，而且它會在應用程式描述項 （SQL_DESC_SCALE 欄位中使用值預設為 0） 的*擴展*欄位。 應用程式可以提供自己的值的有效位數和小數位數設定 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 的應用程式描述項欄位。  
  
 [g] [符號] 欄位為 1，如果是正數，0，如果是負數。  
  
 [某些編譯器可能不提供小時] _int64。  
  
 [i] _SQL_C_BOOKMARK 已被取代，在 ODBC 3 *.x*。  
  
 [j] _SQL_C_SHORT、 SQL_C_LONG、 和 SQL_C_TINYINT 已取代 ODBC 中的帶正負號和不帶正負號的類型：SQL_C_SSHORT 和 SQL_C_USHORT、 SQL_C_SLONG 和 SQL_C_ULONG、 SQL_C_STINYINT 和 SQL_C_UTINYINT。 ODBC 3 *.x*驅動程式就應該使用 ODBC 2。*x*應用程式應支援 SQL_C_SHORT、 SQL_C_LONG、 和 SQL_C_TINYINT，，因為它們呼叫時，驅動程式管理員就會將透過傳遞給驅動程式。  
  
 [k] SQL_C_GUID 可以僅對 SQL_CHAR 或 SQL_WCHAR 轉換。  
  
 本章節包含下列主題。  
  
-   [64 位元整數結構](../../../odbc/reference/appendixes/64-bit-integer-structures.md)  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 中的 C 資料類型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)
