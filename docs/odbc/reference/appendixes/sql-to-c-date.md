---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d282798a31ac9059ed3c1901ea01f1f3104f09c7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68056877"
---
# <a name="sql-to-c-date"></a>SQL 到 C：日期
Date ODBC SQL 資料類型的識別碼為：  
  
 SQL_TYPE_DATE  
  
 下表顯示 SQL 資料轉換日期的 ODBC C 資料類型。 如需資料表中的資料行和詞彙的說明，請參閱將[資料從 SQL 轉換成 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > 字元位元組長度<br /><br /> 11 <= *BufferLength* <= 字元位元組長度<br /><br /> *BufferLength* < 11|資料<br /><br /> 截斷的資料<br /><br /> 未定義|10<br /><br /> 資料長度（以位元組為單位）<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > 字元長度<br /><br /> 11 <= *BufferLength* <= 字元長度<br /><br /> *BufferLength* < 11|資料<br /><br /> 截斷的資料<br /><br /> 未定義|10<br /><br /> 資料長度（以字元為單位）<br /><br /> 未定義|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|資料 <的位元組長度 = *BufferLength*<br /><br /> 資料 > *BufferLength*的位元組長度|資料<br /><br /> 未定義|資料長度（以位元組為單位）<br /><br /> 未定義|n/a<br /><br /> 22003|  
|SQL_C_TYPE_DATE|無 [a]|資料|6 [c]|n/a|  
|SQL_C_TYPE_TIMESTAMP|無 [a]|資料 [b]|16 [c]|n/a|  
  
 [a] 這項轉換會忽略*BufferLength*的值。 驅動程式假設 **TargetValuePtr*的大小是 C 資料類型的大小。  
  
 [b] 時間戳記結構的時間欄位設定為零。  
  
 [c] 這是對應 C 資料類型的大小。  
  
 當日期 SQL 資料轉換成字元 C 資料時，產生的字串會採用 "*yyyy*-*mm*-*dd*" 格式。 此格式不會受到 Windows®國家（地區）設定的影響。
