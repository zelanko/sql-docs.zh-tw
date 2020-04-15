---
title: C 到 SQL:年月間隔 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
- data conversions from C to SQL types [ODBC], year-month intervals
ms.assetid: a0eb7b55-9db0-4375-9210-bddec4593880
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2ec7bfda0015883c8470dd453c7ae5de9bfd6cec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306609"
---
# <a name="c-to-sql-year-month-intervals"></a>C 到 SQL：年月間隔
年月間隔 ODBC C 資料類型的識別碼為:  
  
 SQL_C_INTERVAL_MONTHSQL_C_INTERVAL_YEARSQL_C_INTERVAL_YEAR_TO_MONTH  
  
 下表顯示了可轉換為年月間隔 C 數據的 ODBC SQL 資料類型。 有關表中列與字語的說明,請參考[資料從 C 轉換為 SQL 資料型態](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 類型識別碼|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR[a]<br /><br /> SQL_VARCHAR[a]<br /><br /> SQL_LONGVARCHAR[a]|列位元組長度>= 字元位長度<br /><br /> 列位元組長度<字元位長度 [a]<br /><br /> 資料值不是有效的間隔文字|n/a<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR[a]<br /><br /> SQL_WVARCHAR[a]<br /><br /> SQL_WLONGVARCHAR[a]|列字元長度>= 資料的字元長度<br /><br /> 列字元長度<字元長度的數據[a]<br /><br /> 資料值不是有效的間隔文字|n/a<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b]<br /><br /> SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b]<br /><br /> SQL_NUMERIC[b]<br /><br /> SQL_DECIMAL[b]|單欄位間隔轉換不會導致整個數字的截斷<br /><br /> 轉換導致整個數字的截斷|n/a<br /><br /> 22003|  
|SQL_INTERVAL_MONTH<br /><br /> SQL_INTERVAL_YEAR<br /><br /> SQL_INTERVAL_YEAR_TO_MONTH|資料值已轉換,無需截斷任何欄位<br /><br /> 轉換期間截斷一個或多個資料值欄位|n/a<br /><br /> 22015|  
  
 [a] 所有 C 間隔數據類型都可以轉換為字元數據類型。  
  
 [b] 如果間隔結構中的類型欄位使間隔為單個字段(SQL_YEAR 或SQL_MONTH),則可以將間隔 C 類型轉換為任何精確數值(SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、SQL_BIGINT、SQL_DECIMAL 或SQL_NUMERIC)。  
  
 間隔 C 類型的預設轉換為相應的年月間隔 SQL 類型。  
  
 當從間隔 C 資料類型轉換數據時,驅動程式忽略長度/ 指示器值,並假定數據緩衝區的大小是間隔 C 資料類型的大小。 長度/指標值在**SQLPutData**中的*StrLen_or_Ind*參數中傳遞,在**SQLBind 參數**中用*StrLen_or_IndPtr*參數指定的緩衝區中傳遞。 數據緩衝區使用**SQLPutData**中的*DataPtr*參數和**SQLBind 參數**中的*參數 ValuePtr*參數指定。
