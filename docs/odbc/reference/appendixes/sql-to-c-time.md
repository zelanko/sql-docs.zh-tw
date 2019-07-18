---
title: SQL 轉換為 C：時間 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], time
- time data type [ODBC]
- data conversions from SQL to C types [ODBC], time
ms.assetid: 6dc59973-7bb5-40f1-87c8-5bf68b3bf2ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 99f8219ef53f72b0d7ab1477bba5d24d441a3141
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065086"
---
# <a name="sql-to-c-time"></a>SQL 轉換為 C：Time
ODBC SQL 資料類型是次識別碼：  
  
 SQL_TYPE_TIME  
  
 下表顯示 ODBC C 資料類型可能會轉換時間 SQL 資料。 如需資料行和資料表中的詞彙說明，請參閱 <<c0> [ 轉換將資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > 字元位元組長度<br /><br /> *9* <= *Columnsize* < = 字元位元組長度<br /><br /> *BufferLength* < 9|Data<br /><br /> 截斷的資料 [a]<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > 字元長度<br /><br /> *9* <= *Columnsize* < = 字元長度<br /><br /> *BufferLength* < 9|Data<br /><br /> 截斷的資料 [a]<br /><br /> 未定義|以字元為單位的資料長度<br /><br /> 以字元為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|資料的位元組長度 < = *Columnsize*<br /><br /> 資料的位元組長度 > *Columnsize*|Data<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_TYPE_TIME|無 [b]|Data|6[d]|n/a|  
|SQL_C_TYPE_TIMESTAMP|無 [b]|資料 [c]|16 [d]|n/a|  
  
 [a] 的小數秒數時間會被截斷。  
  
 [b] 的值*Columnsize*會忽略這項轉換。 驅動程式會假設大小 **TargetValuePtr*是 C 資料類型的大小。  
  
 [時間戳記結構 c] 的日期欄位設定為目前的日期和時間戳記結構的小數秒欄位設定為零。  
  
 [d] 這是對應的 C 資料類型的大小。  
  
 當時間 SQL 資料轉換成 C 字元資料時，產生的字串是在 「*hh*:*mm*:*ss*」 格式。 此格式不會受到 Windows® 國家/地區設定。
