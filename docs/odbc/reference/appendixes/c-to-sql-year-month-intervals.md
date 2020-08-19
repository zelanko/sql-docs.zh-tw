---
description: C 到 SQL：年月間隔
title: C 到 SQL：年-月間隔 |Microsoft Docs
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
ms.openlocfilehash: ffd9a3f7f14ff6af93f15521738bebdbc63a8f58
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449020"
---
# <a name="c-to-sql-year-month-intervals"></a>C 到 SQL：年月間隔
年月間隔 ODBC C 資料類型的識別碼如下：  
  
 SQL_C_INTERVAL_MONTH SQL_C_INTERVAL_YEAR SQL_C_INTERVAL_YEAR_TO_MONTH  
  
 下表顯示的 ODBC SQL 資料類型，可轉換的年份間隔 C 資料。 如需資料表中的資料行和詞彙的說明，請參閱將 [資料從 C 轉換成 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 類型識別碼|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR [a]<br /><br /> SQL_VARCHAR [a]<br /><br /> SQL_LONGVARCHAR [a]|資料行位元組長度 >= 字元位元組長度<br /><br /> 資料行位元組長度 < 字元位元組長度 [a]<br /><br /> 資料值不是有效的間隔常值|n/a<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR [a]<br /><br /> SQL_WVARCHAR [a]<br /><br /> SQL_WLONGVARCHAR [a]|資料行字元長度 >= 字元的資料長度<br /><br /> 資料行字元長度 < 資料的字元長度 [a]<br /><br /> 資料值不是有效的間隔常值|n/a<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT [b]<br /><br /> SQL_SMALLINT [b]<br /><br /> SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b]<br /><br /> SQL_NUMERIC [b]<br /><br /> SQL_DECIMAL [b]|單一欄位間隔的轉換未產生整數的截斷<br /><br /> 轉換導致整個數位截斷|n/a<br /><br /> 22003|  
|SQL_INTERVAL_MONTH<br /><br /> SQL_INTERVAL_YEAR<br /><br /> SQL_INTERVAL_YEAR_TO_MONTH|已轉換資料值，但未截斷任何欄位<br /><br /> 轉換期間截斷了一或多個資料值欄位|n/a<br /><br /> 22015|  
  
 [a] 所有 C 間隔資料類型都可以轉換成字元資料類型。  
  
 [b] 如果間隔結構中的類型欄位使間隔是單一欄位 (SQL_YEAR 或 SQL_MONTH) ，則間隔 C 類型可以轉換成任何精確數值 (SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、SQL_BIGINT、SQL_DECIMAL 或 SQL_NUMERIC) 。  
  
 間隔 C 類型的預設轉換是對應的年月間隔 SQL 類型。  
  
 從 interval C 資料類型轉換資料時，驅動程式會忽略長度/指標值，並假設資料緩衝區的大小是 interval C 資料類型的大小。 長度/指標值會傳遞至**SQLPutData**中的*StrLen_or_Ind*引數，以及在**SQLBindParameter**中使用*StrLen_or_IndPtr*引數指定的緩衝區。 資料緩衝區會以**SQLPutData**中的*DataPtr*引數和**SQLBindParameter**中的*ParameterValuePtr*引數來指定。
