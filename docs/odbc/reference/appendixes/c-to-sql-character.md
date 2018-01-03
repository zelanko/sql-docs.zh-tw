---
title: "SQL 到 C： 字元 |Microsoft 文件"
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
- character data type [ODBC]
- data conversions from C to SQL types [ODBC], character
- converting data from c to SQL types [ODBC], character
ms.assetid: be66188a-ebdb-4c9e-af72-c379886766fa
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1496d6d5a6f130b7eea47ad11a47e763a7958e08
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="c-to-sql-character"></a>SQL 到 C： 字元
ODBC C 資料類型之字元的識別項是：  
  
 SQL_C_CHAR  
  
 SQL_C_WCHAR  
  
 下表顯示 ODBC SQL 資料類型可能會轉換 C 字元資料。 如需的資料行和資料表中的詞彙說明，請參閱[轉換資料從 C 到 SQL 資料型別](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
> [!NOTE]  
>  當 C 字元資料轉換成 Unicode SQL 資料時，Unicode 資料的長度必須是偶數。  
  
|SQL 類型識別碼|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|資料的位元組長度 < = 資料行長度。<br /><br /> 資料的位元組長度 > 資料行長度。|n/a<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|字元長度的資料 < = 資料行長度。<br /><br /> 字元資料的長度 > 資料行長度。|n/a<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT|資料轉換而不會截斷<br /><br /> 資料截斷的小數數字 [e] 的轉換<br /><br /> 轉換的資料會導致遺失 （而不是小數） 的整數位數 [e]<br /><br /> 資料值不是*數值常值*|n/a<br /><br /> 22001<br /><br /> 22001<br /><br /> 22018|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|資料是數字轉換的資料類型的範圍內<br /><br /> 資料超出範圍的數字轉換的資料類型<br /><br /> 資料值不是*數值常值*|n/a<br /><br /> 22003<br /><br /> 22018|  
|SQL_BIT|資料是 0 或 1<br /><br /> 資料是大於 0，小於 2，且不等於 1<br /><br /> 小於 0 或大於或等於 2，資料是<br /><br /> 資料不是*數值常值*|n/a<br /><br /> 22001<br /><br /> 22003<br /><br /> 22018|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|（資料的位元組長度） / 2 < = 資料行的位元組長度<br /><br /> （資料的位元組長度） / 2 > 資料行的位元組長度<br /><br /> 資料值不是十六進位值|n/a<br /><br /> 22001<br /><br /> 22018|  
|SQL_TYPE_DATE|資料值是一個有效*ODBC 日期常值*<br /><br /> 資料值是一個有效*ODBC 時間戳記值*; 時間部分為零<br /><br /> 資料值是一個有效*ODBC 時間戳記值*; 時間部分是為非零，[a]<br /><br /> 資料值不是有效*ODBC 日期常值*或*ODBC 時間戳記值*|n/a<br /><br /> n/a<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIME|資料值是一個有效*ODBC 時間常值*<br /><br /> 資料值是一個有效*ODBC 時間戳記值*; 小數秒數部分為零 [b]<br /><br /> 資料值是一個有效*ODBC 時間戳記值*; 小數秒數部分為非零，[b]<br /><br /> 資料值不是有效*ODBC 時間常值*或*ODBC 時間戳記值*|n/a<br /><br /> n/a<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIMESTAMP|資料值是一個有效*ODBC 時間戳記值*; 小數秒數部分不會被截斷<br /><br /> 資料值是一個有效*ODBC 時間戳記值*; 分數截斷的秒數部分<br /><br /> 資料值是一個有效*ODBC 日期常值*[c]<br /><br /> 資料值是一個有效*ODBC 時間常值*[d]<br /><br /> 資料值不是有效*ODBC 日期常值*， *ODBC 時間常值*，或*ODBC 時間戳記值*|n/a<br /><br /> 22008<br /><br /> n/a<br /><br /> n/a<br /><br /> 22018|  
|所有 SQL 間隔類型|資料值是一個有效*間隔值*; 沒有截斷<br /><br /> 資料值是一個有效*間隔值*; 中的其中一個欄位的值會被截斷<br /><br /> 資料值不是常值的有效間隔|n/a<br /><br /> 22015<br /><br /> 22018|  
  
 [a] 的時間戳記的時間部分會被截斷。  
  
 [會忽略時間戳記 b] 的日期部分。  
  
 [時間戳記 c] 的時間部分設為零。  
  
 [d] 上，日期部分的時間戳記設定為目前的日期。  
  
 [e] 的驅動程式/資料來源有效地等待已經收到整個字串直到 (即使字元資料片段以傳送呼叫**SQLPutData**) 之前嘗試執行轉換。  
  
 C 字元資料轉換為數值、 日期、 時間戳記 SQL 資料時，會忽略開頭和尾端空白。  
  
 當 C 字元資料轉換為二進位的 SQL 資料時，每兩個位元組的字元資料會轉換成二進位資料的單一位元組 （8 位元）。 字元資料的每個兩個位元組代表十六進位格式之數字。 例如，"01"會轉換成二進位 00000001 和"FF"會轉換成二進位 11111111。  
  
 驅動程式一律會將成對的十六進位數字轉換成個別的位元組，並忽略 null 結束位元組。 因為這個緣故，如果字元字串的長度為奇數，，最後一個位元組的字串 （不含的 null 結束位元組，如果有的話） 將不會轉換。  
  
> [!NOTE]  
>  應用程式開發人員都建議您不要從字元 C 資料繫結至二進位的 SQL 資料類型。 此轉換通常是緩慢又沒有效率。
