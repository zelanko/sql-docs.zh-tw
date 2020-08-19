---
description: SQL 到 C：時間
title: SQL 到 C： Time |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], time
- time data type [ODBC]
- data conversions from SQL to C types [ODBC], time
ms.assetid: 6dc59973-7bb5-40f1-87c8-5bf68b3bf2ee
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0516cc970238e9535c340c14282be1640ba78513
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429550"
---
# <a name="sql-to-c-time"></a>SQL 到 C：時間
Time ODBC SQL 資料類型的識別碼為：  
  
 SQL_TYPE_TIME  
  
 下表顯示 ODBC C 資料類型，這是 SQL 資料可能轉換的時間。 如需資料表中的資料行和詞彙的說明，請參閱將 [資料從 SQL 轉換成 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > 字元位元組長度<br /><br /> *9*  <= *BufferLength* <= 字元位元組長度<br /><br /> *BufferLength* < 9|資料<br /><br /> 截斷的資料 [a]<br /><br /> 未定義|資料的長度（以位元組為單位）<br /><br /> 資料的長度（以位元組為單位）<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > 字元長度<br /><br /> *9*  <= *BufferLength* <= 字元長度<br /><br /> *BufferLength* < 9|資料<br /><br /> 截斷的資料 [a]<br /><br /> 未定義|資料的長度（以字元為單位）<br /><br /> 資料的長度（以字元為單位）<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|資料 <的位元組長度 = *BufferLength*<br /><br /> 資料 > *BufferLength*的位元組長度|資料<br /><br /> 未定義|資料的長度（以位元組為單位）<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_TYPE_TIME|無 [b]|資料|6 [d]|n/a|  
|SQL_C_TYPE_TIMESTAMP|無 [b]|資料 [c]|16 [d]|n/a|  
  
 [a] 截斷時間的小數秒數。  
  
 [b] 此轉換會忽略 *BufferLength* 的值。 驅動程式會假設 **TargetValuePtr* 的大小是 C 資料類型的大小。  
  
 [c] 時間戳記結構的日期欄位設定為目前的日期，且時間戳記結構的小數秒欄位設定為零。  
  
 [d] 這是對應 C 資料類型的大小。  
  
 當時間 SQL 資料轉換成字元 C 資料時，產生的字串會是 "*hh*：*mm*：*ss*" 格式。 此格式不受 Windows® country 設定影響。
