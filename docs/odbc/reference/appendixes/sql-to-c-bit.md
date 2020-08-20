---
description: SQL 到 C：位元
title: SQL 到 C：位 |Microsoft Docs
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
ms.openlocfilehash: 15f635ea1c325c60e8ae957aed6f8e1f6b7fe58e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456540"
---
# <a name="sql-to-c-bit"></a>SQL 到 C：位元
Bit ODBC SQL 資料類型的識別碼為：  
  
 SQL_BIT  
  
 下表顯示可轉換成位 SQL 資料的 ODBC C 資料類型。 如需資料表中的資料行和詞彙的說明，請參閱將 [資料從 SQL 轉換成 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR<br /><br /> SQL_C_WCHAR|*BufferLength* > 1<br /><br /> *BufferLength* <= 1|資料<br /><br /> 未定義|1<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE<br /><br /> SQL_C_NUMERIC|無 [a]|資料|C 資料類型的大小|n/a|  
|SQL_C_BIT|無 [a]|資料|1 [b]|n/a|  
|SQL_C_BINARY|*BufferLength* >= 1<br /><br /> *BufferLength* < 1|資料<br /><br /> 未定義|1<br /><br /> 未定義|n/a<br /><br /> 22003|  
  
 [a] 此轉換會忽略 *BufferLength* 的值。 驅動程式會假設 **TargetValuePtr* 的大小是 C 資料類型的大小。  
  
 [b] 這是對應 C 資料類型的大小。  
  
 當位 SQL 資料轉換成字元 C 資料時，可能的值為 "0" 和 "1"。
