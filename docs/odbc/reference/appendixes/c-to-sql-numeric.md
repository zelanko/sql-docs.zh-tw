---
title: C 轉換為 SQL：Numeric | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 816394bb8469148504c1b2b416e77fec814bef8f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63191743"
---
# <a name="c-to-sql-numeric"></a>C 轉換為 SQL：Numeric
針對數值的 ODBC C 資料類型的識別項是：  
  
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
  
 下表顯示 ODBC SQL 資料類型可能會轉換數字的 C 資料。 如需資料行和資料表中的詞彙說明，請參閱 <<c0> [ 轉換將資料從 C 到 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 型別識別項|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|數字數目 < = 資料行的位元組長度<br /><br /> 數字 > 資料行的位元組長度|n/a<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|字元數目 < = 資料行的字元長度<br /><br /> 字元數 > 資料行的字元長度|n/a<br /><br /> 22001|  
|SQL_DECIMAL[b]<br /><br /> SQL_NUMERIC[b]<br /><br /> SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b]<br /><br /> SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b]|資料轉換而不會截斷或截斷的小數位數<br /><br /> 轉換後的整個的位數截斷的資料|n/a<br /><br /> 22003|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|資料是數值轉換的資料類型的範圍內<br /><br /> 資料超出範圍的數值轉換的資料類型|n/a<br /><br /> 22003|  
|SQL_BIT|資料是 0 或 1<br /><br /> 資料是大於 0，小於 2，且不等於 1<br /><br /> 小於 0 或大於或等於 2，資料是|n/a<br /><br /> 22001<br /><br /> 22003|  
|SQL_INTERVAL_YEAR[a]<br /><br /> SQL_INTERVAL_MONTH[a]<br /><br /> SQL_INTERVAL_DAY[a]<br /><br /> SQL_INTERVAL_HOUR[a]<br /><br /> SQL_INTERVAL_MINUTE[a]<br /><br /> SQL_INTERVAL_SECOND[a]|不會被截斷的資料。<br /><br /> 資料被截斷。|n/a<br /><br /> 22015|  
  
 [a] 的精確數值資料類型 （SQL_C_STINYINT、 SQL_C_UTINYINT、 SQL_C_SSHORT、 SQL_C_USHORT、 SQL_C_SLONG、 SQL_C_ULONG、 或 SQL_C_NUMERIC） 才支援這些轉換。 它們不支援 （SQL_C_FLOAT 或 SQL_C_DOUBLE） 的近似數值資料類型。 精確數值的 C 資料類型無法轉換成 SQL 類型，其間隔有效位數不是單一欄位間隔。  
  
 [b] 的 [不適用] 案例中，驅動程式可以選擇性地傳回 SQL_SUCCESS_WITH_INFO 而且 01S07 分數截斷時。  
  
 驅動程式將資料轉換的數字的 C 資料類型時，會忽略長度/指標值，並假設資料緩衝區的大小是數字的 C 資料類型的大小。 傳入的長度/指標值無效*Strlen_or_ind&lt*中的引數**SQLPutData**並使用指定的緩衝區中*StrLen_or_IndPtr*引數中**SQLBindParameter**。 使用指定的資料緩衝區*DataPtr*中的引數**SQLPutData**並*ParameterValuePtr*中的引數**SQLBindParameter**.
