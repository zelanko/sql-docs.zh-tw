---
title: SQL 到 C： 每隔年-月 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- converting data from c to SQL types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
- data conversions from C to SQL types [ODBC], year-month intervals
ms.assetid: a0eb7b55-9db0-4375-9210-bddec4593880
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 00546f6f3809e385297be0c8117cffa7a4de9dbc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="c-to-sql-year-month-intervals"></a>SQL 到 C： 年度月份間隔
年-月間隔 ODBC C 資料類型的識別項是：  
  
 SQL_C_INTERVAL_MONTH SQL_C_INTERVAL_YEAR SQL_C_INTERVAL_YEAR_TO_MONTH  
  
 下表顯示 ODBC SQL 間隔 C 資料可能會轉換成的年度月份的資料類型。 如需的資料行和資料表中的詞彙說明，請參閱[轉換資料從 C 到 SQL 資料型別](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 類型識別碼|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR [a]<br /><br /> SQL_VARCHAR，[a]<br /><br /> SQL_LONGVARCHAR [a]|資料行的位元組長度 > = 字元位元組長度<br /><br /> 資料行的位元組長度 < 字元位元組長度 [a]<br /><br /> 資料值不是常值的有效間隔|n/a<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR [a]<br /><br /> SQL_WVARCHAR [a]<br /><br /> SQL_WLONGVARCHAR [a]|資料行的字元長度 > = 字元長度的資料<br /><br /> 資料行的字元長度 < 字元長度的資料，[a]<br /><br /> 資料值不是常值的有效間隔|n/a<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT [b]<br /><br /> SQL_SMALLINT [b]<br /><br /> SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b]<br /><br /> SQL_NUMERIC [b]<br /><br /> SQL_DECIMAL [b]|將單一欄位間隔的轉換不會造成整個位數截斷<br /><br /> 轉換導致截斷整數的數字|n/a<br /><br /> 22003|  
|SQL_INTERVAL_MONTH<br /><br /> SQL_INTERVAL_YEAR<br /><br /> SQL_INTERVAL_YEAR_TO_MONTH|已轉換資料值，而不會截斷的任何欄位<br /><br /> 在轉換期間都不截斷一或多個欄位的資料值|n/a<br /><br /> 22015|  
  
 [a] 的所有 C 間隔資料類型可以轉換成字元資料類型。  
  
 [b] 若間隔結構中的 [類型] 欄位的間隔是 （SQL_YEAR 或 SQL_MONTH） 的單一欄位，可以為任何實際的數值 （SQL_TINYINT、 SQL_SMALLINT、 SQL_INTEGER、 SQL_BIGINT、 SQL_DECIMAL 或 SQL_NUMERIC） 轉換 C 間隔類型。  
  
 預設間隔 C 類型轉換為對應的年度月份間隔 SQL 型別。  
  
 驅動程式將資料轉換從間隔 C 資料類型時，會忽略長度/指標值，並假設資料緩衝區的大小是間隔 C 資料類型的大小。 長度/指標值傳遞*StrLen_or_Ind*引數中的**SQLPutData**並使用指定的緩衝區中*StrLen_or_IndPtr*引數中**SQLBindParameter**。 使用指定的資料緩衝區*DataPtr*引數中的**SQLPutData**和*ParameterValuePtr*引數中的**SQLBindParameter**.
