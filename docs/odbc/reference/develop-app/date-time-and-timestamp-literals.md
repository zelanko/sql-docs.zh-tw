---
title: "日期、 時間和時間戳記常值 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: escape sequences [ODBC], literals
ms.assetid: 2b42a52a-6353-494c-a179-3a7533cd729f
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8aa042321602332ea016b88c69332dd67a256044
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="date-time-and-timestamp-literals"></a>日期、 時間和時間戳記常值
日期、 時間和時間戳記常值的逸出序列是  
  
 **{***-類型* **'** *值* **'}**   
  
 其中*常值型別*其中一個值列於下表。  
  
|*常值型別*|意義|格式化的*值*|  
|---------------------|-------------|-----------------------|  
|**d**|日期|*yyyy*-*公釐*-*dd*|  
|**t**|時間 *|*hh*:*公釐*:*ss*[1]|  
|**ts**|時間戳記|*yyyy*-*公釐*-*dd* *hh*:*公釐*:*ss*[.*f...*] [1]|  
  
 [SQL_DESC_PRECISION 描述項欄位中包含 1] 在時間戳記的間隔時間常值包含秒元件的小數點右邊位數的數目是秒數有效位數而定。 (如需詳細資訊，請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。)  
  
 如需有關日期、 時間和時間戳記逸出序列的詳細資訊，請參閱[日期、 時間和時間戳記逸出序列](../../../odbc/reference/appendixes/date-time-and-timestamp-escape-sequences.md)附錄 c: SQL 文法中。  
  
 比方說，這兩個下列的 SQL 陳述式會更新銷售訂單 1023 Orders 資料表中的開啟日期。 第一個陳述式會使用逸出序列語法。 第二個陳述式會使用 Oracle Rdb 原生語法日期資料行，而且不互通。  
  
```  
UPDATE Orders SET OpenDate={d '1995-01-15'} WHERE OrderID=1023  
UPDATE Orders SET OpenDate='15-Jan-1995' WHERE OrderID=1023  
```  
  
 日期、 時間或時間戳記常值的逸出序列也可以放在繫結至日期、 時間或時間戳記參數字元變數中。 比方說，下列程式碼會使用日期參數繫結至字元變數更新銷售訂單 1023 Orders 資料表中的開啟日期：  
  
```  
SQLCHAR      OpenDate[56]; // The size of a date literal is 55.  
SQLINTEGER   OpenDateLenOrInd = SQL_NTS;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_TYPE_DATE, 0, 0,  
                  OpenDate, sizeof(OpenDate), &OpenDateLenOrInd);  
  
// Place the date in the OpenDate variable. In addition to the escape  
// sequence shown, it would also be possible to use either of the  
// strings "{d '1995-01-15'}" and "15-Jan-1995", although the latter  
// is data source-specific.  
strcpy_s( (char*) OpenDate, _countof(OpenDate), "{d '1995-01-15'}");  
  
// Execute the statement.  
SQLExecDirect(hstmt, "UPDATE Orders SET OpenDate=? WHERE OrderID = 1023", SQL_NTS);  
```  
  
 不過，它會直接繫結參數的日期結構通常更有效率：  
  
```  
SQL_DATE_STRUCT   OpenDate;  
SQLINTEGER        OpenDateInd = 0;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &OpenDate, 0, &OpenDateLen);  
  
// Place the date in the dsOpenDate structure.  
OpenDate.year = 1995;  
OpenDate.month = 1;  
OpenDate.day = 15;  
  
// Execute the statement.  
SQLExecDirect(hstmt, "UPDATE Employee SET OpenDate=? WHERE OrderID = 1023", SQL_NTS);  
```  
  
 若要判斷是否將驅動程式支援 ODBC 逸出序列的日期、 時間或時間戳記常值，應用程式呼叫**SQLGetTypeInfo**。 如果資料來源支援的日期、 時間戳記資料類型，它也必須支援對應的逸出序列。  
  
 資料來源也支援日期時間常值定義在 ANSI sql-92 規格中，也就是不同的 ODBC 逸出序列的日期、 時間或時間戳記常值。 若要判斷資料來源是否支援 ANSI 常值，應用程式呼叫**SQLGetInfo** SQL_ANSI_SQL_DATETIME_LITERALS 選項。  
  
 若要判斷驅動程式是否支援 ODBC 逸出序列間隔常值，應用程式呼叫**SQLGetTypeInfo**。 如果資料來源支援的日期時間間隔資料類型，它也必須支援對應的逸出序列。  
  
 資料來源也支援日期時間常值定義在 ANSI sql-92 規格中，也就是不同的日期時間間隔的常值的 ODBC 逸出序列。 若要判斷資料來源是否支援 ANSI 常值，應用程式呼叫**SQLGetInfo** SQL_ANSI_SQL_DATETIME_LITERALS 選項。
