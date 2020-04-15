---
title: SQL 到 C:日期 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe9656c0c02c0ff5a10029525da3d38280530cc3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296528"
---
# <a name="sql-to-c-date"></a>SQL 到 C：日期
日期 ODBC SQL 資料類型的識別碼是:  
  
 SQL_TYPE_DATE  
  
 下表顯示了可以轉換 SQL 資料的 ODBC C 資料類型。 有關表中列與字語的說明,請參考[資料從 SQL 轉換為 C 資料型態](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**目標價值Ptr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*緩衝區長度*>字符字节长度<br /><br /> 11 <=*緩衝區長度*<= 字元位長度<br /><br /> *緩衝區長度*< 11|資料<br /><br /> 截斷的資料<br /><br /> 未定義|10<br /><br /> 以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*緩衝區長度*>字符长度<br /><br /> 11<=*緩衝區長度*<= 字元長度<br /><br /> *緩衝區長度*< 11|資料<br /><br /> 截斷的資料<br /><br /> 未定義|10<br /><br /> 字元中的資料長度<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|資料<位元組長度 =*緩衝區長度*<br /><br /> >*緩衝區長度*的資料位元組長度|資料<br /><br /> 未定義|以位元組為單位的資料長度<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_TYPE_DATE|無[a]|資料|6[c]|n/a|  
|SQL_C_TYPE_TIMESTAMP|無[a]|資料[b]|16[c]|n/a|  
  
 [a] 此轉換將忽略*緩衝區長度*的值。 驅動程式假定 **目標價值Ptr*的大小是 C 資料類型的大小。  
  
 [b] 時間戳結構的時間欄位設置為零。  
  
 [c] 這是相應的 C 資料類型的大小。  
  
 當 SQL 資料轉換為字元 C 資料的日期時,生成的字串採用 *「yyyymm*-*mm*-*dd」* 格式。 此格式不受 Windows ®國家 / 地區設置的影響。
