---
title: C 到 SQL：時間戳記 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aa75299f4d8e8f15293064d0bf3fb3979fe382d1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037700"
---
# <a name="c-to-sql-timestamp"></a>C 到 SQL：時間戳記
時間戳記 ODBC C 資料類型的識別碼為：  
  
 SQL_C_TYPE_TIMESTAMP  
  
 下表顯示可能轉換時間戳記 C 資料的 ODBC SQL 資料類型。 如需資料表中的資料行和詞彙的說明，請參閱將[資料從 C 轉換成 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 類型識別碼|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|資料行位元組長度 >= 字元位元組長度<br /><br /> 19 <= 資料行位元組長度 < 字元位元組長度<br /><br /> 資料行位元組長度 < 19<br /><br /> 資料值不是有效的時間戳記|n/a<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|資料行字元長度 >= 字元長度<br /><br /> 19 <= 資料行字元長度 < 字元長度<br /><br /> 資料行字元長度 < 19<br /><br /> 資料值不是有效的時間戳記|n/a<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|時間欄位為零<br /><br /> 時間欄位不是零<br /><br /> 資料值不包含有效的日期|n/a<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIME|小數秒數位段為零 [a]<br /><br /> 小數秒數位段不是零 [a]<br /><br /> 資料值不包含有效的時間|n/a<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|小數秒數位段不會被截斷<br /><br /> 小數秒欄位已截斷<br /><br /> 資料值不是有效的時間戳記|n/a<br /><br /> 22008<br /><br /> 22007|  
  
 [a] 已忽略 timestamp 結構的日期欄位。  
  
 如需 SQL_C_TIMESTAMP 結構中有效值的相關資訊，請參閱本附錄稍早的[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)。  
  
 當時間戳 C 資料轉換成字元 SQL 資料時，產生的字元資料會是 "*yyyy*-*mm*-*dd* *hh*：*mm*：*ss*[。*f ...*] "編排.  
  
 從 timestamp C 資料類型轉換資料時，驅動程式會忽略長度/指標值，並假設資料緩衝區的大小為時間戳記 C 資料類型的大小。 長度/指標值會傳入**SQLPutData**中的*StrLen_or_Ind*引數，以及在**SQLBindParameter**中使用*StrLen_or_IndPtr*引數指定的緩衝區。 資料緩衝區會使用**SQLPutData**中的*DataPtr*引數和**SQLBindParameter**中的*ParameterValuePtr*引數來指定。
