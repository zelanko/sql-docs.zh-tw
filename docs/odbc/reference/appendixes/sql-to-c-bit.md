---
title: SQL 到 C:位 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], bit
- bit data type [ODBC]
- data conversions from SQL to C types [ODBC], bit
ms.assetid: 0eeaab8b-ad82-4a36-b464-9a1211d5f72c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 57688f34c504b221f77c1b66792bf9ee9398df27
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296748"
---
# <a name="sql-to-c-bit"></a>SQL 到 C：位元
位 ODBC SQL 資料類型的識別碼是:  
  
 SQL_BIT  
  
 下表顯示了可以轉換為位 SQL 資料的 ODBC C 資料類型。 有關表中列與字語的說明,請參考[資料從 SQL 轉換為 C 資料型態](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**目標價值Ptr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR<br /><br /> SQL_C_WCHAR|*緩衝區長度*> 1<br /><br /> *緩衝區長度*<= 1|資料<br /><br /> 未定義|1<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE<br /><br /> SQL_C_NUMERIC|無[a]|資料|C 資料型態大小|n/a|  
|SQL_C_BIT|無[a]|資料|1[b]|n/a|  
|SQL_C_BINARY|*緩衝區長度*>= 1<br /><br /> *緩衝區長度*< 1|資料<br /><br /> 未定義|1<br /><br /> 未定義|n/a<br /><br /> 22003|  
  
 [a] 此轉換將忽略*緩衝區長度*的值。 驅動程式假定 **目標價值Ptr*的大小是 C 資料類型的大小。  
  
 [b] 這是相應的 C 資料類型的大小。  
  
 當位 SQL 資料轉換為字元 C 數據時,可能的值是"0"和"1"。
