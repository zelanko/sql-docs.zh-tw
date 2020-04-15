---
title: SQL 到 C:時間 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ebd146abf650861099a40bf91b2641df768b343d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296378"
---
# <a name="sql-to-c-time"></a>SQL 到 C：時間
ODBC SQL 資料類型的時間識別碼為:  
  
 SQL_TYPE_TIME  
  
 下表顯示了可以轉換 SQL 資料的時間的 ODBC C 資料類型。 有關表中列與字語的說明,請參考[資料從 SQL 轉換為 C 資料型態](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**目標價值Ptr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*緩衝區長度*>字符字节长度<br /><br /> *9* <= *緩衝區長度*<= 字元位長度<br /><br /> *緩衝區長度*< 9|資料<br /><br /> 截斷的資料[a]<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*緩衝區長度*>字符长度<br /><br /> *9* <= *緩衝區長度*<= 字元長度<br /><br /> *緩衝區長度*< 9|資料<br /><br /> 截斷的資料[a]<br /><br /> 未定義|字元中的資料長度<br /><br /> 字元中的資料長度<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|資料<位元組長度 =*緩衝區長度*<br /><br /> >*緩衝區長度*的資料位元組長度|資料<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_TYPE_TIME|無[b]|資料|6[d]|n/a|  
|SQL_C_TYPE_TIMESTAMP|無[b]|資料[c]|16[d]|n/a|  
  
 [a] 時間的小秒被截斷。  
  
 [b] 此轉換將忽略*緩衝區長度*的值。 驅動程式假定 **目標價值Ptr*的大小是 C 資料類型的大小。  
  
 [c] 時間戳結構的日期欄位設置為當前日期,時間戳結構的小數秒欄位設置為零。  
  
 [d] 這是相應的 C 資料類型的大小。  
  
 當 SQL 資料轉換為字元 C 資料時,生成的字串採用 *「hh:mm:**mm**ss」* 格式。 此格式不受 Windows ®國家 / 地區設置的影響。
