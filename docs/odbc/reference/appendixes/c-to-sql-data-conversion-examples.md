---
title: "SQL 資料轉換範例的 C |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from c to SQL types [ODBC], examples
- data conversions from C to SQL types [ODBC], examples
ms.assetid: 9f390afc-d8b8-4286-b559-98b3b8781f3d
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 46c1a95015858fbec4ff1e1b5f10bb9b409c9482
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="c-to-sql-data-conversion-examples"></a>SQL 資料轉換範例 C
下列範例說明如何驅動程式將 C 資料轉換成 SQL 資料：  
  
|C 類型識別碼|C 資料值|SQL 類型<br /><br /> 識別碼 (identifier)|資料行<br /><br /> 長度|SQL 資料<br /><br /> value|SQLSTATE|  
|-----------------------|------------------|-----------------------------|-----------------------|------------------------|--------------|  
|SQL_C_CHAR|abcdef\0 [a]|SQL_CHAR|6|abcdef|n/a|  
|SQL_C_CHAR|abcdef\0 [a]|SQL_CHAR|5|abcde|22001|  
|SQL_C_CHAR|1234.56\0 [a]|SQL_DECIMAL|8 [b]|1234.56|n/a|  
|SQL_C_CHAR|1234.56\0 [a]|SQL_DECIMAL|7 [b]|1234.5|22001|  
|SQL_C_CHAR|1234.56\0 [a]|SQL_DECIMAL|4|----|22003|  
|SQL_C_FLOAT|1234.56|SQL_FLOAT|n/a|1234.56|n/a|  
|SQL_C_FLOAT|1234.56|SQL_INTEGER|n/a|1234|22001|  
|SQL_C_FLOAT|1234.56|SQL_TINYINT|n/a|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31 [c]|SQL_CHAR|10|1992-12-31|n/a|  
|SQL_C_TYPE_DATE|1992,12,31 [c]|SQL_CHAR|9|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31 [c]|SQL_TIMESTAMP|n/a|1992-12-31 00:00:00.0|n/a|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31、 23,45,55、 120000000 [d]|SQL_CHAR|22|1992-12-31 23:45:55.12|n/a|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31、 23,45,55、 120000000 [d]|SQL_CHAR|21|1992-12-31 23:45:55.1|22001|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31、 23,45,55、 120000000 [d]|SQL_CHAR|18|----|22003|  
  
 [a]"\0"代表 null 結束位元組。 只有資料的長度是 sql_nts; 需要的 null 終止的位元組。  
  
 [b] 中除了為位元組的數字，一個位元組是必要的符號，另一個位元組需要做為小數點。  
  
 [這份清單中的 c] 的數字為 SQL_DATE_STRUCT 結構的欄位中儲存的數字。  
  
 [這份清單中 a] 的數字為 SQL_TIMESTAMP_STRUCT 結構的欄位中儲存的數字。

