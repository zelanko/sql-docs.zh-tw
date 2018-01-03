---
title: "SQL 到 c： 位元 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from SQL to c types [ODBC], bit
- bit data type [ODBC]
- data conversions from SQL to C types [ODBC], bit
ms.assetid: 0eeaab8b-ad82-4a36-b464-9a1211d5f72c
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3b0cb6f2dacadde22ee78b6cbb4b9acc3e824630
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sql-to-c-bit"></a>SQL 到 c： 位元
位元 ODBC SQL 資料類型的識別項是：  
  
 SQL_BIT  
  
 下表顯示 ODBC C 位元 SQL 資料可能會轉換成資料類型。 如需的資料行和資料表中的詞彙說明，請參閱[轉換資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR<br /><br /> SQL_C_WCHAR|*Columnsize* > 1<br /><br /> *Columnsize* < = 1|data<br /><br /> 未定義|@shouldalert<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE<br /><br /> SQL_C_NUMERIC|無 [a]|data|C 資料類型的大小|n/a|  
|SQL_C_BIT|無 [a]|data|1 [b]|n/a|  
|SQL_C_BINARY|*Columnsize* > = 1<br /><br /> *Columnsize* < 1|data<br /><br /> 未定義|@shouldalert<br /><br /> 未定義|n/a<br /><br /> 22003|  
  
 [a] 的值*Columnsize*會忽略這項轉換。 驅動程式假設大小 **TargetValuePtr*是 C 資料類型的大小。  
  
 [b] 這是對應的 C 資料類型的大小。  
  
 當位元的 SQL 資料轉換成 C 字元資料時，可能的值為"0"和"1"。
