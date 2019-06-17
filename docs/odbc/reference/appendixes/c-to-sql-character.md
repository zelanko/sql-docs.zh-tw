---
title: C 轉換為 SQL：字元 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- character data type [ODBC]
- data conversions from C to SQL types [ODBC], character
- converting data from c to SQL types [ODBC], character
ms.assetid: be66188a-ebdb-4c9e-af72-c379886766fa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0158da62ed360e926cdb5382b89b1491c0723550
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63201632"
---
# <a name="c-to-sql-character"></a>C 轉換為 SQL：字元
ODBC C 資料類型的字元的識別項是：  
  
 SQL_C_CHAR  
  
 SQL_C_WCHAR  
  
 下表顯示 ODBC SQL C 字元資料可能會轉換成的資料類型。 如需資料行和資料表中的詞彙說明，請參閱 <<c0> [ 轉換將資料從 C 到 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
> [!NOTE]  
>  當字元 C 資料轉換到 Unicode SQL 資料時，Unicode 資料的長度必須是偶數。  
  
|SQL 型別識別項|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|資料的位元組長度 < = 資料行長度。<br /><br /> 資料的位元組長度 > 資料行長度。|n/a<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|字元資料的長度 < = 資料行長度。<br /><br /> 字元資料的長度 > 資料行長度。|n/a<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT|而不會截斷轉換資料<br /><br /> 截斷的小數數字 [e] 與轉換資料<br /><br /> 資料轉換會導致整體 （而不是小數） 數字 [e] 遺失<br /><br /> 資料值不是*數值常值*|n/a<br /><br /> 22001<br /><br /> 22001<br /><br /> 22018|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|資料是數值轉換的資料類型的範圍內<br /><br /> 資料超出範圍的數值轉換的資料類型<br /><br /> 資料值不是*數值常值*|n/a<br /><br /> 22003<br /><br /> 22018|  
|SQL_BIT|資料是 0 或 1<br /><br /> 資料是大於 0，小於 2，且不等於 1<br /><br /> 小於 0 或大於或等於 2，資料是<br /><br /> 資料不是*數值常值*|n/a<br /><br /> 22001<br /><br /> 22003<br /><br /> 22018|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|（資料中的位元組長度） / 2 < = 資料行的位元組長度<br /><br /> （資料中的位元組長度） / 2 > 資料行的位元組長度<br /><br /> 資料值不是十六進位值|n/a<br /><br /> 22001<br /><br /> 22018|  
|SQL_TYPE_DATE|資料值是有效*ODBC 日期常值*<br /><br /> 資料值是有效*ODBC 時間戳記值*; 時間部分為零<br /><br /> 資料值是有效*ODBC 時間戳記值*; 時間部分為非零值 [a]<br /><br /> 資料值不是有效*ODBC 日期常值*或*ODBC 時間戳記值*|n/a<br /><br /> n/a<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIME|資料值是有效*ODBC 時間常值*<br /><br /> 資料值是有效*ODBC 時間戳記值*; 小數秒數部分為零個 [b]<br /><br /> 資料值是有效*ODBC 時間戳記值*; 小數秒數部分為非零值 [b]<br /><br /> 資料值不是有效*ODBC 時間常值*或*ODBC 時間戳記值*|n/a<br /><br /> n/a<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIMESTAMP|資料值是有效*ODBC 時間戳記值*; 小數秒部分不會被截斷<br /><br /> 資料值是有效*ODBC 時間戳記值*; 小數秒部分截斷<br /><br /> 資料值是有效*ODBC 日期常值*[c]<br /><br /> 資料值是有效*ODBC 時間常值*[d]<br /><br /> 資料值不是有效*ODBC 日期常值*， *ODBC 時間常值*，或*ODBC 時間戳記值*|n/a<br /><br /> 22008<br /><br /> n/a<br /><br /> n/a<br /><br /> 22018|  
|所有 SQL 間隔類型|資料值是有效*間隔值*; 不截斷，就會發生<br /><br /> 資料值是有效*間隔值*; 中的其中一個欄位的值會被截斷<br /><br /> 資料值不是常值的有效間隔|n/a<br /><br /> 22015<br /><br /> 22018|  
  
 [a] 時間戳記的時間部分會被截斷。  
  
 [時間戳記 b] 的日期部分會被忽略。  
  
 [c] 時間部分的時間戳記會設定為零。  
  
 [d] 的日期部分的時間戳記已設定為目前的日期。  
  
 [e] 的驅動程式/資料來源實際上會等待直到收到整個字串為止 (即使字元資料，會藉由呼叫傳送分段**SQLPutData**) 然後再嘗試執行轉換。  
  
 C 字元資料轉換為數值、 日期、 時間戳記的 SQL 資料時，會忽略開頭和尾端空白。  
  
 當字元 C 資料轉換為二進位的 SQL 資料時，每兩個位元組的字元資料會轉換成單一位元組 （8 位元） 的二進位資料。 每兩個位元組的字元資料代表十六進位格式的數字。 例如，"01"會轉換成二進位 00000001 和"FF"會轉換成二進位 11111111。  
  
 驅動程式一律會將成對的十六進位數字轉換成個別的位元組，並忽略 null 結束的位元組。 因為這個緣故，如果字元字串的長度為奇數，最後一個位元組的字串 （不含 null 終止的位元組，如果有的話） 不會轉換。  
  
> [!NOTE]  
>  應用程式開發人員會建議您不要從字元 C 資料繫結至二進位的 SQL 資料類型。 此轉換通常是緩慢又沒有效率。
