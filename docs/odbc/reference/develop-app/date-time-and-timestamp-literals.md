---
title: 日期、時間和時間戳文本 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288294"
---
# <a name="date-time-and-timestamp-literals"></a>日期、時間和時間戳記常值
日期、時間與時間戳文字的逸出序列是  
  
 **【**  _- 類型_ **'** _值_ **']**  
  
 *其中文本類型*是下表中列出的值之一。  
  
|*字型態*|意義|*價值*格式|  
|---------------------|-------------|-----------------------|  
|**D**|Date|*yyyy*-*mm*-*dd*|  
|**t**|時間*|*hh*:*mm*:*ss*[1]|  
|**Ts**|時間戳記|*yyyymm*-*mm*-*dd* *hh*:*mm*:*ss*_..*f...*[1]|  
  
 [1] 時間或時間戳間隔文本中包含秒分的十進位點右側的位數取決於秒精度,如SQL_DESC_PRECISION描述符欄位中所包含的。 (有關詳細資訊,請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。  
  
 有關日期、時間和時間戳轉義序列的詳細資訊,請參閱附錄 C 中[的日期、時間和時間戳轉義序列](../../../odbc/reference/appendixes/date-time-and-timestamp-escape-sequences.md):SQL 語法。  
  
 例如,以下兩個 SQL 語句都會更新訂單表中銷售訂單 1023 的打開日期。 第一個語句使用轉義序列語法。 第二個語句對 DATE 列使用 Oracle Rdb 本機語法,並且不可互通。  
  
```  
UPDATE Orders SET OpenDate={d '1995-01-15'} WHERE OrderID=1023  
UPDATE Orders SET OpenDate='15-Jan-1995' WHERE OrderID=1023  
```  
  
 日期、時間或時間戳文本的轉義序列也可以放置在綁定到日期、時間或時間戳參數的字元變數中。 例如,以下代碼使用繫結到字元變數的日期參數來更新訂單表中銷售訂單 1023 的開啟日期:  
  
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
  
 但是,將參數直接綁定到日期結構通常更有效:  
  
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
  
 要確定驅動程式是否支援日期、時間或時間戳文字的 ODBC 轉義序列,應用程式呼叫**SQLGetTypeInfo**。 如果數據源支援日期、時間或時間戳數據類型,則它還必須支持相應的轉義序列。  
  
 數據來源還可以支援 ANSI SQL-92 規範中定義的日期時間文本,這與日期、時間或時間戳文本的 ODBC 轉義序列不同。 要確定資料來源是否支援 ANSI 文字,應用程式使用SQL_ANSI_SQL_DATETIME_LITERALS選項呼叫**SQLGetInfo。**  
  
 要確定驅動程式是否支援間隔文字的 ODBC 逸出序列,應用程式呼叫**SQLGetTypeInfo**。 如果數據源支援日期時間間隔數據類型,則還必須支持相應的轉義序列。  
  
 數據來源還可以支援 ANSI SQL-92 規範中定義的日期時間文本,這與日期時間間隔文本的 ODBC 轉義序列不同。 要確定資料來源是否支援 ANSI 文字,應用程式使用SQL_ANSI_SQL_DATETIME_LITERALS選項呼叫**SQLGetInfo。**
