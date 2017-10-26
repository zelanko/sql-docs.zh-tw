---
title: "SQL 到 c: GUID |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from SQL to C types [ODBC], GUID
- data conversions from SQL to C types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: cf56c684-c261-4b89-994a-db14ab2241d6
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0d60ca76d44f443c564bd354535833ab6c7b407f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sql-to-c-guid"></a>SQL 到 c: GUID
GUID ODBC SQL 資料類型的識別項是：  
  
 SQL_GUID  
  
 下表顯示 ODBC C 資料類型可能會轉換 GUID SQL 資料。 如需的資料行和資料表中的詞彙說明，請參閱[轉換資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*Columnsize* > 字元位元組長度|data|36|n/a|  
||*Columnsize* < 37|未定義|未定義|22003|  
|SQL_C_WCHAR|*Columnsize* > 字元長度|data|36|n/a|  
||*Columnsize* < 37|未定義|未定義|22003|  
|SQL_C_BINARY|資料的位元組長度\< =  *Columnsize*|data|以位元組為單位的資料長度|n/a|  
||資料的位元組長度 > *Columnsize*|未定義|未定義|22003|  
|SQL_C_GUID|無 [a]|data|16 [b]|n/a|  
  
 [a] 的值*Columnsize*會忽略這項轉換。 驅動程式假設大小 **TargetValuePtr*是 C 資料類型的大小。  
  
 [b] 這是對應的 C 資料類型的大小。

