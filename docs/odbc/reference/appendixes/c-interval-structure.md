---
title: C 間隔結構 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3387b4fa48eb1a04102daadcc08f971765d7ca2b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037778"
---
# <a name="c-interval-structure"></a>C 間隔結構
[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)一節中所列的每個 c 間隔資料類型，都會使用相同的結構來包含間隔資料。 當呼叫**SQLFetch**、 **SQLFetchScroll**或**SQLGetData**時，驅動程式會將資料傳回 SQL_INTERVAL_STRUCT 結構、使用應用程式針對 c 資料類型（在**SQLBindCol**、 **SQLGetData**或**SQLBindParameter**的呼叫中）所指定的值來解讀 SQL_INTERVAL_STRUCT 的內容，並使用對應至 c 類型的*列舉*值來填入結構的*interval_type*欄位。 請注意，驅動程式不會讀取 [ *interval_type* ] 欄位來判斷間隔的類型;它們會抓取 [SQL_DESC_CONCISE_TYPE 描述項] 欄位的值。 當此結構用於參數資料時，驅動程式會使用 APD 之 [SQL_DESC_CONCISE_TYPE] 欄位中的應用程式所指定的值來解讀 SQL_INTERVAL_STRUCT 的內容，即使應用程式將*interval_type*欄位的值設定為不同的值亦然。  
  
 此結構定義如下：  
  
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
  
 SQL_INTERVAL_STRUCT 的 [ *interval_type* ] 欄位會向應用程式指出在聯集中保留的結構，以及結構的哪些成員相關。 如果間隔前置欄位不帶正負號， *interval_sign*欄位會有 SQL_FALSE 的值;如果 SQL_TRUE，則前置欄位為負數。 不論*interval_sign*的值為何，前置欄位本身的值永遠都是不帶正負號的。 [ *Interval_sign* ] 欄位會作為符號位。
