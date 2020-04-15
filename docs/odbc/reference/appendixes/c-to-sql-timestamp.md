---
title: C 到 SQL:時間戳 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from C to SQL types [ODBC], timestamp
- timestamp data type [ODBC]
- converting data from c to SQL types [ODBC], timestamp
ms.assetid: 0e08bfff-68f9-4648-9558-09b57fea08ad
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3102e5043527a1aa9463980c9dd546839cb92f37
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283748"
---
# <a name="c-to-sql-timestamp"></a>C 到 SQL：時間戳記
時間戳 ODBC C 資料類型的識別碼是:  
  
 SQL_C_TYPE_TIMESTAMP  
  
 下表顯示了可轉換為時間戳 C 資料的 ODBC SQL 資料類型。 有關表中列與字語的說明,請參考[資料從 C 轉換為 SQL 資料型態](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 類型識別碼|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|列位元組長度>= 字元位長度<br /><br /> 19 <= 列位元組長度<字元位長度<br /><br /> 列位元組長度< 19<br /><br /> 資料值不是有效的時間戳|n/a<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|列字元長度>= 資料的字元長度<br /><br /> 19 <= 列字元長度<字元長度的資料<br /><br /> 列字元長度< 19<br /><br /> 資料值不是有效的時間戳|n/a<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|時間欄位為零<br /><br /> 時間欄位為非零<br /><br /> 資料值不包含有效日期|n/a<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIME|分數秒欄位為零 [a]<br /><br /> 分數秒欄位是非零 [a]<br /><br /> 資料值不包含有效時間|n/a<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|分數秒欄位未截斷<br /><br /> 分數秒欄位被截斷<br /><br /> 資料值不是有效的時間戳|n/a<br /><br /> 22008<br /><br /> 22007|  
  
 [a] 時間戳結構的日期欄位將被忽略。  
  
 有關哪些值在SQL_C_TIMESTAMP結構中有效的資訊,請參閱本附錄前面介紹[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)。  
  
 當時間戳 C 資料轉換為字元 SQL 資料時,生成的字元資料位於 *「yyyymm*-*mm*-*dd* *hh**:mm:ss」**ss*中。*f...* 格式。  
  
 當從時間戳 C 資料類型轉換數據時,驅動程式會忽略長度/ 指示器值,並假定數據緩衝區的大小是時間戳 C 資料類型的大小。 長度/指標值在**SQLPutData**中的*StrLen_or_Ind*參數中傳遞,在**SQLBind 參數**中用*StrLen_or_IndPtr*參數指定的緩衝區中傳遞。 數據緩衝區使用**SQLPutData**中的*DataPtr*參數和**SQLBind 參數**中的*參數 ValuePtr*參數指定。
