---
title: C 到 SQL:日期 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298846"
---
# <a name="c-to-sql-date"></a>C 到 SQL：日期
ODBC C 資料類型的日期識別碼為:  
  
 SQL_C_TYPE_DATE  
  
 下表顯示了可轉換為 C 資料的 ODBC SQL 資料類型。 有關表中列與字語的說明,請參考[資料從 C 轉換為 SQL 資料型態](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 類型識別碼|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|列位元組長度>= 10<br /><br /> 列位元組長度< 10<br /><br /> 資料值不是有效日期|n/a<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|列字元長度>= 10<br /><br /> 列字元長度< 10<br /><br /> 資料值不是有效日期|n/a<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|資料值是合法的日期<br /><br /> 資料值不是有效日期|n/a<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|資料值是有效的日期[a]<br /><br /> 資料值不是有效日期|n/a<br /><br /> 22007|  
  
 [a] 時間戳的時間部分設置為零。  
  
 有關哪些值在SQL_C_TYPE_DATE結構中有效的資訊,請參閱本附錄前面介紹[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)。  
  
 當日期 C 資料轉換為字元 SQL 資料時,生成的字元數據採用 *「yyyy*-*mm*-*dd」* 格式。  
  
 驅動程式在從日期 C 資料類型轉換數據時忽略長度/指示器值,並假定數據緩衝區的大小是日期 C 數據類型的大小。 長度/指標值在**SQLPutData**中的*StrLen_or_Ind*參數中傳遞,在**SQLBind 參數**中用*StrLen_or_IndPtr*參數指定的緩衝區中傳遞。 數據緩衝區使用**SQLPutData**中的*DataPtr*參數和**SQLBind 參數**中的*參數 ValuePtr*參數指定。
