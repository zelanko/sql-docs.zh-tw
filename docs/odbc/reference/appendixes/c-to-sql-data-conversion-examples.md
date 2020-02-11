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
ms.openlocfilehash: e475abb699c7fa7240ca6eb39b1b32f1730d33c6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125743"
---
# <a name="c-to-sql-data-conversion-examples"></a>C 到 SQL 資料轉換範例
下列範例說明驅動程式如何將 C 資料轉換成 SQL 資料：  
  
|C 類型識別碼|C 資料值|SQL 類型<br /><br /> 識別碼 (identifier)|資料行<br /><br /> length|SQL 資料<br /><br /> value|SQLSTATE|  
|-----------------------|------------------|-----------------------------|-----------------------|------------------------|--------------|  
|SQL_C_CHAR|abcdef\0 [a]|SQL_CHAR|6|abcdef|n/a|  
|SQL_C_CHAR|abcdef\0 [a]|SQL_CHAR|5|abcde|22001|  
|SQL_C_CHAR|1234.56 \ 0 [a]|SQL_DECIMAL|8 [b]|1234.56|n/a|  
|SQL_C_CHAR|1234.56 \ 0 [a]|SQL_DECIMAL|7 [b]|1234.5|22001|  
|SQL_C_CHAR|1234.56 \ 0 [a]|SQL_DECIMAL|4|----|22003|  
|SQL_C_FLOAT|1234.56|SQL_FLOAT|n/a|1234.56|n/a|  
|SQL_C_FLOAT|1234.56|SQL_INTEGER|n/a|1234|22001|  
|SQL_C_FLOAT|1234.56|SQL_TINYINT|n/a|----|22003|  
|SQL_C_TYPE_DATE|1992、12、31 [c]|SQL_CHAR|10|1992-12-31|n/a|  
|SQL_C_TYPE_DATE|1992、12、31 [c]|SQL_CHAR|9|----|22003|  
|SQL_C_TYPE_DATE|1992、12、31 [c]|SQL_TIMESTAMP|n/a|1992-12-31 00：00：00。0|n/a|  
|SQL_C_TYPE_TIMESTAMP|1992，12，31，23，45，55，120000000 [d]|SQL_CHAR|22|1992-12-31 23：45：55.12|n/a|  
|SQL_C_TYPE_TIMESTAMP|1992，12，31，23，45，55，120000000 [d]|SQL_CHAR|21|1992-12-31 23：45：55。1|22001|  
|SQL_C_TYPE_TIMESTAMP|1992，12，31，23，45，55，120000000 [d]|SQL_CHAR|18|----|22003|  
  
 [a] "\ 0" 代表 null 終止位元組。 只有在 SQL_NTS 資料長度時，才需要 null 終止位元組。  
  
 [b] 除了數位的位元組之外，正負號需要一個位元組，而小數點需要另一個位元組。  
  
 [c] 這份清單中的數位是儲存在 SQL_DATE_STRUCT 結構之欄位中的數位。  
  
 [d] 這份清單中的數位是儲存在 SQL_TIMESTAMP_STRUCT 結構之欄位中的數位。
