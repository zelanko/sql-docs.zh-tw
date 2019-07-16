---
title: SQL 轉換為 C：日期 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], date
- date data type [ODBC]
- data conversions from SQL to C types [ODBC], date
ms.assetid: 703c7960-9cf4-4d7a-9920-53b29c184f97
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d282798a31ac9059ed3c1901ea01f1f3104f09c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056877"
---
# <a name="sql-to-c-date"></a>SQL 轉換為 C：Date
日期的 ODBC SQL 資料類型的識別項是：  
  
 SQL_TYPE_DATE  
  
 下表顯示 ODBC C 資料類型可能會轉換日期的 SQL 資料。 如需資料行和資料表中的詞彙說明，請參閱 <<c0> [ 轉換將資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > 字元位元組長度<br /><br /> 11 < = *Columnsize* < = 字元位元組長度<br /><br /> *BufferLength* < 11|Data<br /><br /> 截斷的資料<br /><br /> 未定義|10<br /><br /> 以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > 字元長度<br /><br /> 11 < = *Columnsize* < = 字元長度<br /><br /> *BufferLength* < 11|Data<br /><br /> 截斷的資料<br /><br /> 未定義|10<br /><br /> 以字元為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|資料的位元組長度 < = *Columnsize*<br /><br /> 資料的位元組長度 > *Columnsize*|Data<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_TYPE_DATE|無 [a]|Data|6[c]|n/a|  
|SQL_C_TYPE_TIMESTAMP|無 [a]|資料 [b]|16[c]|n/a|  
  
 [a] 的值*Columnsize*會忽略這項轉換。 驅動程式會假設大小 **TargetValuePtr*是 C 資料類型的大小。  
  
 [時間戳記結構 b] 的時間欄位會設定為零。  
  
 [c] 這是對應的 C 資料類型的大小。  
  
 當日期 SQL 資料轉換成 C 字元資料時，產生的字串是在 「*yyyy*-*mm*-*dd*」 格式。 此格式不會受到 Windows® 國家/地區設定。
