---
title: "SQL 到 C： 時間戳記 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data conversions from C to SQL types [ODBC], timestamp
- timestamp data type [ODBC]
- converting data from c to SQL types [ODBC], timestamp
ms.assetid: 0e08bfff-68f9-4648-9558-09b57fea08ad
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 472afd8fa958dd4602510a04c14a1268fe713194
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="c-to-sql-timestamp"></a>SQL 到 C： 時間戳記
時間戳記 ODBC C 資料類型的識別項是：  
  
 SQL_C_TYPE_TIMESTAMP  
  
 下表顯示 ODBC SQL 時間戳記 C 資料可能會轉換成資料類型。 如需的資料行和資料表中的詞彙說明，請參閱[轉換資料從 C 到 SQL 資料型別](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 類型識別碼|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|資料行的位元組長度 > = 字元位元組長度<br /><br /> 19 < = 資料行的位元組長度 < 字元位元組長度<br /><br /> 資料行長度的位元組數 < 19<br /><br /> 資料值不是有效的時間戳記|n/a<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|資料行的字元長度 > = 字元長度的資料<br /><br /> 19 < = 資料行的字元長度 < 字元長度的資料<br /><br /> 資料行的字元長度 < 19<br /><br /> 資料值不是有效的時間戳記|n/a<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|時間欄位都是零<br /><br /> 時間欄位會為非零，<br /><br /> 資料值不包含有效的日期|n/a<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIME|小數秒欄位是零 [a]<br /><br /> 小數秒欄位是為非零，[a]<br /><br /> 資料值不包含有效的時間|n/a<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|小數秒數欄位不會被截斷<br /><br /> 小數秒欄位會被截斷<br /><br /> 資料值不是有效的時間戳記|n/a<br /><br /> 22008<br /><br /> 22007|  
  
 [a] 的日期時間戳記結構的欄位會被忽略。  
  
 如需有效值 SQL_C_TIMESTAMP 結構中的資訊，請參閱[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)稍早在本附錄中。  
  
 當時間戳記 C 資料轉換成字元的 SQL 資料時，產生的字元資料就會處於 「*yyyy*-*公釐*-*dd* *hh*:*公釐*:*ss*[。*f...*]"格式。  
  
 驅動程式會忽略時間戳記 C 資料類型轉換資料的長度/指標值，並假設資料緩衝區的大小是時間戳記 C 資料類型的大小。 長度/指標值傳遞*StrLen_or_Ind*引數中的**SQLPutData**並使用指定的緩衝區中*StrLen_or_IndPtr*引數中**SQLBindParameter**。 使用指定的資料緩衝區*DataPtr*引數中的**SQLPutData**和*ParameterValuePtr*引數中的**SQLBindParameter**.
