---
title: SQL 到 C 資料轉換範例 |微軟文件
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC], examples
- converting data from SQL to C types [ODBC], examples
ms.assetid: 0190c76c-7f9b-42f4-be9d-cef7284840fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96b10dd93c807aaa49a7e10e198f789fb47ccdeb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296648"
---
# <a name="sql-to-c-data-conversion-examples"></a>SQL 到 C 資料轉換範例

下表中所示的範例說明驅動程式如何將 SQL 資料轉換為 C 資料:  
  
|SQL 類型<br /><br /> 識別碼 (identifier)|SQL 資料<br /><br /> value|C 類型<br /><br /> 識別碼 (identifier)|Buffer<br /><br /> 長度|**目標價值Ptr*|SQLSTATE|  
|-----------------------------|------------------------|---------------------------|-----------------------|------------------------|--------------|  
|SQL_CHAR|abcdef|SQL_C_CHAR|7|abcdef\0[a]|n/a|  
|SQL_CHAR|abcdef|SQL_C_CHAR|6|abcde_0[a]|01004|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|8|1234.56[0]a|n/a|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|5|1234[0]a]|01004|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|4|----|22003|  
|SQL_DECIMAL|1234.56|SQL_C_FLOAT|忽略|1234.56|n/a|  
|SQL_DECIMAL|1234.56|SQL_C_SSHORT|忽略|1234|01S07|  
|SQL_DECIMAL|1234.56|SQL_C_STINYINT|忽略|----|22003|  
|SQL_DOUBLE|1.2345678|SQL_C_DOUBLE|忽略|1.2345678|n/a|  
|SQL_DOUBLE|1.2345678|SQL_C_FLOAT|忽略|1.234567|n/a|  
|SQL_DOUBLE|1.2345678|SQL_C_STINYINT|忽略|1|n/a|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_CHAR|11|1992-12-31[0]a|n/a|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_CHAR|10|-----|22003|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_TIMESTAMP|忽略|1992,12,31,0,0,0,0[b]|n/a|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|23|1992-12-31 23:45:55.12[0]|n/a|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|22|1992-12-31 23:45:55.1[0]|01004|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|18|----|22003|  
  
 [a] "\0"表示一個空終止位元組。 驅動程序始終為空終止SQL_C_CHAR數據。  
  
 [b] 此清單中的數位是存儲在TIMESTAMP_STRUCT結構欄位中的數位。
