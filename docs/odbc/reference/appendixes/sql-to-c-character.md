---
title: SQL 到 C:字元 |微軟文件
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], character
- character data type [ODBC]
- data conversions from SQL to C types [ODBC], character
ms.assetid: 7fdb7f38-b64d-48f2-bcb4-1ca96b2bbdb6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3486c0fcf5cefc39c4b85af814d7d3c1d609b4e3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296668"
---
# <a name="sql-to-c-character"></a>SQL 到 C：字元

字元 ODBC SQL 資料類型的識別碼如下:

- SQL_CHAR
- SQL_VARCHAR
- SQL_LONGVARCHAR
- SQL_WCHAR
- SQL_WVARCHAR
- SQL_WLONGVARCHAR

下表顯示了可轉換為字元 SQL 資料的 ODBC C 資料類型。 有關表中列與字語的說明,請參考[資料從 SQL 轉換為 C 資料型態](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  

|C 類型識別碼|測試|目標價值Ptr|StrLen_or_IndPtr|SQLSTATE|
|:----------------|:---|:-------------|:---------------|:-------|
|SQL_C_CHAR|<*緩衝區長度*的資料位元組長度<br /><br /> 資料>位元組長度 =*緩衝區長度*|資料<br /><br /> 截斷的資料|以位元組為單位的資料長度<br /><br /> 以位元組為單位的資料長度|n/a<br /><br /> 01004|  
|SQL_C_WCHAR|<*緩衝區長度*的資料字元長度<br /><br /> 資料>的字元長度 =*緩衝區長度*|資料<br /><br /> 截斷的資料|字元中的資料長度<br /><br /> 字元中的資料長度|n/a<br /><br /> 01004|  
|SQL_C_STINYINTSQL_C_UTINYINT SQL_C_TINYINT SQL_C_USHORT SQL_C_SSHORTSQL_C_SBIGINTSQL_C_UBIGINTSQL_C_UBIGINTSQL_C_UBIGINTSQL_C_LONGSQL_C_LONGSQL_C_LONG SQL_C_NUMERIC SQL_C_ULONG SQL_C_SLONGSQL_C_SHORTSQL_C_SHORT|在不截斷的情況下轉換的資料[b]<br /><br /> 使用小數數字截斷轉換的資料[a]<br /><br /> 資料轉換將導致整體數位(相對於小數)的丟失[a]<br /><br /> 資料不是*數字文字*[b]|資料<br /><br /> 截斷的資料<br /><br /> 未定義<br /><br /> 未定義|C 資料型態的位元組數<br /><br /> C 資料型態的位元組數<br /><br /> 未定義<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_FLOATSQL_C_DOUBLE|資料在要轉換數字的資料型態範圍內[a]<br /><br /> 資料不在要轉換數字的資料型態範圍之外[a]<br /><br /> 資料不是*數字文字*[b]|資料<br /><br /> 未定義<br /><br /> 未定義|C 資料型態大小<br /><br /> 未定義<br /><br /> 未定義|n/a<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BIT|資料為 0 或 1<br /><br /> 數據大於 0,小於 2,不等於 1<br /><br /> 資料小於 0 或大於或等於 2<br /><br /> 資料不是*數字文字*|資料<br /><br /> 截斷的資料<br /><br /> 未定義<br /><br /> 未定義|1[b]<br /><br /> 1[b]<br /><br /> 未定義<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BINARY|資料<位元組長度 =*緩衝區長度*<br /><br /> >*緩衝區長度*的資料位元組長度|資料<br /><br /> 截斷的資料|以位元組為單位的資料長度<br /><br /> 資料長度|n/a<br /><br /> 01004|  
|SQL_C_TYPE_DATE|資料值是合法*的日期值*[a]<br /><br /> 資料值是有效的*時間戳值*;時間部分為零[a]<br /><br /> 資料值是有效的*時間戳值*;時間部分是非零[a],[c]<br /><br /> 資料值不是合法*的日期值*或*時間戳值*[a]|資料<br /><br /> 資料<br /><br /> 截斷的資料<br /><br /> 未定義|6[b]<br /><br /> 6[b]<br /><br /> 6[b]<br /><br /> 未定義|n/a<br /><br /> n/a<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIME|資料值是有效的*時間值,小數秒值為 0*[a]<br /><br /> 資料值是有效的*時間戳值或有效的時間值*;小數秒部分為零[a],[d]<br /><br /> 資料值是有效的*時間戳值*;小數秒部分是非零[a],[d],[e]<br /><br /> 資料值不是有效的*時間值*或*時間戳值*[a]|資料<br /><br /> 資料<br /><br /> 截斷的資料<br /><br /> 未定義|6[b]<br /><br /> 6[b]<br /><br /> 6[b]<br /><br /> 未定義|n/a<br /><br /> n/a<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIMESTAMP|資料值是有效的*時間戳值或有效的時間值*;分數秒部份未截斷 [a]<br /><br /> 資料值是有效的*時間戳值或有效的時間值*;小數秒部分截斷[a]<br /><br /> 資料值是合法*的日期值*[a]<br /><br /> 資料值是有效的*時間值*[a]<br /><br /> 資料值不是合法*的日期值*,*時間值*或*時間戳值*[a]|資料<br /><br /> 截斷的資料<br /><br /> 資料[f]<br /><br /> 資料[g]<br /><br /> 未定義|16[b]<br /><br /> 16[b]<br /><br /> 16[b]<br /><br /> 16[b]<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> n/a<br /><br /> n/a<br /><br /> 22018|  
|所有 C 間隔型態|資料值是有效的*間隔值*;無截斷<br /><br /> 資料值是有效的*間隔值*;截斷一個或多個尾隨欄位<br /><br /> 數據是有效的間隔;前導場顯著精度丟失<br /><br /> 資料值不是有效的間隔值|資料<br /><br /> 截斷的資料<br /><br /> 未定義<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 以位元組為單位的資料長度<br /><br /> 未定義<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> 22015<br /><br /> 22018|  
|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|

 [a] 此轉換將忽略*緩衝區長度*的值。 驅動程式假定 **目標價值Ptr*的大小是 C 資料類型的大小。  
  
 [b] 這是相應的 C 資料類型的大小。  
  
 [c]*時間戳值*的時間部分被截斷。  
  
 [d]*時間戳值*的日期部分將被忽略。  
  
 [e] 時間戳的小秒部分被截斷。  
  
 [f] 時間戳結構的時間欄位設置為零。  
  
 [g] 時間戳結構的日期欄位設定為當前日期。  

**額外空間**

將 SQL 字元資料轉換為以下任一類型時,會忽略前導空格與尾隨空白:

- date
- NUMERIC
- time
- timestamp
- 間隔 C 資料
