---
title: SQL 轉換為 C：年月間隔 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01af57739f23db586991f8a54d14b90b47f15933
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63259583"
---
# <a name="sql-to-c-year-month-intervals"></a>SQL 轉換為 C：年月間隔

年月間隔 ODBC SQL 資料類型的識別碼，如下所示：

- SQL_INTERVAL_MONTH
- SQL_INTERVAL_YEAR
- SQL_INTERVAL_YEAR_TO_MONTH

下表顯示 ODBC C SQL 資料的間隔可能會轉換成的年度月份的資料類型。 如需資料行和資料表中的詞彙說明，請參閱 <<c0> [ 轉換將資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  

|C 類型識別碼|測試|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_INTERVAL_MONTH[a]<br /><br /> SQL_C_INTERVAL_YEAR[a]<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH[a]|不會被截斷尾端的欄位部分<br /><br /> 截斷尾端的欄位部分<br /><br /> 開頭有效位數不是目標的夠大，無法容納來自來源的資料|資料<br /><br /> 截斷的資料<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT[b]<br /><br /> SQL_C_UTINYINT[b]<br /><br /> SQL_C_USHORT[b]<br /><br /> SQL_C_SHORT[b]<br /><br /> SQL_C_SLONG[b]<br /><br /> SQL_C_ULONG[b]<br /><br /> SQL_C_NUMERIC[b]<br /><br /> SQL_C_BIGINT[b]|間隔精確度是單一欄位，而不會截斷轉換資料<br /><br /> 間隔精確度是單一欄位和整個截斷<br /><br /> 未單一欄位間隔有效位數。|資料<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料類型的大小<br /><br /> 以位元組為單位的資料長度<br /><br /> C 資料類型的大小|n/a<br /><br /> 22003<br /><br /> 22015|  
|SQL_C_BINARY|資料的位元組長度 < = *Columnsize*<br /><br /> 資料的位元組長度 > *Columnsize*|資料<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_CHAR|字元的位元組長度 < *Columnsize*<br /><br /> （相對於小數） 的整數位數 < *Columnsize*<br /><br /> 整體 （而不是小數） 數 > = *Columnsize*|資料<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料類型的大小<br /><br /> C 資料類型的大小<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|字元長度 < *Columnsize*<br /><br /> （相對於小數） 的整數位數 < *Columnsize*<br /><br /> 整體 （而不是小數） 數 > = *Columnsize*|資料<br /><br /> 截斷的資料<br /><br /> 未定義|C 資料類型的大小<br /><br /> C 資料類型的大小<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
  
 [a] 的年度月份間隔 SQL 型別被可轉換成任何年月間隔 C 類型。  
  
 [b] 如果間隔有效位數的單一欄位 （其中一個年份或月份），間隔 SQL 型別被可轉換成任何精確數值 （SQL_C_STINYINT、 SQL_C_UTINYINT、 SQL_C_USHORT、 SQL_C_SHORT、 SQL_C_SLONG、 SQL_C_ULONG、 或 SQL_C_NUMERIC）。  

## <a name="default-conversions"></a>預設轉換

預設間隔 SQL 型別轉換為對應的 C 間隔資料類型。 應用程式再繫結資料行或參數 （或設定 SQL_DESC_DATA_PTR 欄位 ARD 適當記錄中） 以指向初始化 SQL_INTERVAL_STRUCT 結構 (或將指標傳遞給SQL_INTERVAL_STRUCT結構*TargetValuePtr*呼叫中的引數**SQLGetData**)。
