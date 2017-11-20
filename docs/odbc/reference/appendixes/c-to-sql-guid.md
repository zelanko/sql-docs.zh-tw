---
title: "C 到 SQL: GUID |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from c to SQL types [ODBC], guid
- data conversions from C to SQL types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: 9168b0b6-a828-4fef-b8cd-bdf439776f23
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 36aadcf415fcf447f87f5952f6b6d32c921b07c2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="c-to-sql-guid"></a>C 到 SQL: GUID
GUID ODBC C 資料類型的識別項是：  
  
 SQL_C_GUID  
  
 下表顯示 ODBC SQL GUID C 資料可能會轉換成資料類型。 如需的資料行和資料表中的詞彙說明，請參閱[轉換資料從 C 到 SQL 資料型別](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 類型識別碼|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|資料行的位元組長度 > = 36|n/a|  
|SQL_VARCHAR|資料行長度的位元組數 < 36|22001|  
|SQL_LONGVARCHAR|資料值不是有效的 GUID|22018|  
|SQL_WCHAR|資料行的字元長度 > = 36|n/a|  
|SQL_WVARCHAR|資料行的字元長度 < 36|22001|  
|SQL_WLONGVARCHAR|資料值不是有效的 GUID|22018|  
|SQL_GUID|無 [a]|n/a|  
  
 [a] 所有的十六進位值為有效的 guid。  
  
 驅動程式將資料轉換從 GUID C 資料類型時，會忽略長度/指標值，並假設資料緩衝區的大小是 GUID C 資料類型的大小。 長度/指標值傳遞*StrLen_or_Ind*引數中的**SQLPutData**並使用指定的緩衝區中*StrLen_or_IndPtr*引數中**SQLBindParameter**。 使用指定的資料緩衝區*DataPtr*引數中的**SQLPutData**和*ParameterValuePtr*引數中的**SQLBindParameter**.

