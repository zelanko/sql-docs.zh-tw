---
title: "設定參數值 |Microsoft 文件"
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
helpviewer_keywords: parameter values [ODBC]
ms.assetid: 13e5da79-b60c-48d0-b467-773f481ef2a4
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 726af8b2a7b4e9f0b630c95c45f512201fa1cf3a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="setting-parameter-values"></a>設定參數值
若要設定參數的值，應用程式只會設定繫結至參數之變數的值。 它並不重要時設定此值，只要執行陳述式之前，它會設定。 應用程式可以設定的值之前或之後繫結變數，並可能會變更的值，它想要的次數。 當執行陳述式時，驅動程式只會擷取變數的目前值。 一次以上。 執行已備妥的陳述式時，這會特別有用應用程式會設定新值的部分或所有變數的每次執行陳述式時。 這個範例，請參閱[已備妥執行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)稍早在本章節中。  
  
 如果在呼叫繫結長度/指標緩衝區**SQLBindParameter**，它必須設定為下列值的其中一個陳述式之前：  
  
-   繫結變數中的資料位元組的長度。 驅動程式會檢查此長度，只有當變數是字元或二進位 (*ValueType* SQL_C_CHAR 或 SQL_C_BINARY)。  
  
-   SQL_NTS。 資料是以 null 結束的字串。  
  
-   SQL_NULL_DATA。 資料值為 NULL，以及驅動程式會忽略繫結變數的值。  
  
-   SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 巨集的結果。 參數的值是與傳送**SQLPutData**。 如需詳細資訊，請參閱[傳送長資料](../../../odbc/reference/develop-app/sending-long-data.md)稍後這一節。  
  
 下表顯示繫結的變數和應用程式會設定各種不同的參數值的長度/指標緩衝區的值。  
  
|參數<br /><br /> value|參數<br /><br /> (SQL)<br /><br /> 資料類型|Variable (C)<br /><br /> 資料類型|中的值<br /><br /> 繫結<br /><br /> 變數|中的值<br /><br /> 長度/指標<br /><br /> 緩衝區 [d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC\0 [a]|SQL_NTS 或 3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|10\0 [a]|SQL_NTS 或 2|  
|下午 1|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13,0,0 [b]|--|  
|下午 1|SQL_TYPE_TIME|SQL_C_CHAR|{t ' 13: 00:00'} \0 [a]、 [c]|SQL_NTS 或是 14|  
|NULL|SQL_SMALLINT|SQL_C_SSHORT|--|SQL_NULL_DATA|  
  
 [a]"\0"表示 null 結束字元。 只有當長度/指標緩衝區中的值是 sql_nts; 需要的 null 結束的字元。  
  
 [這份清單中的 b] 的數字為 TIME_STRUCT 結構的欄位中儲存的數字。  
  
 [使用 ODBC 日期逸出子句 c] 的字串。 如需詳細資訊，請參閱[日期、 時間和時間戳記常值](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)。  
  
 [d] 的驅動程式必須一律會檢查此值，以查看其是否為特殊值，例如 SQL_NULL_DATA。  
  
 驅動程式未使用的參數值在執行階段會驅動程式而異。 必要時，驅動程式將值從繫結變數的 C 資料類型與位元組長度 SQL 資料類型、 有效位數和小數位數參數。 在大部分情況下，驅動程式再將值傳送至資料來源。 在某些情況下，它會格式化為文字值，並將它插入之前的陳述式傳送到資料來源的 SQL 陳述式。
