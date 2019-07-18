---
title: C 轉換為 SQL：年月間隔 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3db8d61bacefa8588db4c0081c6be591d7ffdacf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019280"
---
# <a name="c-to-sql-year-month-intervals"></a>C 轉換為 SQL：年月間隔
年月間隔 ODBC C 資料類型的識別項是：  
  
 SQL_C_INTERVAL_MONTH SQL_C_INTERVAL_YEAR SQL_C_INTERVAL_YEAR_TO_MONTH  
  
 下表顯示 ODBC SQL 資料 C 間隔可能會轉換成的年度月份的資料類型。 如需資料行和資料表中的詞彙說明，請參閱 <<c0> [ 轉換將資料從 C 到 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 型別識別項|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR[a]<br /><br /> SQL_VARCHAR[a]<br /><br /> SQL_LONGVARCHAR[a]|資料行的位元組長度 > = 字元位元組長度<br /><br /> 資料行的位元組長度 < 字元位元組長度 [a]<br /><br /> 資料值不是常值的有效間隔|n/a<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR[a]<br /><br /> SQL_WVARCHAR[a]<br /><br /> SQL_WLONGVARCHAR[a]|資料行的字元長度 > = 字元長度的資料<br /><br /> 資料行的字元長度 < 字元長度的資料，[a]<br /><br /> 資料值不是常值的有效間隔|n/a<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b]<br /><br /> SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b]<br /><br /> SQL_NUMERIC[b]<br /><br /> SQL_DECIMAL[b]|將單一欄位間隔轉換不會造成整個的位數截斷<br /><br /> 轉換導致截斷的整數|n/a<br /><br /> 22003|  
|SQL_INTERVAL_MONTH<br /><br /> SQL_INTERVAL_YEAR<br /><br /> SQL_INTERVAL_YEAR_TO_MONTH|已轉換資料值，而不會截斷的任何欄位<br /><br /> 資料值的一個或多個欄位已在轉換期間截斷|n/a<br /><br /> 22015|  
  
 [a] 的所有 C 間隔資料類型可以轉換成字元資料類型。  
  
 [b] 如果間隔是 （SQL_YEAR 或 SQL_MONTH） 的單一欄位間隔結構中的 [類型] 欄位，C 間隔類型可轉換成任何精確數值 （SQL_TINYINT、 SQL_SMALLINT、 SQL_INTEGER、 SQL_BIGINT、 SQL_DECIMAL，還是 SQL_NUMERIC）。  
  
 預設間隔 C 類型轉換為相對應的年度月份間隔 SQL 型別。  
  
 驅動程式將資料從間隔 C 資料類型轉換時，會忽略長度/指標值，並假設資料緩衝區的大小是間隔 C 資料類型的大小。 傳入的長度/指標值無效*Strlen_or_ind&lt*中的引數**SQLPutData**並使用指定的緩衝區中*StrLen_or_IndPtr*引數中**SQLBindParameter**。 使用指定的資料緩衝區*DataPtr*中的引數**SQLPutData**並*ParameterValuePtr*中的引數**SQLBindParameter**.
