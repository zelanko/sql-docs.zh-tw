---
title: SQL 轉換為 C：GUID | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], GUID
- data conversions from SQL to C types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: cf56c684-c261-4b89-994a-db14ab2241d6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1a2ed3cffcb196cb09841df3b54fbfab53e22477
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056870"
---
# <a name="sql-to-c-guid"></a>SQL 轉換為 C：GUID
GUID ODBC SQL 資料類型的識別項是：  
  
 SQL_GUID  
  
 下表顯示 ODBC C 資料類型可能會轉換 GUID SQL 資料。 如需資料行和資料表中的詞彙說明，請參閱 <<c0> [ 轉換將資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > 字元位元組長度|Data|36|n/a|  
||*BufferLength* < 37|未定義|未定義|22003|  
|SQL_C_WCHAR|*BufferLength* > 字元長度|Data|36|n/a|  
||*BufferLength* < 37|未定義|未定義|22003|  
|SQL_C_BINARY|資料的位元組長度\< =  *Columnsize*|Data|以位元組為單位的資料長度|n/a|  
||資料的位元組長度 > *Columnsize*|未定義|未定義|22003|  
|SQL_C_GUID|無 [a]|Data|16[b]|n/a|  
  
 [a] 的值*Columnsize*會忽略這項轉換。 驅動程式會假設大小 **TargetValuePtr*是 C 資料類型的大小。  
  
 [b] 這是對應的 C 資料類型的大小。
