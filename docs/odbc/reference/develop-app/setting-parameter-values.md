---
description: 設定參數值
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: af2992ea66601ec0ae4804e327863e6abb285d73
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476420"
---
# <a name="setting-parameter-values"></a>設定參數值
若要設定參數的值，應用程式只會設定系結至參數的變數值。 如果設定此值，就不重要，只要它是在執行語句之前設定。 應用程式可以在系結變數之前或之後設定值，也可以將值變更為想要的次數。 當語句執行時，驅動程式會直接取出變數目前的值。 當已備妥的語句執行一次以上時，這特別有用。應用程式會在每次執行語句時，設定部分或全部變數的新值。 如需這項操作的範例，請參閱本節稍早的「 [準備執行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)」。  
  
 如果長度/指標緩衝區系結至 **SQLBindParameter**的呼叫中，則在執行語句之前，它必須設定為下列其中一個值：  
  
-   系結變數中資料的位元組長度。 只有當變數是字元或二進位 (*ValueType* 是 SQL_C_CHAR 或 SQL_C_BINARY) 時，驅動程式才會檢查此長度。  
  
-   SQL_NTS。 資料是以 null 結束的字串。  
  
-   SQL_Null_DATA。 資料值為 Null，而驅動程式會忽略系結變數的值。  
  
-   SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 宏的結果。 參數的值會與 **SQLPutData**一起傳送。 如需詳細資訊，請參閱本節稍後的傳送 [長資料](../../../odbc/reference/develop-app/sending-long-data.md)。  
  
 下表顯示系結變數的值，以及應用程式為各種參數值設定的長度/指標緩衝區。  
  
|參數<br /><br /> value|參數<br /><br />  (SQL) <br /><br /> 資料類型|變數 (C) <br /><br /> 資料類型| 中的值<br /><br /> 繫結<br /><br /> 變動| 中的值<br /><br /> 長度/指標<br /><br /> 緩衝區 [d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC\0 [a]|SQL_NTS 或3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|10 \ 0 [a]|SQL_NTS 或2|  
|下午1點|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13、0、0 [b]|--|  
|下午1點|SQL_TYPE_TIME|SQL_C_CHAR|{t ' 13：00： 00 '} \ 0 [a]，[c]|SQL_NTS 或14|  
|NULL|SQL_SMALLINT|SQL_C_SSHORT|--|SQL_Null_DATA|  
  
 [a] "\ 0" 代表 null 終止字元。 只有當長度/指標緩衝區中的值 SQL_NTS 時，才需要 null 終止字元。  
  
 [b] 這份清單中的數位是儲存在 TIME_STRUCT 結構之欄位中的數位。  
  
 [c] 字串使用 ODBC date escape 子句。 如需詳細資訊，請參閱 [日期、時間和時間戳記常](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)值。  
  
 [d] 驅動程式一律必須檢查此值，以查看它是否為特殊值，例如 SQL_Null_DATA。  
  
 驅動程式在執行時間使用參數值的方式取決於驅動程式。 必要時，驅動程式會將值從系結變數的 C 資料類型和位元組長度轉換成參數的 SQL 資料類型、有效位數和小數位數。 在大部分的情況下，驅動程式會接著將值傳送至資料來源。 在某些情況下，它會將值格式化為文字，並將其插入至 SQL 語句，然後再將語句傳送到資料來源。
