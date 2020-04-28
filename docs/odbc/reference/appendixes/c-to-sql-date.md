---
title: C 到 SQL： Date |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date data type [ODBC]
- converting data from c to SQL types [ODBC], date
- data conversions from C to SQL types [ODBC], date
ms.assetid: bea087d3-911f-418b-b483-d2b5b334da19
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fa3df8aaee03472076b3241cb9bb60e2a307e28b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298846"
---
# <a name="c-to-sql-date"></a>C 到 SQL：日期
Date ODBC C 資料類型的識別碼為：  
  
 SQL_C_TYPE_DATE  
  
 下表顯示可以轉換 date C 資料的 ODBC SQL 資料類型。 如需資料表中的資料行和詞彙的說明，請參閱將[資料從 C 轉換成 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 類型識別碼|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|資料行位元組長度 >= 10<br /><br /> 資料行位元組長度 < 10<br /><br /> 資料值不是有效的日期|n/a<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|資料行字元長度 >= 10<br /><br /> 資料行字元長度 < 10<br /><br /> 資料值不是有效的日期|n/a<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|資料值是有效的日期<br /><br /> 資料值不是有效的日期|n/a<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|資料值是有效的日期 [a]<br /><br /> 資料值不是有效的日期|n/a<br /><br /> 22007|  
  
 [a] 時間戳記的時間部分設定為零。  
  
 如需 SQL_C_TYPE_DATE 結構中有效值的相關資訊，請參閱本附錄稍早的[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)。  
  
 當日期 C 資料轉換成字元 SQL 資料時，產生的字元資料會採用 "*yyyy*-*mm*-*dd*" 格式。  
  
 在轉換 date C 資料類型的資料時，驅動程式會忽略長度/指標值，並假設資料緩衝區的大小是 date C 資料類型的大小。 長度/指標值會傳入**SQLPutData**中的*StrLen_or_Ind*引數，以及在**SQLBindParameter**中使用*StrLen_or_IndPtr*引數指定的緩衝區。 資料緩衝區會使用**SQLPutData**中的*DataPtr*引數和**SQLBindParameter**中的*ParameterValuePtr*引數來指定。
