---
title: SQL 到 C：時間戳記 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- timestamp data type [ODBC]
- converting data from SQL to C types [ODBC], timestamp
- data conversions from SQL to C types [ODBC], timestamp
ms.assetid: 6a0617cf-d8c0-4316-8bb4-e6ddb45d7bf1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 552bab585e4480fd922c9b9a6b112830f5c11ad9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81296348"
---
# <a name="sql-to-c-timestamp"></a>SQL 到 C：時間戳記

時間戳記 ODBC SQL 資料類型的識別碼如下：

- SQL_TYPE_TIMESTAMP  

下表顯示可以轉換時間戳記 SQL 資料的 ODBC C 資料類型。 如需資料表中的資料行和詞彙的說明，請參閱將[資料從 SQL 轉換成 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  

|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > 字元位元組長度<br /><br /> 20 <= *BufferLength* <= 字元位元組長度<br /><br /> *BufferLength* < 20|資料<br /><br /> 截斷的資料 [b]<br /><br /> 未定義|資料長度（以位元組為單位）<br /><br /> 資料長度（以位元組為單位）<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > 字元長度<br /><br /> 20 <= *BufferLength* <= 字元長度<br /><br /> *BufferLength* < 20|資料<br /><br /> 截斷的資料 [b]<br /><br /> 未定義|資料長度（以字元為單位）<br /><br /> 資料長度（以字元為單位）<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|資料 <的位元組長度 = *BufferLength*<br /><br /> 資料 > *BufferLength*的位元組長度|資料<br /><br /> 未定義|資料長度（以位元組為單位）<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_TYPE_DATE|時間戳記的時間部分為零 [a]<br /><br /> Timestamp 的時間部分是非零的 [a]|資料<br /><br /> 截斷的資料 [c]|6 [f]<br /><br /> 6 [f]|n/a<br /><br /> 01S07|  
|SQL_C_TYPE_TIME|時間戳記的小數秒部分為零 [a]<br /><br /> 時間戳記的小數秒部分是非零的 [a]|資料 [d]<br /><br /> 截斷的資料 [d]，[e]|6 [f]<br /><br /> 6 [f]|n/a<br /><br /> 01S07|  
|SQL_C_TYPE_TIMESTAMP|時間戳記的小數秒部分不會截斷 [a]<br /><br /> 時間戳記的小數秒部分已截斷 [a]|資料 [e]<br /><br /> 截斷的資料 [e]|16 [f]<br /><br /> 16 [f]|n/a<br /><br /> 01S07|  

 [a] 這項轉換會忽略*BufferLength*的值。 驅動程式假設 **TargetValuePtr*的大小是 C 資料類型的大小。  
  
 [b] 時間戳記的小數秒數已截斷。  
  
 [c] 時間戳記的時間部分會被截斷。  
  
 [d] 已忽略時間戳記的日期部分。  
  
 [e] 時間戳記的小數秒部分已截斷。  
  
 [f] 這是對應 C 資料類型的大小。  

當時間戳 SQL 資料轉換成字元 C 資料時，產生的字串會是 "*yyyy*-*mm*-*dd* *hh*：*mm*：*ss*[。*f ...*] "格式，最多可以使用9位數的小數秒數。 此格式不會受到 Windows®國家（地區）設定的影響。 （小數點和小數秒除外，不論 timestamp SQL 資料類型的有效位數為何，都必須使用整個格式）。
