---
title: C 到 SQL 資料轉換範例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], examples
- data conversions from C to SQL types [ODBC], examples
ms.assetid: 9f390afc-d8b8-4286-b559-98b3b8781f3d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 40cd9973bfdce68b1ccbe63edd8c875519dbd22b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63201587"
---
# <a name="c-to-sql-data-conversion-examples"></a>C 到 SQL 資料轉換範例
下列範例說明如何驅動程式將 C 資料轉換為 SQL 資料：  
  
|C 類型識別碼|C 資料值|SQL 類型<br /><br /> 識別碼 (identifier)|「資料行」<br /><br /> 長度|SQL 資料<br /><br /> value|SQLSTATE|  
|-----------------------|------------------|-----------------------------|-----------------------|------------------------|--------------|  
|SQL_C_CHAR|abcdef\0[a]|SQL_CHAR|6|abcdef|n/a|  
|SQL_C_CHAR|abcdef\0[a]|SQL_CHAR|5|abcde|22001|  
|SQL_C_CHAR|1234.56\0[a]|SQL_DECIMAL|8[b]|1234.56|n/a|  
|SQL_C_CHAR|1234.56\0[a]|SQL_DECIMAL|7[b]|1234.5|22001|  
|SQL_C_CHAR|1234.56\0[a]|SQL_DECIMAL|4|----|22003|  
|SQL_C_FLOAT|1234.56|SQL_FLOAT|n/a|1234.56|n/a|  
|SQL_C_FLOAT|1234.56|SQL_INTEGER|n/a|1234|22001|  
|SQL_C_FLOAT|1234.56|SQL_TINYINT|n/a|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31 [c]|SQL_CHAR|10|1992-12-31|n/a|  
|SQL_C_TYPE_DATE|1992,12,31 [c]|SQL_CHAR|9|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31 [c]|SQL_TIMESTAMP|n/a|1992-12-31 00:00:00.0|n/a|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31、 23,45,55 120000000 [d]|SQL_CHAR|22|1992-12-31 23:45:55.12|n/a|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31、 23,45,55 120000000 [d]|SQL_CHAR|21|1992-12-31 23:45:55.1|22001|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31、 23,45,55 120000000 [d]|SQL_CHAR|18|----|22003|  
  
 [a]"\0 」 代表終止 null 位元組。 只有當資料的長度是 sql_nts; 時，才需要的 null 終止的位元組。  
  
 [b] 中除了要位元組數字，一個位元組則需要為號，另一個位元組是需要做為小數點。  
  
 [這份清單中的 c] 的數字是儲存在 SQL_DATE_STRUCT 結構的欄位中的數字。  
  
 [這份清單中的 d] 的數字是儲存在 SQL_TIMESTAMP_STRUCT 結構的欄位中的數字。
