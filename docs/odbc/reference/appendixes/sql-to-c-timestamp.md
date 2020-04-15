---
title: SQL 到 C:時間戳 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 552bab585e4480fd922c9b9a6b112830f5c11ad9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296348"
---
# <a name="sql-to-c-timestamp"></a>SQL 到 C：時間戳記

時間戳 ODBC SQL 資料類型的識別碼如下:

- SQL_TYPE_TIMESTAMP  

下表顯示了可轉換為時間戳 SQL 資料的 ODBC C 資料類型。 有關表中列與字語的說明,請參考[資料從 SQL 轉換為 C 資料型態](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  

|C 類型識別碼|測試|**目標價值Ptr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*緩衝區長度*>字符字节长度<br /><br /> 20 個<=*緩衝區長度*<= 字元位節長度<br /><br /> *緩衝區長度*< 20|資料<br /><br /> 截斷的資料[b]<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*緩衝區長度*>字符长度<br /><br /> 20 <=*緩衝區長度*<= 字元長度<br /><br /> *緩衝區長度*< 20|資料<br /><br /> 截斷的資料[b]<br /><br /> 未定義|字元中的資料長度<br /><br /> 字元中的資料長度<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|資料<位元組長度 =*緩衝區長度*<br /><br /> >*緩衝區長度*的資料位元組長度|資料<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_TYPE_DATE|時間戳的時間部分為零[a]<br /><br /> 時間戳的時間部分是非零[a]|資料<br /><br /> 截斷資料[c]|6[f]<br /><br /> 6[f]|n/a<br /><br /> 01S07|  
|SQL_C_TYPE_TIME|時間戳的分數秒部份為零 [a]<br /><br /> 時間戳的分數秒部分是非零[a]|資料[d]<br /><br /> 截斷資料[d],[e]|6[f]<br /><br /> 6[f]|n/a<br /><br /> 01S07|  
|SQL_C_TYPE_TIMESTAMP|時間戳的分數秒部分不會截斷[a]<br /><br /> 時間戳的分數秒部分被截斷[a]|資料[e]<br /><br /> 截斷資料[e]|16[f]<br /><br /> 16[f]|n/a<br /><br /> 01S07|  

 [a] 此轉換將忽略*緩衝區長度*的值。 驅動程式假定 **目標價值Ptr*的大小是 C 資料類型的大小。  
  
 [b] 時間戳的小數秒被截斷。  
  
 [c] 時間戳的時間部分被截斷。  
  
 [d] 時間戳的日期部分將被忽略。  
  
 [e] 時間戳的小秒部分被截斷。  
  
 [f] 這是相應的 C 資料類型的大小。  

當時間戳 SQL 資料轉換為字元 C 資料時,生成的字串位於 *「yyyymm*-*mm*-*dd* *hh**:mm:ss」**ss*中。*f...* 格式,其中最多九位數位可用於小數秒。 此格式不受 Windows ®國家 / 地區設置的影響。 (除了小數點和小數秒外,無論時間戳 SQL 數據類型的精度如何,都必須使用整個格式。
