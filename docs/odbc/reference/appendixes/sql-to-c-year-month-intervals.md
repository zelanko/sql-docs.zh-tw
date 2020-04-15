---
title: SQL 到 C:年月間隔 |微軟文件
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], about converting
- data conversions from SQL to C types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
ms.assetid: 1233634b-8214-420f-b872-3b2630105ba4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba79a4d6165a43676634a6b79db56b88f5bcc234
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296388"
---
# <a name="sql-to-c-year-month-intervals"></a>SQL 到 C：年月間隔

年月間隔 ODBC SQL 資料類型的識別碼如下:

- SQL_INTERVAL_MONTH
- SQL_INTERVAL_YEAR
- SQL_INTERVAL_YEAR_TO_MONTH

下表顯示了可轉換為年月間隔 SQL 數據的 ODBC C 數據類型。 有關表中列與字語的說明,請參考[資料從 SQL 轉換為 C 資料型態](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  

|C 類型識別碼|測試|目標價值Ptr|StrLen_or_IndPtr|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_INTERVAL_MONTH[a]<br /><br /> SQL_C_INTERVAL_YEAR[a]<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH[a]|尾隨欄位部份未截斷<br /><br /> 尾隨欄位部份截斷<br /><br /> 目標的領先精度不足以儲存來自源的資料|資料<br /><br /> 截斷的資料<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT[b]<br /><br /> SQL_C_UTINYINT[b]<br /><br /> SQL_C_USHORT[b]<br /><br /> SQL_C_SHORT[b]<br /><br /> SQL_C_SLONG[b]<br /><br /> SQL_C_ULONG[b]<br /><br /> SQL_C_NUMERIC[b]<br /><br /> SQL_C_BIGINT[b]|間隔精度是單個字段,數據在不截斷的情況下被轉換<br /><br /> 間隔精度是單個字段,並截斷整個<br /><br /> 間隔精度不是單個字段|資料<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料型態大小<br /><br /> 以位元組為單位的資料長度<br /><br /> C 資料型態大小|n/a<br /><br /> 22003<br /><br /> 22015|  
|SQL_C_BINARY|資料<位元組長度 =*緩衝區長度*<br /><br /> >*緩衝區長度*的資料位元組長度|資料<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_CHAR|字元位元組長度<*緩衝區長度*<br /><br /> *緩衝區長度*<整数(與小數)位數<br /><br /> >=*緩衝區長度*的整個(與小數)數字數|資料<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料型態大小<br /><br /> C 資料型態大小<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|字元長度<*緩衝區長度*<br /><br /> *緩衝區長度*<整数(與小數)位數<br /><br /> >=*緩衝區長度*的整個(與小數)數字數|資料<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料型態大小<br /><br /> C 資料型態大小<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
  
 [a] 年月間隔 SQL 類型可以轉換為任何年月間隔 C 類型。  
  
 [b] 如果間隔精度是單個字段(YEAR 或 MONTH 之一),則可以將間隔 SQL 類型轉換為任何精確數值(SQL_C_STINYINT、SQL_C_UTINYINT、SQL_C_USHORT、SQL_C_SHORT、SQL_C_SLONG、SQL_C_ULONG或SQL_C_NUMERIC)。  

## <a name="default-conversions"></a>預設轉換

間隔 SQL 類型的預設轉換為相應的 C 間隔數據類型。 然後,應用程式綁定列或參數(或在ARD的適當記錄中設置SQL_DESC_DATA_PTR欄位),以指向初始化SQL_INTERVAL_STRUCT結構(或將指向SQL_INTERVAL_STRUCT結構的指標作為對**SQLGetData**調用中的*TargetValuePtr*參數)。
