---
title: 'SQL 到 c: GUID |Microsoft 文件'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- converting data from SQL to C types [ODBC], GUID
- data conversions from SQL to C types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: cf56c684-c261-4b89-994a-db14ab2241d6
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0a0e4d11048f532f91cc4fc06f85f6c1e355d1d4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sql-to-c-guid"></a>SQL 到 c: GUID
GUID ODBC SQL 資料類型的識別項是：  
  
 SQL_GUID  
  
 下表顯示 ODBC C 資料類型可能會轉換 GUID SQL 資料。 如需的資料行和資料表中的詞彙說明，請參閱[轉換資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*Columnsize* > 字元位元組長度|資料|36|n/a|  
||*Columnsize* < 37|未定義|未定義|22003|  
|SQL_C_WCHAR|*Columnsize* > 字元長度|資料|36|n/a|  
||*Columnsize* < 37|未定義|未定義|22003|  
|SQL_C_BINARY|資料的位元組長度\< =  *Columnsize*|資料|以位元組為單位的資料長度|n/a|  
||資料的位元組長度 > *Columnsize*|未定義|未定義|22003|  
|SQL_C_GUID|無 [a]|資料|16 [b]|n/a|  
  
 [a] 的值*Columnsize*會忽略這項轉換。 驅動程式假設大小 **TargetValuePtr*是 C 資料類型的大小。  
  
 [b] 這是對應的 C 資料類型的大小。
