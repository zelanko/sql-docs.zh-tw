---
title: C 到 SQL:字元 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: acde0d2a79492607185d56d3082797c79a100fa2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292029"
---
# <a name="c-to-sql-character"></a>C 到 SQL：字元
字元 ODBC C 資料類型的識別碼為:  
  
 SQL_C_CHAR  
  
 SQL_C_WCHAR  
  
 下表顯示了可以轉換為 C 字元數據的 ODBC SQL 資料類型。 有關表中列與字語的說明,請參考[資料從 C 轉換為 SQL 資料型態](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
> [!NOTE]  
>  當字元 C 資料轉換為 Unicode SQL 資料時,Unicode 數據的長度必須為偶數。  
  
|SQL 類型識別碼|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|數據<位元組長度 = 列長度。<br /><br /> 數據位組長度>列長度。|n/a<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|數據<的字元長度 = 列長度。<br /><br /> >列长度的数据的字符长度。|n/a<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGERSQL_BIGINT|在不截斷的情況下轉換的資料<br /><br /> 使用小數數字截斷轉換的資料[e]<br /><br /> 資料轉換將導致整體(相對於小數)數位的丟失[e]<br /><br /> 資料值不是*數字文字*|n/a<br /><br /> 22001<br /><br /> 22001<br /><br /> 22018|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|資料在要轉換數字的資料型態<br /><br /> 資料超出要轉換數字的資料型態的範圍<br /><br /> 資料值不是*數字文字*|n/a<br /><br /> 22003<br /><br /> 22018|  
|SQL_BIT|資料為 0 或 1<br /><br /> 數據大於 0,小於 2,不等於 1<br /><br /> 資料小於 0 或大於或等於 2<br /><br /> 資料不是*數字文字*|n/a<br /><br /> 22001<br /><br /> 22003<br /><br /> 22018|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|(資料位元組長度) / 2 <= 列位元組長度<br /><br /> (資料位元組長度) / 2 >列字节长度<br /><br /> 資料值不是十六進位值|n/a<br /><br /> 22001<br /><br /> 22018|  
|SQL_TYPE_DATE|資料值是有效的*ODBC 日期文字*<br /><br /> 資料值是有效的*ODBC 時間戳文字*;時間部份為零<br /><br /> 資料值是有效的*ODBC 時間戳文字*;時間部分是非零[a]<br /><br /> 資料值不是有效的*ODBC-日期文字*或*ODBC 時間戳-文字*|n/a<br /><br /> n/a<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIME|資料值是有效的*ODBC 時間文字*<br /><br /> 資料值是有效的*ODBC 時間戳文字*;小數秒部分為零[b]<br /><br /> 資料值是有效的*ODBC 時間戳文字*;小數秒部分是非零[b]<br /><br /> 資料值不是有效的*ODBC-時間文字*或*ODBC 時間戳-文字*|n/a<br /><br /> n/a<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIMESTAMP|資料值是有效的*ODBC 時間戳文字*;分數秒部份未截斷<br /><br /> 資料值是有效的*ODBC 時間戳文字*;小數秒部分截斷<br /><br /> 資料值是有效的*ODBC-日期文字*[c]<br /><br /> 資料值是有效的*ODBC 時間文字*[d]<br /><br /> 資料值不是有效的*ODBC-日期文字**、ODBC 時間-文字*或*ODBC 時間戳-文字*|n/a<br /><br /> 22008<br /><br /> n/a<br /><br /> n/a<br /><br /> 22018|  
|所有 SQL 間隔型態|資料值是有效的*間隔值*;未發生截斷<br /><br /> 資料值是有效的*間隔值*;其中一個字段中的值被截斷<br /><br /> 資料值不是有效的間隔文字|n/a<br /><br /> 22015<br /><br /> 22018|  
  
 [a] 時間戳的時間部分被截斷。  
  
 [b] 時間戳的日期部分將被忽略。  
  
 [c] 時間戳的時間部分設置為零。  
  
 [d] 時間戳的日期部分設置為當前日期。  
  
 [e] 驅動程式/資料來源有效地等待整個字串已收到(即使字元數據通過呼叫**SQLPutData**分批發送),然後再嘗試執行轉換。  
  
 當字元 C 資料轉換為數位、日期、時間或時間戳 SQL 資料時,將忽略前導和尾隨空格。  
  
 當字元 C 數據轉換為二進位 SQL 資料時,字元數據的每兩個字節將轉換為二進位資料的單個字節(8 位)。 字元數據的每兩個字節以十六進位形式表示數位。 例如,"01"轉換為二進位0000001,"FF"轉換為二進制11111111。  
  
 驅動程序始終將十六進位數位對轉換為單個字節,並忽略 null 端接位元組。 因此,如果字串的長度為奇數,則不會轉換字串的最後一個字節(不包括 null 端接位元組(如果有)。  
  
> [!NOTE]  
>  禁止應用程式開發人員將字元 C 數據繫結到二進位 SQL 資料類型。 此轉換通常效率低下且速度緩慢。
