---
title: C 轉換為 SQL：GUID | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: af0ed8307652ccf45e7fbfffb6c00355c8a8b004
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63159358"
---
# <a name="c-to-sql-guid"></a>C 轉換為 SQL：GUID
GUID ODBC C 資料類型的識別項是：  
  
 SQL_C_GUID  
  
 下表顯示 ODBC SQL GUID C 資料可能會轉換成的資料類型。 如需資料行和資料表中的詞彙說明，請參閱 <<c0> [ 轉換將資料從 C 到 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 型別識別項|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|資料行的位元組長度 > = 36|n/a|  
|SQL_VARCHAR|資料行的位元組長度 < 36|22001|  
|SQL_LONGVARCHAR|資料值不是有效的 GUID|22018|  
|SQL_WCHAR|資料行的字元長度 > = 36|n/a|  
|SQL_WVARCHAR|資料行的字元長度 < 36|22001|  
|SQL_WLONGVARCHAR|資料值不是有效的 GUID|22018|  
|SQL_GUID|None[a]|n/a|  
  
 [a] 所有的十六進位值的有效期為 GUID。  
  
 驅動程式將資料從 GUID C 資料類型轉換時，會忽略長度/指標值，並假設資料緩衝區的大小是 GUID C 資料類型的大小。 傳入的長度/指標值無效*Strlen_or_ind&lt*中的引數**SQLPutData**並使用指定的緩衝區中*StrLen_or_IndPtr*引數中**SQLBindParameter**。 使用指定的資料緩衝區*DataPtr*中的引數**SQLPutData**並*ParameterValuePtr*中的引數**SQLBindParameter**.
