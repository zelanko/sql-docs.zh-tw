---
title: C 到 SQL： GUID |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306619"
---
# <a name="c-to-sql-guid"></a>C 到 SQL：GUID
GUID ODBC C 資料類型的識別碼為：  
  
 SQL_C_GUID  
  
 下表顯示可轉換 GUID C 資料的 ODBC SQL 資料類型。 如需資料表中的資料行和詞彙的說明，請參閱將[資料從 C 轉換成 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 類型識別碼|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|資料行位元組長度 >= 36|n/a|  
|SQL_VARCHAR|資料行位元組長度 < 36|22001|  
|SQL_LONGVARCHAR|資料值不是有效的 GUID|22018|  
|SQL_WCHAR|資料行字元長度 >= 36|n/a|  
|SQL_WVARCHAR|資料行字元長度 < 36|22001|  
|SQL_WLONGVARCHAR|資料值不是有效的 GUID|22018|  
|SQL_GUID|無 [a]|n/a|  
  
 [a] 所有的十六進位值都是有效的 GUID。  
  
 從 GUID C 資料類型轉換資料時，驅動程式會忽略長度/指標值，並假設資料緩衝區的大小是 GUID C 資料類型的大小。 長度/指標值會傳入**SQLPutData**中的*StrLen_or_Ind*引數，以及在**SQLBindParameter**中使用*StrLen_or_IndPtr*引數指定的緩衝區。 資料緩衝區會使用**SQLPutData**中的*DataPtr*引數和**SQLBindParameter**中的*ParameterValuePtr*引數來指定。
