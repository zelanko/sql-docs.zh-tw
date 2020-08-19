---
description: C 到 SQL：數值
title: C 到 SQL：數值 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], converting
- data conversions from C to SQL types [ODBC], numeric
- converting data from c to SQL types [ODBC], numeric
ms.assetid: af4095ff-06c3-4b04-83bf-19f9ee098dc2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 111d2bedf6b988255a569587fd766406b6b4176a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421512"
---
# <a name="c-to-sql-numeric"></a>C 到 SQL：數值
數值 ODBC C 資料類型的識別碼如下：  
  
 SQL_C_STINYINT  
  
 SQL_C_SLONG  
  
 SQL_C_UTINYINT  
  
 SQL_C_ULONG  
  
 SQL_C_TINYINT  
  
 SQL_C_LONG  
  
 SQL_C_SSHORT  
  
 SQL_C_FLOAT  
  
 SQL_C_USHORT  
  
 SQL_C_DOUBLE  
  
 SQL_C_SHORT  
  
 SQL_C_NUMERIC  
  
 SQL_C_SBIGINT  
  
 SQL_C_UBIGINT  
  
 下表顯示可轉換數值 C 資料的 ODBC SQL 資料類型。 如需資料表中的資料行和詞彙的說明，請參閱將 [資料從 C 轉換成 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 類型識別碼|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|位數 <= 資料行位元組長度<br /><br /> > 資料行位元組長度的位數|n/a<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|<= 資料行字元長度的字元數<br /><br /> 字元數 > 資料行字元長度|n/a<br /><br /> 22001|  
|SQL_DECIMAL [b]<br /><br /> SQL_NUMERIC [b]<br /><br /> SQL_TINYINT [b]<br /><br /> SQL_SMALLINT [b]<br /><br /> SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b]|未截斷或截斷小數數位的資料轉換<br /><br /> 使用整數位截斷轉換的資料|n/a<br /><br /> 22003|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|資料在轉換數位的資料類型範圍內<br /><br /> 資料超出要轉換數位的資料類型範圍|n/a<br /><br /> 22003|  
|SQL_BIT|資料為0或1<br /><br /> 資料大於0、小於2，且不等於1<br /><br /> 資料小於0或大於或等於2|n/a<br /><br /> 22001<br /><br /> 22003|  
|SQL_INTERVAL_YEAR [a]<br /><br /> SQL_INTERVAL_MONTH [a]<br /><br /> SQL_INTERVAL_DAY [a]<br /><br /> SQL_INTERVAL_HOUR [a]<br /><br /> SQL_INTERVAL_MINUTE [a]<br /><br /> SQL_INTERVAL_SECOND [a]|未截斷的資料。<br /><br /> 資料已截斷。|n/a<br /><br /> 22015|  
  
 [a] 只有精確數值資料類型支援這些轉換 (SQL_C_STINYINT、SQL_C_UTINYINT、SQL_C_SSHORT、SQL_C_USHORT、SQL_C_SLONG、SQL_C_ULONG 或 SQL_C_NUMERIC) 。  (SQL_C_FLOAT 或 SQL_C_DOUBLE) 的近似數值資料類型不支援它們。 精確數值 C 資料類型無法轉換成間隔 SQL 類型，其間隔精確度不是單一欄位。  
  
 [b] 對於 "n/a" 案例，驅動程式可能會在有小數截斷時，選擇性地傳回 SQL_SUCCESS_WITH_INFO 和01S07。  
  
 從數值 C 資料類型轉換資料時，驅動程式會忽略長度/指標值，並假設資料緩衝區的大小是數位 C 資料類型的大小。 長度/指標值會傳遞至**SQLPutData**中的*StrLen_or_Ind*引數，以及在**SQLBindParameter**中使用*StrLen_or_IndPtr*引數指定的緩衝區。 資料緩衝區會以**SQLPutData**中的*DataPtr*引數和**SQLBindParameter**中的*ParameterValuePtr*引數來指定。
