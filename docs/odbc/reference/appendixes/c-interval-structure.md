---
title: C 間隔結構 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- interval data type [ODBC], structure
- C data types [ODBC], interval
ms.assetid: 52b42b56-50aa-4ce6-8d79-0963c7a71437
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 02c86ebe24a0e12531e355f95185b01f3089a31b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292150"
---
# <a name="c-interval-structure"></a>C 間隔結構
[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)部分中列出的每個 C 間隔數據類型都使用相同的結構來包含間隔數據。 當調用**SQLFetch、SQLFetch**或**SQLGetData**時,驅動程式將數據返回到SQL_INTERVAL_STRUCT結構中,使用應用程式為 C 數據類型指定**SQLFetchScroll**的值(在調用**SQLBindCol、SQLGetData**或**SQLGetData****SQLBind 參數**)來解釋SQL_INTERVAL_STRUCT的內容,並使用與 C 類型的枚*舉*值填充結構*interval_type*字段。 請注意,驅動程式不讀取*interval_type*欄位以確定間隔的類型;因此,驅動程式不會讀取該欄位。它們檢索SQL_DESC_CONCISE_TYPE描述符欄位的值。 當結構用於參數數據時,驅動程式使用應用程式在 APD SQL_DESC_CONCISE_TYPE欄位中指定的值來解釋SQL_INTERVAL_STRUCT的內容,即使應用程式將*interval_type*欄位的值設置為不同的值也是如此。  
  
 此結構的定義如下:  
  
```  
typedef struct tagSQL_INTERVAL_STRUCT  
{  
   SQLINTERVAL interval_type;   
   SQLSMALLINT interval_sign;  
   union {  
         SQL_YEAR_MONTH_STRUCT   year_month;  
         SQL_DAY_SECOND_STRUCT   day_second;  
         } intval;  
} SQL_INTERVAL_STRUCT;  
typedef enum   
{  
   SQL_IS_YEAR = 1,  
   SQL_IS_MONTH = 2,  
   SQL_IS_DAY = 3,  
   SQL_IS_HOUR = 4,  
   SQL_IS_MINUTE = 5,  
   SQL_IS_SECOND = 6,  
   SQL_IS_YEAR_TO_MONTH = 7,  
   SQL_IS_DAY_TO_HOUR = 8,  
   SQL_IS_DAY_TO_MINUTE = 9,  
   SQL_IS_DAY_TO_SECOND = 10,  
   SQL_IS_HOUR_TO_MINUTE = 11,  
   SQL_IS_HOUR_TO_SECOND = 12,  
   SQL_IS_MINUTE_TO_SECOND = 13  
} SQLINTERVAL;  
  
typedef struct tagSQL_YEAR_MONTH  
{  
   SQLUINTEGER year;  
   SQLUINTEGER month;   
} SQL_YEAR_MONTH_STRUCT;  
  
typedef struct tagSQL_DAY_SECOND  
{  
   SQLUINTEGER day;  
   SQLUINTEGER hour;  
   SQLUINTEGER minute;  
   SQLUINTEGER second;  
   SQLUINTEGER fraction;  
} SQL_DAY_SECOND_STRUCT;  
```  
  
 SQL_INTERVAL_STRUCT*的interval_type*欄位向應用程式指示在聯合中持有哪些結構,以及結構中哪些成員是相關的。 如果間隔前導字段未簽名,*則interval_sign*欄位具有值SQL_FALSE;如果SQL_TRUE,則前導欄位為負。 無論*interval_sign*的值如何,前導欄位本身的值始終沒有符號。 *interval_sign*欄位充當符號位。
