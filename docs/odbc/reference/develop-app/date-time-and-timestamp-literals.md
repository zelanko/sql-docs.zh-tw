---
description: 日期、時間和時間戳記常值
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
ms.openlocfilehash: 10fb362a8ab61595a9b7205492de9c1115ae7013
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424780"
---
# <a name="date-time-and-timestamp-literals"></a>日期、時間和時間戳記常值
日期、時間和時間戳記常值的 escape 序列為  
  
 **{**  _-type_ **'** _value_ **'}**  
  
 其中， *常* 值型別是下表所列的其中一個值。  
  
|*常數值型別*|意義|*值*的格式|  
|---------------------|-------------|-----------------------|  
|**d**|Date|*yyyy* -*mm* -*dd*|  
|**10gbase-t**|時間|*hh*：*mm*：*ss*[1]|  
|**Ts**|時間戳記|*yyyy* -*mm* -*dd* *hh*：*mm*：*ss*[.*f ...*]單|  
  
 [1] 時間或時間戳記間隔常值中包含秒陣列件之小數點右邊的位數，取決於 SQL_DESC_PRECISION 描述項欄位中包含的秒數精確度。  (需詳細資訊，請參閱 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 )   
  
 如需日期、時間和時間戳記轉義順序的詳細資訊，請參閱附錄 C： SQL 文法中的 [日期、時間和時間戳記逸出序列](../../../odbc/reference/appendixes/date-time-and-timestamp-escape-sequences.md) 。  
  
 例如，下列兩個 SQL 語句都會更新 Orders 資料表中銷售訂單1023的開啟日期。 第一個語句使用 escape sequence 語法。 第二個語句會針對日期資料行使用 Oracle Rdb 原生語法，而且無法互通。  
  
```  
UPDATE Orders SET OpenDate={d '1995-01-15'} WHERE OrderID=1023  
UPDATE Orders SET OpenDate='15-Jan-1995' WHERE OrderID=1023  
```  
  
 日期、時間或時間戳記常值的 escape 序列也可以放在系結至日期、時間或時間戳記參數的字元變數中。 例如，下列程式碼會使用系結至字元變數的 date 參數來更新 Orders 資料表中銷售訂單1023的開啟日期：  
  
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
  
 為了判斷驅動程式是否支援日期、時間或時間戳記常值的 ODBC escape 序列，應用程式會呼叫 **SQLGetTypeInfo**。 如果資料來源支援日期、時間或時間戳記資料類型，則它也必須支援對應的 escape 序列。  
  
 資料來源也可以支援 ANSI SQL-92 規格中定義的日期時間常值，這與日期、時間或時間戳記常值的 ODBC 轉義順序不同。 為了判斷資料來源是否支援 ANSI 常值，應用程式會使用 SQL_ANSI_SQL_DATETIME_LITERALS 選項來呼叫 **SQLGetInfo** 。  
  
 為了判斷驅動程式是否支援間隔常值的 ODBC escape 序列，應用程式會呼叫 **SQLGetTypeInfo**。 如果資料來源支援 datetime interval 資料類型，則它也必須支援對應的 escape 序列。  
  
 資料來源也可以支援 ANSI SQL-92 規格中定義的日期時間常值，這與日期時間間隔常值的 ODBC 轉義順序不同。 為了判斷資料來源是否支援 ANSI 常值，應用程式會使用 SQL_ANSI_SQL_DATETIME_LITERALS 選項來呼叫 **SQLGetInfo** 。
