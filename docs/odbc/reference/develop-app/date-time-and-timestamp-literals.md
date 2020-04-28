---
title: 日期、時間和時間戳記常值 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d899938be4689daab50a773f189219a797794006
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288294"
---
# <a name="date-time-and-timestamp-literals"></a>日期、時間和時間戳記常值
日期、時間和時間戳記常值的轉義順序為  
  
 **{**  _-類型_ **'** _value_ **'}**  
  
 其中， *literal 類型*是下表所列的其中一個值。  
  
|*常數值型別*|意義|*值*的格式|  
|---------------------|-------------|-----------------------|  
|**d**|Date|*yyyy*-*mm*mm-*dd*|  
|**t**|階段|*hh*：*mm*：*ss*[1]|  
|**ts**|時間戳記|*yyyy*-*mm*mm-*dd* *hh*：*mm*：*ss*[。*f ...*]sha-1|  
  
 [1] 包含在 [SQL_DESC_PRECISION 描述項] 欄位中的時間或時間戳記間隔常值中，小數點右邊的位數，以秒為單位。 （如需詳細資訊，請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)）。  
  
 如需日期、時間和時間戳記逸出序列的詳細資訊，請參閱附錄 C： SQL 文法中的[日期、時間和時間戳記逸出序列](../../../odbc/reference/appendixes/date-time-and-timestamp-escape-sequences.md)。  
  
 例如，下列兩個 SQL 語句都會在 Orders 資料表中更新銷售訂單1023的開啟日期。 第一個語句使用 escape 序列語法。 第二個語句使用日期資料行的 Oracle Rdb 原生語法，而且無法互通。  
  
```  
UPDATE Orders SET OpenDate={d '1995-01-15'} WHERE OrderID=1023  
UPDATE Orders SET OpenDate='15-Jan-1995' WHERE OrderID=1023  
```  
  
 日期、時間或時間戳記常值的轉義順序也可以放在系結至日期、時間或時間戳記參數的字元變數中。 例如，下列程式碼會使用系結至字元變數的日期參數，在 Orders 資料表中更新銷售訂單1023的開啟日期：  
  
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
  
 不過，將參數直接系結至日期結構通常會更有效率：  
  
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
  
 若要判斷驅動程式是否支援日期、時間或時間戳記常值的 ODBC 轉義順序，應用程式會呼叫**SQLGetTypeInfo**。 如果資料來源支援日期、時間或時間戳記資料類型，它也必須支援對應的逸出序列。  
  
 資料來源也可以支援 ANSI SQL-92 規格中所定義的日期時間常值，這不同于日期、時間或時間戳記常值的 ODBC 逸出序列。 為了判斷資料來源是否支援 ANSI 常值，應用程式會使用 SQL_ANSI_SQL_DATETIME_LITERALS 選項來呼叫**SQLGetInfo** 。  
  
 若要判斷驅動程式是否支援間隔常值的 ODBC 逸出序列，應用程式會呼叫**SQLGetTypeInfo**。 如果資料來源支援 datetime interval 資料類型，它也必須支援對應的逸出序列。  
  
 資料來源也可以支援 ANSI SQL-92 規格中所定義的日期時間常值，這與日期時間間隔常值的 ODBC 轉義順序不同。 為了判斷資料來源是否支援 ANSI 常值，應用程式會使用 SQL_ANSI_SQL_DATETIME_LITERALS 選項來呼叫**SQLGetInfo** 。
