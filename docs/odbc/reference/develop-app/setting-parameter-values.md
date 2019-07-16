---
title: 設定參數值 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- parameter values [ODBC]
ms.assetid: 13e5da79-b60c-48d0-b467-773f481ef2a4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0bb1115290f53c19fae1aacb0a976cfcef63e086
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094228"
---
# <a name="setting-parameter-values"></a>設定參數值
若要設定參數的值，應用程式只會設定變數繫結至參數的值。 它並不重要設定此值時，只要執行陳述式之前，它會設定。 應用程式可以設定的值之前或之後繫結變數，而且可以變更它想要的次數的值。 當執行陳述式時，驅動程式就只會擷取變數的目前值。 備妥的陳述式執行一次以上; 時，這會特別有用應用程式設定新值的部分或所有變數的每次執行陳述式時。 這個範例，請參閱[已備妥執行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)稍早的這一節。  
  
 如果長度/指標緩衝區已繫結，在呼叫**SQLBindParameter**，它必須先設定下列值來執行陳述式：  
  
-   繫結變數中的資料位元組長度。 驅動程式的變數是字元或二進位時，才會檢查這個長度 (*ValueType*為 SQL_C_CHAR 或 SQL_C_BINARY)。  
  
-   SQL_NTS. 資料是以 null 結束的字串。  
  
-   SQL_NULL_DATA. 資料值是 NULL，以及驅動程式會忽略的繫結的變數值。  
  
-   SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 巨集的結果。 參數的值是與傳送**SQLPutData**。 如需詳細資訊，請參閱 <<c0> [ 傳送長資料](../../../odbc/reference/develop-app/sending-long-data.md)稍後這一節。  
  
 下表顯示繫結的變數和應用程式會設定各種不同的參數值之長度/指標緩衝區的值。  
  
|參數<br /><br /> value|參數<br /><br /> (SQL)<br /><br /> 資料類型|Variable (C)<br /><br /> 資料類型|中的值<br /><br /> 繫結<br /><br /> 變數|中的值<br /><br /> 長度/指標<br /><br /> 緩衝區 [d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC\0[a]|SQL_NTS 或 3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|10\0[a]|SQL_NTS 或 2|  
|下午 1 點|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13,0,0 [b]|--|  
|下午 1 點|SQL_TYPE_TIME|SQL_C_CHAR|{t ' 13: 00:00'} \0 [a]、 [c]|SQL_NTS 或 14|  
|NULL|SQL_SMALLINT|SQL_C_SSHORT|--|SQL_NULL_DATA|  
  
 [a]"\0 」 表示 null 結束字元。 長度/指標緩衝區中的值是 sql_nts; 時，才需要 null 結束字元。  
  
 [這份清單中的 b] 的數字是儲存在 TIME_STRUCT 結構的欄位中的數字。  
  
 [c] 的字串會使用 ODBC 日期逸出子句。 如需詳細資訊，請參閱 <<c0> [ 日期、 時間和時間戳記常值](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)。  
  
 [d] 的驅動程式必須一律會檢查此值，以查看其是否為特殊值，例如 SQL_NULL_DATA。  
  
 驅動程式未使用的參數值在執行階段會驅動程式而異。 如有必要，驅動程式會將值從繫結的變數的 C 資料類型和位元組長度轉換為 SQL 資料類型、 有效位數和小數位數參數中。 在大部分情況下，驅動程式會接著將值傳送至資料來源。 在某些情況下，它會格式化為文字值，並將其插入至 SQL 陳述式之前的陳述式傳送到資料來源。
