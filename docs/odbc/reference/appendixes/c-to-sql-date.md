---
title: C 轉換為 SQL：Date | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8edb075be1bf64dad8f4ef18924a6396b7c64e80
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63294365"
---
# <a name="c-to-sql-date"></a>C 轉換為 SQL：Date
日期的 ODBC C 資料類型的識別項是：  
  
 SQL_C_TYPE_DATE  
  
 下表顯示 ODBC SQL 日期 C 資料可能會轉換成的資料類型。 如需資料行和資料表中的詞彙說明，請參閱 <<c0> [ 轉換將資料從 C 到 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 型別識別項|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|資料行的位元組長度 > = 10<br /><br /> 資料行的位元組長度 < 10<br /><br /> 資料值不是有效的日期|n/a<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|資料行的字元長度 > = 10<br /><br /> 資料行的字元長度 < 10<br /><br /> 資料值不是有效的日期|n/a<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|資料值是有效的日期<br /><br /> 資料值不是有效的日期|n/a<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|資料值是有效的日期 [a]<br /><br /> 資料值不是有效的日期|n/a<br /><br /> 22007|  
  
 [a] 時間戳記的時間部分設為零。  
  
 如需哪些值是有效 SQL_C_TYPE_DATE 結構中的資訊，請參閱[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)稍早在本附錄中。  
  
 當日期 C 資料轉換成字元 SQL 資料時，產生的字元資料是在 「*yyyy*-*mm*-*dd*」 格式。  
  
 驅動程式將資料轉換的日期 C 資料類型時，會忽略長度/指標值，並假設資料緩衝區的大小是 date C 資料類型的大小。 傳入的長度/指標值無效*Strlen_or_ind&lt*中的引數**SQLPutData**並使用指定的緩衝區中*StrLen_or_IndPtr*引數中**SQLBindParameter**。 使用指定的資料緩衝區*DataPtr*中的引數**SQLPutData**並*ParameterValuePtr*中的引數**SQLBindParameter**.
