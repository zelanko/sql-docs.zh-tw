---
title: "C 間隔結構 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], interval data types
- interval data type [ODBC], structure
- C data types [ODBC], interval
ms.assetid: 52b42b56-50aa-4ce6-8d79-0963c7a71437
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 146e16608f0f2f790bf49a84de2ef4610df33d0f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="c-interval-structure"></a>C 間隔結構
每個 C 間隔資料類型中所列[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)區段包含間隔資料使用相同的結構。 當**SQLFetch**， **SQLFetchScroll**，或**SQLGetData**是呼叫，此驅動程式傳回的資料到 SQL_INTERVAL_STRUCT 結構，會使用所指定的值應用程式的 C 資料類型 (在呼叫**SQLBindCol**， **SQLGetData**，或**SQLBindParameter**) 來解譯 SQL_INTERVAL_STRUCT 的內容並於其中填入*interval_type*欄位具有結構*列舉*對應到 C 類型的值。 請注意，驅動程式不會讀取*interval_type*欄位來決定的間隔類型; 它們會擷取 SQL_DESC_CONCISE_TYPE 描述項欄位的值。 參數資料的使用結構時，驅動程式會使用 APD SQL_DESC_CONCISE_TYPE 欄位中的應用程式所指定的值解譯內容 SQL_INTERVAL_STRUCT，即使應用程式設定的值*interval_type*欄位設為不同的值。  
  
 這個結構被定義，如下所示：  
  
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
  
 *Interval_type* SQL_INTERVAL_STRUCT 欄位指出應用程式等位中保留哪些結構和結構的成員也會相關。 *Interval_sign*欄位值 SQL_FALSE 如果間隔的開頭欄位是不帶正負號; 如果這是 SQL_TRUE，[前置] 欄位是負數。 前置欄位本身中的值一律是不帶正負號的值為何*interval_sign*。 *Interval_sign*欄位做為正負號位元。

