---
title: C 到 SQL:數位 |微軟文件
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
ms.openlocfilehash: bbc0a994ef95f2deca29c8a4cbb06f3167b0433f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304729"
---
# <a name="c-to-sql-numeric"></a>C 到 SQL：數值
數位 ODBC C 資料類型的識別碼為:  
  
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
  
 下表顯示了數位 C 資料可轉換為的 ODBC SQL 資料類型。 有關表中列與字語的說明,請參考[資料從 C 轉換為 SQL 資料型態](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 類型識別碼|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|數字數<= 列位元組長度<br /><br /> >列字节长度的数字数|n/a<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|<= 列字元長度的字元<br /><br /> >列字符长度的字符数|n/a<br /><br /> 22001|  
|SQL_DECIMAL[b]<br /><br /> SQL_NUMERIC[b]<br /><br /> SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b]<br /><br /> SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b]|在不截斷或小數數字截斷的情況下轉換的資料<br /><br /> 使用完整數字的截斷轉換的資料|n/a<br /><br /> 22003|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|資料在要轉換數字的資料型態<br /><br /> 資料超出要轉換數字的資料型態的範圍|n/a<br /><br /> 22003|  
|SQL_BIT|資料為 0 或 1<br /><br /> 數據大於 0,小於 2,不等於 1<br /><br /> 資料小於 0 或大於或等於 2|n/a<br /><br /> 22001<br /><br /> 22003|  
|SQL_INTERVAL_YEAR[a]<br /><br /> SQL_INTERVAL_MONTH[a]<br /><br /> SQL_INTERVAL_DAY[a]<br /><br /> SQL_INTERVAL_HOUR[a]<br /><br /> SQL_INTERVAL_MINUTE[a]<br /><br /> SQL_INTERVAL_SECOND[a]|數據未截斷。<br /><br /> 數據被截斷。|n/a<br /><br /> 22015|  
  
 [a] 這些轉換僅支援精確數值數據類型(SQL_C_STINYINT、SQL_C_UTINYINT、SQL_C_SSHORT、SQL_C_USHORT、SQL_C_SLONG、SQL_C_ULONG或SQL_C_NUMERIC)。 對於近似數值數據類型(SQL_C_FLOAT或SQL_C_DOUBLE),不支援它們。 精確數位 C 資料類型不能轉換為間隔 SQL 類型,其間隔精度不是單個字段。  
  
 [b] 對於"n/a"情況,當出現小段截斷時,驅動程式可以選擇返回SQL_SUCCESS_WITH_INFO和 01S07。  
  
 當從數位 C 資料類型轉換數據時,驅動程式忽略長度/ 指示器值,並假定數據緩衝區的大小是數位 C 資料類型的大小。 長度/指標值在**SQLPutData**中的*StrLen_or_Ind*參數中傳遞,在**SQLBind 參數**中用*StrLen_or_IndPtr*參數指定的緩衝區中傳遞。 數據緩衝區使用**SQLPutData**中的*DataPtr*參數和**SQLBind 參數**中的*參數 ValuePtr*參數指定。
