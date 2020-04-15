---
title: C 到 SQL:位 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], bit
- bit data type [ODBC]
- data conversions from C to SQL types [ODBC], bit
ms.assetid: 267c9fa9-599e-4ee6-b51b-0cae43f09183
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a96982573d83cf01947f82dc2014ee2c470931e3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292041"
---
# <a name="c-to-sql-bit"></a>C 到 SQL：位元
位元 ODBC C 資料類型的識別碼是:  
  
 SQL_C_BIT  
  
 下表顯示了可轉換為位 C 數據的 ODBC SQL 資料類型。 有關表中列與字語的說明,請參考[資料從 C 轉換為 SQL 資料型態](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 類型識別碼|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHARSQL_VARCHAR<br /><br /> SQL_LONGVARCHAR<br /><br /> SQL_WCHARSQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|None|n/a|  
|SQL_DECIMALSQL_NUMERIC<br /><br /> SQL_TINYINTSQL_SMALLINT<br /><br /> SQL_INTEGERSQL_BIGINT<br /><br /> SQL_REALSQL_FLOAT<br /><br /> SQL_DOUBLE|None|n/a|  
|SQL_BIT|None|n/a|  
  
 驅動程式在從位 C 資料類型轉換數據時忽略長度/ 指示器值,並假定數據緩衝區的大小是位 C 資料類型的大小。 長度/指標值在**SQLPutData**中的*StrLen_or_Ind*參數中傳遞,在**SQLBind 參數**中用*StrLen_or_IndPtr*參數指定的緩衝區中傳遞。 數據緩衝區使用**SQLPutData**中的*DataPtr*參數和**SQLBind 參數**中的*參數 ValuePtr*參數指定。
