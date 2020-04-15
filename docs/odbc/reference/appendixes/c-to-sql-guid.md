---
title: 'C 到 SQL: GUID |微軟文件'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], guid
- data conversions from C to SQL types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: 9168b0b6-a828-4fef-b8cd-bdf439776f23
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b3b559499273e885e23da10d9093a0ce9ff92393
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306619"
---
# <a name="c-to-sql-guid"></a>C 到 SQL：GUID
GUID ODBC C 資料類型的識別碼是:  
  
 SQL_C_GUID  
  
 下表顯示了 GUID C 數據可以轉換為的 ODBC SQL 資料類型。 有關表中列與字語的說明,請參考[資料從 C 轉換為 SQL 資料型態](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 類型識別碼|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|列位元組長度>= 36|n/a|  
|SQL_VARCHAR|柱位元組長度< 36|22001|  
|SQL_LONGVARCHAR|資料值不是有效的 GUID|22018|  
|SQL_WCHAR|列字元長度>= 36|n/a|  
|SQL_WVARCHAR|列字元長度< 36|22001|  
|SQL_WLONGVARCHAR|資料值不是有效的 GUID|22018|  
|SQL_GUID|無[a]|n/a|  
  
 [a] 所有十六進位值都作為 GUID 有效。  
  
 驅動程式在從 GUID C 資料類型轉換數據時忽略長度/指示器值,並假定數據緩衝區的大小是 GUID C 數據類型的大小。 長度/指標值在**SQLPutData**中的*StrLen_or_Ind*參數中傳遞,在**SQLBind 參數**中用*StrLen_or_IndPtr*參數指定的緩衝區中傳遞。 數據緩衝區使用**SQLPutData**中的*DataPtr*參數和**SQLBind 參數**中的*參數 ValuePtr*參數指定。
