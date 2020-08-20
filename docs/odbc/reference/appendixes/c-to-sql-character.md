---
description: C 到 SQL：字元
title: C 到 SQL：字元 |Microsoft Docs
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
ms.openlocfilehash: 0ab8f1c0471c6e079f792aa40119f13cb31ca9ed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500021"
---
# <a name="c-to-sql-character"></a>C 到 SQL：字元
字元 ODBC C 資料類型的識別碼如下：  
  
 SQL_C_CHAR  
  
 SQL_C_WCHAR  
  
 下表顯示可以轉換 C 字元資料的 ODBC SQL 資料類型。 如需資料表中的資料行和詞彙的說明，請參閱將 [資料從 C 轉換成 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
> [!NOTE]  
>  當字元 C 資料轉換成 Unicode SQL 資料時，Unicode 資料的長度必須是偶數。  
  
|SQL 類型識別碼|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|資料的位元組長度 <= 資料行長度。<br /><br /> 資料的位元組長度 > 資料行長度。|n/a<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|資料的字元長度 <= 資料行長度。<br /><br /> 資料的字元長度 > 資料行長度。|n/a<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT|未截斷的資料轉換<br /><br /> 以截斷小數數位 [e] 轉換的資料<br /><br /> 轉換資料會導致整個 (遺失，而不是小數) 位數 [e]<br /><br /> 資料值不是*數值常*值|n/a<br /><br /> 22001<br /><br /> 22001<br /><br /> 22018|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|資料在轉換數位的資料類型範圍內<br /><br /> 資料超出要轉換數位的資料類型範圍<br /><br /> 資料值不是*數值常*值|n/a<br /><br /> 22003<br /><br /> 22018|  
|SQL_BIT|資料為0或1<br /><br /> 資料大於0、小於2，且不等於1<br /><br /> 資料小於0或大於或等於2<br /><br /> 資料不是*數值常*值|n/a<br /><br /> 22001<br /><br /> 22003<br /><br /> 22018|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY| (位元組長度的資料) /2 <= 資料行位元組長度<br /><br />  (位元組長度的資料) /2 > 資料行位元組長度<br /><br /> 資料值不是十六進位值|n/a<br /><br /> 22001<br /><br /> 22018|  
|SQL_TYPE_DATE|資料值是有效的*ODBC 日期-常*值<br /><br /> 資料值是有效的 *ODBC 時間戳記-常*值;時間部分為零<br /><br /> 資料值是有效的 *ODBC 時間戳記-常*值;時間部分為非零 [a]<br /><br /> 資料值不是有效的*ODBC 日期-常*值或*odbc-timestamp-常*值|n/a<br /><br /> n/a<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIME|資料值是有效的*ODBC 時間常*值<br /><br /> 資料值是有效的 *ODBC 時間戳記-常*值;小數秒部分為零 [b]<br /><br /> 資料值是有效的 *ODBC 時間戳記-常*值;小數秒部分為非零值 [b]<br /><br /> 資料值不是有效的*ODBC 時間常*值或*odbc-timestamp-常*值|n/a<br /><br /> n/a<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIMESTAMP|資料值是有效的 *ODBC 時間戳記-常*值;小數秒數部分未截斷<br /><br /> 資料值是有效的 *ODBC 時間戳記-常*值;小數秒部分已截斷<br /><br /> 資料值是有效的 *ODBC 日期-常*值 [c]<br /><br /> 資料值是有效的 *ODBC 時間-常*值 [d]<br /><br /> 資料值不是有效的*odbc 日期-常*值、 *odbc 時間常*值或*odbc-timestamp-常*值|n/a<br /><br /> 22008<br /><br /> n/a<br /><br /> n/a<br /><br /> 22018|  
|所有 SQL 間隔類型|資料值是有效的 *間隔值*;不會發生截斷<br /><br /> 資料值是有效的 *間隔值*;其中一個欄位中的值會被截斷<br /><br /> 資料值不是有效的間隔常值|n/a<br /><br /> 22015<br /><br /> 22018|  
  
 [a] 時間戳記的時間部分會被截斷。  
  
 [b] 會忽略時間戳記的日期部分。  
  
 [c] 時間戳記的時間部分設為零。  
  
 [d] 時間戳記的日期部分會設定為目前的日期。  
  
 [e] 驅動程式/資料來源會有效等候直到收到整個字串為止 (即使字元資料是在嘗試執行轉換之前，透過呼叫 **SQLPutData**) 來傳送。  
  
 當字元 C 資料轉換成數值、日期、時間或時間戳記 SQL 資料時，會忽略開頭和尾端空白。  
  
 當字元 C 資料轉換成二進位 SQL 資料時，每兩個位元組的字元資料都會轉換成單一位元組， (8 位的二進位資料) 。 字元資料的每個位元組都代表十六進位格式的數位。 例如，"01" 會轉換成二進位00000001，並將 "FF" 轉換為二進位11111111。  
  
 驅動程式一律會將一組十六進位數位轉換成個別位元組，並忽略 null 終止位元組。 基於這個原因，如果字元字串的長度是奇數，則字串的最後一個位元組 (排除 null 終止位元組（如果沒有轉換任何) ）。  
  
> [!NOTE]  
>  應用程式開發人員不建議將字元 C 資料系結至二進位 SQL 資料類型。 這項轉換通常沒有效率且速度很慢。
