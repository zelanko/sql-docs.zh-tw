---
title: SQL 到 C： 日期 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- date data type [ODBC]
- converting data from c to SQL types [ODBC], date
- data conversions from C to SQL types [ODBC], date
ms.assetid: bea087d3-911f-418b-b483-d2b5b334da19
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 63e28a29258b012f246be83123360a52a90e68ea
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="c-to-sql-date"></a>SQL 到 C： 日期
日期 ODBC C 資料類型的識別項是：  
  
 SQL_C_TYPE_DATE  
  
 下表顯示 ODBC SQL 資料類型可能會轉換日期 C 資料。 如需的資料行和資料表中的詞彙說明，請參閱[轉換資料從 C 到 SQL 資料型別](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 類型識別碼|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|資料行的位元組長度 > = 10<br /><br /> 資料行長度的位元組數 < 10<br /><br /> 資料值不是有效的日期|n/a<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|資料行的字元長度 > = 10<br /><br /> 資料行的字元長度 < 10<br /><br /> 資料值不是有效的日期|n/a<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|資料值為有效的日期<br /><br /> 資料值不是有效的日期|n/a<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|資料值為有效的日期 [a]<br /><br /> 資料值不是有效的日期|n/a<br /><br /> 22007|  
  
 [a] 的時間戳記的時間部分設為零。  
  
 如需有效值 SQL_C_TYPE_DATE 結構中的資訊，請參閱[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)稍早在本附錄中。  
  
 當日期 C 資料轉換成字元的 SQL 資料時，產生的字元資料就會處於 「*yyyy*-*公釐*-*dd*」 格式。  
  
 驅動程式會忽略日期 C 資料類型轉換資料的長度/指標值，並假設資料緩衝區的大小是日期 C 資料類型的大小。 長度/指標值傳遞*StrLen_or_Ind*引數中的**SQLPutData**並使用指定的緩衝區中*StrLen_or_IndPtr*引數中**SQLBindParameter**。 使用指定的資料緩衝區*DataPtr*引數中的**SQLPutData**和*ParameterValuePtr*引數中的**SQLBindParameter**.
