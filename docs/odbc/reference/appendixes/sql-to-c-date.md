---
description: SQL 到 C：日期
title: SQL 到 C：日期 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], date
- date data type [ODBC]
- data conversions from SQL to C types [ODBC], date
ms.assetid: 703c7960-9cf4-4d7a-9920-53b29c184f97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5bab301c7a4bc55289006df1c9df5498629f317
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456514"
---
# <a name="sql-to-c-date"></a>SQL 到 C：日期
日期 ODBC SQL 資料類型的識別碼為：  
  
 SQL_TYPE_DATE  
  
 下表顯示 SQL 資料可能轉換日期的 ODBC C 資料類型。 如需資料表中的資料行和詞彙的說明，請參閱將 [資料從 SQL 轉換成 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > 字元位元組長度<br /><br /> 11 <= *BufferLength* <= 字元位元組長度<br /><br /> *BufferLength* < 11|資料<br /><br /> 截斷的資料<br /><br /> 未定義|10<br /><br /> 資料的長度（以位元組為單位）<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > 字元長度<br /><br /> 11 <= *BufferLength* <= 字元長度<br /><br /> *BufferLength* < 11|資料<br /><br /> 截斷的資料<br /><br /> 未定義|10<br /><br /> 資料的長度（以字元為單位）<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|資料 <的位元組長度 = *BufferLength*<br /><br /> 資料 > *BufferLength*的位元組長度|資料<br /><br /> 未定義|資料的長度（以位元組為單位）<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_TYPE_DATE|無 [a]|資料|6 [c]|n/a|  
|SQL_C_TYPE_TIMESTAMP|無 [a]|資料 [b]|16 [c]|n/a|  
  
 [a] 此轉換會忽略 *BufferLength* 的值。 驅動程式會假設 **TargetValuePtr* 的大小是 C 資料類型的大小。  
  
 [b] 時間戳記結構的時間欄位會設定為零。  
  
 [c] 這是對應 C 資料類型的大小。  
  
 當 SQL 資料的日期轉換成字元 C 資料時，產生的字串會是 "*yyyy* - *mm* - *dd*" 格式。 此格式不受 Windows® country 設定影響。
