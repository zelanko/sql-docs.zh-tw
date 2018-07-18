---
title: SQL 到 c： 日期 |Microsoft 文件
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
- converting data from SQL to C types [ODBC], date
- date data type [ODBC]
- data conversions from SQL to C types [ODBC], date
ms.assetid: 703c7960-9cf4-4d7a-9920-53b29c184f97
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d99ebd45ffa463ccfd66bd751dd7415b35a8f5d1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32908863"
---
# <a name="sql-to-c-date"></a>SQL 到 c： 日期
日期的 ODBC SQL 資料類型的識別項是：  
  
 SQL_TYPE_DATE  
  
 下表顯示 ODBC C 資料類型可能會轉換日期 SQL 資料。 如需的資料行和資料表中的詞彙說明，請參閱[轉換資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*Columnsize* > 字元位元組長度<br /><br /> 11 < = *Columnsize* < = 字元位元組長度<br /><br /> *Columnsize* < 11|資料<br /><br /> 截斷的資料<br /><br /> 未定義|10<br /><br /> 以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*Columnsize* > 字元長度<br /><br /> 11 < = *Columnsize* < = 字元長度<br /><br /> *Columnsize* < 11|資料<br /><br /> 截斷的資料<br /><br /> 未定義|10<br /><br /> 以字元為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|資料的位元組長度 < = *Columnsize*<br /><br /> 資料的位元組長度 > *Columnsize*|資料<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_TYPE_DATE|無 [a]|資料|6 [c]|n/a|  
|SQL_C_TYPE_TIMESTAMP|無 [a]|資料 [b]|16 [c]|n/a|  
  
 [a] 的值*Columnsize*會忽略這項轉換。 驅動程式假設大小 **TargetValuePtr*是 C 資料類型的大小。  
  
 [時間戳記結構的 b] 時間欄位會設定為零。  
  
 [c] 這是對應的 C 資料類型的大小。  
  
 當日期 SQL 資料轉換成 C 字元資料時，產生的字串就會處於 「*yyyy*-*公釐*-*dd*」 格式。 此格式不受 Windows® 國家/地區設定。
