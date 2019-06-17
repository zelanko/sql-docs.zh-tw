---
title: SQL 轉換為 C：Timestamp | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- timestamp data type [ODBC]
- converting data from SQL to C types [ODBC], timestamp
- data conversions from SQL to C types [ODBC], timestamp
ms.assetid: 6a0617cf-d8c0-4316-8bb4-e6ddb45d7bf1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 69c9f1258f35a69d6554783f5d1b4ca79be313d2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63259263"
---
# <a name="sql-to-c-timestamp"></a>SQL 轉換為 C：時間戳記

時間戳記的 ODBC SQL 資料類型的識別項是下列項目：

- SQL_TYPE_TIMESTAMP  

下表顯示 ODBC C 資料類型可以轉換為時間戳記的 SQL 資料。 如需資料行和資料表中的詞彙說明，請參閱 <<c0> [ 轉換將資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  

|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > 字元位元組長度<br /><br /> 20 < = *Columnsize* < = 字元位元組長度<br /><br /> *BufferLength* < 20|資料<br /><br /> 截斷的資料 [b]<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > 字元長度<br /><br /> 20 < = *Columnsize* < = 字元長度<br /><br /> *BufferLength* < 20|資料<br /><br /> 截斷的資料 [b]<br /><br /> 未定義|以字元為單位的資料長度<br /><br /> 以字元為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|資料的位元組長度 < = *Columnsize*<br /><br /> 資料的位元組長度 > *Columnsize*|資料<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_TYPE_DATE|時間戳記的時間部分為零 [a]<br /><br /> 時間戳記的時間部分為非零值 [a]|資料<br /><br /> 截斷的資料 [c]|6[f]<br /><br /> 6[f]|n/a<br /><br /> 01S07|  
|SQL_C_TYPE_TIME|時間戳記的小數秒數部分為零 [a]<br /><br /> 時間戳記的小數秒數部分為非零值 [a]|Data[d]<br /><br /> 截斷的資料 [d]、 [e]|6[f]<br /><br /> 6[f]|n/a<br /><br /> 01S07|  
|SQL_C_TYPE_TIMESTAMP|不會被截斷的小數秒數部分的時間戳記 [a]<br /><br /> 會被截斷的小數秒數部分的時間戳記，[a]|Data[e]<br /><br /> 截斷的資料 [e]|16[f]<br /><br /> 16[f]|n/a<br /><br /> 01S07|  

 [a] 的值*Columnsize*會忽略這項轉換。 驅動程式會假設大小 **TargetValuePtr*是 C 資料類型的大小。  
  
 [b] 的小數秒數時間戳記會被截斷。  
  
 [c] 時間部分的時間戳記會被截斷。  
  
 [時間戳記 d] 的日期部分會被忽略。  
  
 [截斷時間戳記 e] 的小數秒數部分。  
  
 [f] 這是對應的 C 資料類型的大小。  

當時間戳記的 SQL 資料轉換成 C 字元資料時，產生的字串是在 「*yyyy*-*mm*-*dd* *hh*:*公釐*:*ss*[。*f...* ]"格式，其中最多九個數字可用於小數秒數。 此格式不會受到 Windows® 國家/地區設定。 （除了小數位數和小數秒數，整個格式必須使用，不論時間戳記 SQL 資料類型的有效位數。）
