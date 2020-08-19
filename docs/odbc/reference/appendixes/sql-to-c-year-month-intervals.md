---
description: SQL 到 C：年月間隔
title: SQL 到 C：年間間隔 |Microsoft Docs
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
ms.openlocfilehash: 66134ca1dcd82fec5213f01ef33a1b5f050e8a8b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429530"
---
# <a name="sql-to-c-year-month-intervals"></a>SQL 到 C：年月間隔

年月間隔 ODBC SQL 資料類型的識別碼如下：

- SQL_INTERVAL_MONTH
- SQL_INTERVAL_YEAR
- SQL_INTERVAL_YEAR_TO_MONTH

下表顯示可轉換之年中的 SQL 資料類型的 ODBC C 資料類型。 如需資料表中的資料行和詞彙的說明，請參閱將 [資料從 SQL 轉換成 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  

|C 類型識別碼|測試|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_INTERVAL_MONTH [a]<br /><br /> SQL_C_INTERVAL_YEAR [a]<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH [a]|尾端欄位部分未截斷<br /><br /> 尾端欄位部分已截斷<br /><br /> 目標的前置精確度不夠大，無法保存來源的資料|資料<br /><br /> 截斷的資料<br /><br /> 未定義|資料的長度（以位元組為單位）<br /><br /> 資料的長度（以位元組為單位）<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT [b]<br /><br /> SQL_C_UTINYINT [b]<br /><br /> SQL_C_USHORT [b]<br /><br /> SQL_C_SHORT [b]<br /><br /> SQL_C_SLONG [b]<br /><br /> SQL_C_ULONG [b]<br /><br /> SQL_C_NUMERIC [b]<br /><br /> SQL_C_BIGINT [b]|間隔精確度是單一欄位，而且資料已轉換而不截斷<br /><br /> 間隔精確度是單一欄位，而且全部截斷<br /><br /> 間隔精確度不是單一欄位|資料<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料類型的大小<br /><br /> 資料的長度（以位元組為單位）<br /><br /> C 資料類型的大小|n/a<br /><br /> 22003<br /><br /> 22015|  
|SQL_C_BINARY|資料 <的位元組長度 = *BufferLength*<br /><br /> 資料 > *BufferLength*的位元組長度|資料<br /><br /> 未定義|資料的長度（以位元組為單位）<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_CHAR|字元位元組長度 < *BufferLength*<br /><br /> 相對於小數) 位數 < *BufferLength*的整體 (數目<br /><br /> 整個 (的數目，而不是小數) 位數 >= *BufferLength*|資料<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料類型的大小<br /><br /> C 資料類型的大小<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|字元長度 < *BufferLength*<br /><br /> 相對於小數) 位數 < *BufferLength*的整體 (數目<br /><br /> 整個 (的數目，而不是小數) 位數 >= *BufferLength*|資料<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料類型的大小<br /><br /> C 資料類型的大小<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
  
 [a] 每月的間隔 SQL 類型可以轉換成任何年份的間隔 C 類型。  
  
 [b] 如果間隔精確度是 (YEAR 或 MONTH) 之一的單一欄位，則可以將間隔 SQL 類型轉換成任何精確的數值 (SQL_C_STINYINT、SQL_C_UTINYINT、SQL_C_USHORT、SQL_C_SHORT、SQL_C_SLONG、SQL_C_ULONG 或 SQL_C_NUMERIC) 。  

## <a name="default-conversions"></a>預設轉換

間隔 SQL 類型的預設轉換為對應的 C 間隔資料類型。 然後，應用程式會將資料行或參數系結 (，或將適當 ARD) 記錄中的 SQL_DESC_DATA_PTR 欄位設定為指向初始化的 SQL_INTERVAL_STRUCT 結構 (或傳遞 SQL_ INTERVAL_STRUCT 結構的指標做為**SQLGetData**) 呼叫中的*TargetValuePtr*引數。
