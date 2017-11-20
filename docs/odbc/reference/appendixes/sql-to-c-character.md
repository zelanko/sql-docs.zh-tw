---
title: "SQL 到 c： 字元 |Microsoft 文件"
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
- converting data from SQL to C types [ODBC], character
- character data type [ODBC]
- data conversions from SQL to C types [ODBC], character
ms.assetid: 7fdb7f38-b64d-48f2-bcb4-1ca96b2bbdb6
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3ba39caca1a4ad37437f35918545ed54a5dd2266
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sql-to-c-character"></a>SQL 到 c： 字元
字元 ODBC SQL 資料類型的識別項是：  
  
 SQL_CHAR  
  
 SQL_VARCHAR  
  
 SQL_LONGVARCHAR  
  
 SQL_WCHAR  
  
 SQL_WVARCHAR  
  
 SQL_WLONGVARCHAR  
  
 下表顯示 ODBC C 資料類型可能會轉換字元 SQL 資料。 如需的資料行和資料表中的詞彙說明，請參閱[轉換資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|資料的位元組長度 < *Columnsize*<br /><br /> 資料的位元組長度 > = *Columnsize*|data<br /><br /> 截斷的資料|以位元組為單位的資料長度<br /><br /> 以位元組為單位的資料長度|n/a<br /><br /> 01004|  
|SQL_C_WCHAR|字元長度的資料 < *Columnsize*<br /><br /> 字元資料的長度 > = *Columnsize*|data<br /><br /> 截斷的資料|以字元為單位的資料長度<br /><br /> 以字元為單位的資料長度|n/a<br /><br /> 01004|  
|SQL_C_STINYINT SQL_C_UTINYINT SQL_C_TINYINT SQL_C_SBIGINT SQL_C_UBIGINT SQL_C_SSHORT SQL_C_USHORT SQL_C_SHORT SQL_C_SLONG SQL_C_ULONG SQL_C_LONG SQL_C_NUMERIC|資料轉換，而不會截斷 [b]<br /><br /> 資料截斷的小數數字 [a] 的轉換<br /><br /> 轉換的資料會導致遺失 （而不是小數） 的整數位數 [a]<br /><br /> 資料不是*數值常值*[b]。|data<br /><br /> 截斷的資料<br /><br /> 未定義<br /><br /> 未定義|C 資料類型的位元組數<br /><br /> C 資料類型的位元組數<br /><br /> 未定義<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_FLOAT SQL_C_DOUBLE|資料範圍內的數字轉換的資料類型是 [a]<br /><br /> 資料超出範圍的數字轉換的資料類型 [a]<br /><br /> 資料不是*數值常值*[b]。|data<br /><br /> 未定義<br /><br /> 未定義|C 資料類型的大小<br /><br /> 未定義<br /><br /> 未定義|n/a<br /><br /> 22003<br /><br /> 22018|  
_C_BIT|資料是 0 或 1<br /><br /> 資料是大於 0，小於 2，且不等於 1<br /><br /> 小於 0 或大於或等於 2，資料是<br /><br /> 資料不是*數值常值*|data<br /><br /> 截斷的資料<br /><br /> 未定義<br /><br /> 未定義|1 [b]<br /><br /> 1 [b]<br /><br /> 未定義<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BINARY|資料的位元組長度 < = *Columnsize*<br /><br /> 資料的位元組長度 > *Columnsize*|data<br /><br /> 截斷的資料|以位元組為單位的資料長度<br /><br /> 資料長度|n/a<br /><br /> 01004|  
|SQL_C_TYPE_DATE|資料值是一個有效*日期值*[a]<br /><br /> 資料值是一個有效*時間戳記值*; 時間部分為零 [a]<br /><br /> 資料值是一個有效*時間戳記值*; 時間部分是為非零，[a]、 [c]<br /><br /> 資料值不是有效*日期值*或*時間戳記值*[a]|data<br /><br /> data<br /><br /> 截斷的資料<br /><br /> 未定義|6 [b]<br /><br /> 6 [b]<br /><br /> 6 [b]<br /><br /> 未定義|n/a<br /><br /> n/a<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIME|資料值是一個有效*時間值，以及值為 0 的小數秒*[a]<br /><br /> 資料值是一個有效*時間戳記值或有效的時間值*; 小數秒數部分為零 [a]、 [d]<br /><br /> 資料值是一個有效*時間戳記值*; 小數秒數部分為非零，[a]、 [d] [e]<br /><br /> 資料值不是有效*時間值*或*時間戳記值*[a]|data<br /><br /> data<br /><br /> 截斷的資料<br /><br /> 未定義|6 [b]<br /><br /> 6 [b]<br /><br /> 6 [b]<br /><br /> 未定義|n/a<br /><br /> n/a<br /><br /> 01S07<br /><br /> 22018|  
_C_TYPE_TIMESTAMP|資料值是一個有效*時間戳記值或有效的時間值*; 小數秒數部分不會被截斷 [a]<br /><br /> 資料值是一個有效*時間戳記值或有效的時間值*; 小數秒數部分截斷 [a]<br /><br /> 資料值是一個有效*日期值*[a]<br /><br /> 資料值是一個有效*時間值*[a]<br /><br /> 資料值不是有效*日期值*，*時間值*，或*時間戳記值*[a]|data<br /><br /> 截斷的資料<br /><br /> 資料 [f]<br /><br /> 資料 [g]<br /><br /> 未定義|16 [b]<br /><br /> 16 [b]<br /><br /> 16 [b]<br /><br /> 16 [b]<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> n/a<br /><br /> n/a<br /><br /> 22018|  
|所有 C 間隔類型|資料值是一個有效*間隔值*; 無截斷<br /><br /> 資料值是一個有效*間隔值*; 截斷一或多個尾端欄位<br /><br /> 資料是有效的間隔時間。開頭欄位顯著的有效位數將會遺失<br /><br /> 資料值不是有效的間隔值|data<br /><br /> 截斷的資料<br /><br /> 未定義<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 以位元組為單位的資料長度<br /><br /> 未定義<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> 22015<br /><br /> 22018|  
  
 [a] 的值*Columnsize*會忽略這項轉換。 驅動程式假設大小 **TargetValuePtr*是 C 資料類型的大小。  
  
 [b] 這是對應的 C 資料類型的大小。  
  
 [c] 的時間部分*時間戳記值*會被截斷。  
  
 [d] 的日期部分*時間戳記值*會被忽略。  
  
 [時間戳記 e] 的小數秒數部分會被截斷。  
  
 [時間戳記結構 f] 時間欄位會設定為零。  
  
 [時間戳記結構的 g] 的日期欄位設定為目前的日期。  
  
 當字元 SQL 資料會轉換為數值時，會忽略日期、 時間、 時間戳記或間隔 C 資料，開頭和尾端空白。

