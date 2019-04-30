---
title: C 轉換為 SQL：Timestamp | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: a738712a8fb1b032ef8244f579b10fdcc22becee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63241424"
---
# <a name="c-to-sql-timestamp"></a>C 轉換為 SQL：時間戳記
時間戳記 ODBC C 資料類型的識別項是：  
  
 SQL_C_TYPE_TIMESTAMP  
  
 下表顯示 ODBC SQL 時間戳記 C 資料可能會轉換成的資料類型。 如需資料行和資料表中的詞彙說明，請參閱 <<c0> [ 轉換將資料從 C 到 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 型別識別項|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|資料行的位元組長度 > = 字元位元組長度<br /><br /> 19 < = 資料行的位元組長度 < 字元位元組長度<br /><br /> 資料行的位元組長度 < 19<br /><br /> 資料值不是有效的時間戳記|n/a<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|資料行的字元長度 > = 字元長度的資料<br /><br /> 19 < = 資料行的字元長度 < 字元長度的資料<br /><br /> 資料行的字元長度 < 19<br /><br /> 資料值不是有效的時間戳記|n/a<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|時間欄位都是零<br /><br /> 時間欄位為非零值<br /><br /> 資料值不包含有效的日期|n/a<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIME|小數秒欄位都是零 [a]<br /><br /> 小數秒欄位為非零值 [a]<br /><br /> 資料值不包含有效的時間|n/a<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|不會被截斷的小數秒數欄位<br /><br /> 小數秒欄位會被截斷<br /><br /> 資料值不是有效的時間戳記|n/a<br /><br /> 22008<br /><br /> 22007|  
  
 [a] 的日期時間戳記結構的欄位會被忽略。  
  
 如需哪些值是有效 SQL_C_TIMESTAMP 結構中的資訊，請參閱[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)稍早在本附錄中。  
  
 時間戳記 C 資料轉換為字元的 SQL 資料，產生的字元資料時，在 「*yyyy*-*mm*-*dd* *hh*:*mm*:*ss*[。*f...*]"格式。  
  
 驅動程式將資料轉換的時間戳記 C 資料類型時，會忽略長度/指標值，並假設資料緩衝區的大小，是時間戳記 C 資料類型的大小。 傳入的長度/指標值無效*Strlen_or_ind&lt*中的引數**SQLPutData**並使用指定的緩衝區中*StrLen_or_IndPtr*引數中**SQLBindParameter**。 使用指定的資料緩衝區*DataPtr*中的引數**SQLPutData**並*ParameterValuePtr*中的引數**SQLBindParameter**.
