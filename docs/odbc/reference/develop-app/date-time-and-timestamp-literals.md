---
title: 日期、 時間和時間戳記常值 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], literals
ms.assetid: 2b42a52a-6353-494c-a179-3a7533cd729f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a13356aae88f332132bc6e8f6d6578971d2be99
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641031"
---
# <a name="date-time-and-timestamp-literals"></a>日期、時間和時間戳記常值
日期、 時間和時間戳記常值的逸出序列是  
  
 **{**  _-type_ **'** _value_ **'}**  
  
 何處*常值型別*其中一個值會列在下表。  
  
|*literal-type*|意義|格式化的*值*|  
|---------------------|-------------|-----------------------|  
|**d**|date|*yyyy*-*mm*-*dd*|  
|**t**|時間 *|*hh*:*mm*:*ss*[1]|  
|**ts**|時間戳記|*yyyy*-*mm*-*dd* *hh*:*mm*:*ss*[.*f...*][1]|  
  
 [SQL_DESC_PRECISION 描述項欄位中包含 1] 的時間戳記常值包含秒數元件間隔中右側位數的數目是小數點的秒數有效位數而定。 (如需詳細資訊，請參閱 < [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。)  
  
 如需日期、 時間和時間戳記逸出序列的詳細資訊，請參閱[日期、 時間和時間戳記逸出序列](../../../odbc/reference/appendixes/date-time-and-timestamp-escape-sequences.md)附錄 c:SQL 文法。  
  
 比方說，這兩個下列的 SQL 陳述式更新的 「 訂單 」 資料表中的銷售單 1023年開啟的日期。 第一個陳述式會使用逸出序列語法。 第二個陳述式會使用 Oracle Rdb 原生語法日期資料行，而且不具互通性。  
  
```  
UPDATE Orders SET OpenDate={d '1995-01-15'} WHERE OrderID=1023  
UPDATE Orders SET OpenDate='15-Jan-1995' WHERE OrderID=1023  
```  
  
 日期、 時間或時間戳記常值的逸出序列也可以放在繫結至日期、 時間或時間戳記參數字元變數。 比方說，下列的程式碼會使用繫結至字元變數的日期參數來更新 「 訂單 」 資料表中的銷售單 1023年開啟日期：  
  
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
  
 若要判斷是否驅動程式支援 ODBC 逸出序列的日期、 時間或時間戳記常值，應用程式會呼叫**SQLGetTypeInfo**。 如果資料來源支援的日期、 時間戳記資料類型，它也必須支援對應的逸出序列。  
  
 資料來源也可以支援的日期時間常值定義在 ANSI SQL-92 規格中，屬於不同的 ODBC 逸出序列的日期、 時間或時間戳記常值。 若要判斷資料來源是否支援 ANSI 常值，應用程式會呼叫**SQLGetInfo** SQL_ANSI_SQL_DATETIME_LITERALS 選項。  
  
 若要判斷驅動程式是否支援 ODBC 逸出序列間隔常值，應用程式會呼叫**SQLGetTypeInfo**。 如果資料來源支援的日期時間間隔資料類型，它也必須支援對應的逸出序列。  
  
 資料來源也可以支援 datetime 常值定義在 ANSI SQL-92 規格中，也就是不同的日期時間間隔常值的 ODBC 逸出序列。 若要判斷資料來源是否支援 ANSI 常值，應用程式會呼叫**SQLGetInfo** SQL_ANSI_SQL_DATETIME_LITERALS 選項。
