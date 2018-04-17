---
title: SQL 到 c： 時間戳記 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- timestamp data type [ODBC]
- converting data from SQL to C types [ODBC], timestamp
- data conversions from SQL to C types [ODBC], timestamp
ms.assetid: 6a0617cf-d8c0-4316-8bb4-e6ddb45d7bf1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 66e6d84f713911b91bc55a8757bb6b149d6ec582
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sql-to-c-timestamp"></a>SQL 到 c： 時間戳記
時間戳記 ODBC SQL 資料類型的識別項是：  
  
 SQL_TYPE_TIMESTAMP  
  
 下表顯示 ODBC C 時間戳記 SQL 資料可以轉換成資料類型。 如需的資料行和資料表中的詞彙說明，請參閱[轉換資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*Columnsize* > 字元位元組長度<br /><br /> 20 < = *Columnsize* < = 字元位元組長度<br /><br /> *Columnsize* < 20|資料<br /><br /> 截斷的資料 [b]<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*Columnsize* > 字元長度<br /><br /> 20 < = *Columnsize* < = 字元長度<br /><br /> *Columnsize* < 20|資料<br /><br /> 截斷的資料 [b]<br /><br /> 未定義|以字元為單位的資料長度<br /><br /> 以字元為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|資料的位元組長度 < = *Columnsize*<br /><br /> 資料的位元組長度 > *Columnsize*|資料<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_TYPE_DATE|時間戳記的時間部分為零 [a]<br /><br /> 時間戳記的時間部分是為非零，[a]|資料<br /><br /> 截斷的資料 [c]|6 [f]<br /><br /> 6 [f]|n/a<br /><br /> 01S07|  
|SQL_C_TYPE_TIME|時間戳記的小數秒數部分為零 [a]<br /><br /> 小數秒數部分的時間戳記是為非零，[a]|資料 [d]<br /><br /> 截斷的資料 [d]、 [e]|6 [f]<br /><br /> 6 [f]|n/a<br /><br /> 01S07|  
_C_TYPE_TIMESTAMP|不會截斷小數秒數部分的時間戳記，[a]<br /><br /> 會截斷小數秒數部分的時間戳記，[a]|資料 [e]<br /><br /> 截斷的資料 [e]|16 [f]<br /><br /> 16 [f]|n/a<br /><br /> 01S07|  
  
 [a] 的值*Columnsize*會忽略這項轉換。 驅動程式假設大小 **TargetValuePtr*是 C 資料類型的大小。  
  
 [b] 的小數秒的時間戳記會被截斷。  
  
 [時間戳記 c] 的時間部分會被截斷。  
  
 [d] 日期部分的時間戳記會被忽略。  
  
 [時間戳記 e] 的小數秒數部分會被截斷。  
  
 [f] 這是對應的 C 資料類型的大小。  
  
 當時間戳記 SQL 資料轉換成 C 字元資料時，產生的字串就會處於 「*yyyy*-*公釐*-*dd* *hh*:*公釐*:*ss*[。*f...*]"格式，其中使用高達九位數，小數秒數。 此格式不受 Windows® 國家/地區設定。 （除了小數點和小數秒數，整個格式必須使用，不論時間戳記 SQL 資料類型的有效位數。）
