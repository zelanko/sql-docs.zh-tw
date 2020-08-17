---
description: 時間、日期和間隔函數
title: 時間、日期和間隔函數 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], time functions
- functions [ODBC], date functions
- interval functions [ODBC]
- functions [ODBC], interval functions
- time functions [ODBC]
- date functions [ODBC]
ms.assetid: bdf054a0-7aba-4e99-a34a-799917376fd5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dcbdf9f40a9cd1f1296920e3d2ea71fcb5ce6b39
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386374"
---
# <a name="time-date-and-interval-functions"></a>時間、日期和間隔函數
下表列出 ODBC 純量函數集內所包含的時間和日期函數。 應用程式可以藉由呼叫 SQL_TIMEDATE_FUNCTIONS*資訊類型*的**SQLGetInfo** ，判斷驅動程式支援的時間和日期函數。  
  
 表示為*timestamp_exp*的引數可以是資料行的名稱、另一個純量函式的結果，或 odbc--escape、 *odbc--escape*或 odbc*時間**戳-escape*，其中基礎資料類型可表示為 SQL_CHAR、SQL_VARCHAR、SQL_TYPE_TIME、SQL_TYPE_DATE 或 SQL_TYPE_TIMESTAMP。  
  
 表示為 *date_exp* 的引數可以是資料行的名稱、另一個純量函數的結果，或 *odbc-日期/* ////////////////////////////SQL_TYPE_DATE SQL_VARCHAR SQL_CHAR *///////////* SQL_TYPE_TIMESTAMP 或 odbc  
  
 表示為 *time_exp* 的引數可以是資料行的名稱、另一個純量函數的結果，或 *odbc-escape* 或 *odbc 時間戳記-escape*，其中基礎資料類型可表示為 SQL_CHAR、SQL_VARCHAR、SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP。  
  
 ODBC 3.0 中已加入 CURRENT_DATE、CURRENT_TIME 和 CURRENT_TIMESTAMP timedate 純量函數，以配合 SQL-92。  
  
|函式|描述|  
|--------------|-----------------|  
|**CURRENT_DATE ( ) ** (ODBC 3.0) |傳回目前的日期。|  
|**CURRENT_TIME [ (** *時間精確度* **) ]** (ODBC 3.0) |傳回目前的當地時間。 *時間精確度*引數會決定傳回值的秒數有效位數。|  
|**CURRENT_TIMESTAMP**<br /> **[ (** *timestamp-precision* **) ]** (ODBC 3.0) |以時間戳記值傳回目前的本機日期和本地時間。 *時間戳記精確度*引數會決定傳回之時間戳記的秒數有效位數。|  
|**CURDATE ( ) ** (ODBC 1.0) |傳回目前的日期。|  
|**CURTIME ( ) ** (ODBC 1.0) |傳回目前的當地時間。|  
|**DAYNAME (** *DATE_EXP* **) ** (ODBC 2.0) |傳回包含日期之資料來源特定名稱的字元字串 (例如，星期日到星期六或 Sun。 到 Sat.； 若為使用英文的資料來源，或針對 *date_exp*的日期部分使用德文) 的資料來源，則使用則為 sonntag 至 Samstag。|  
|**DAYOFMONTH (** *DATE_EXP* **) ** (ODBC 1.0) |根據 *date_exp* 中的月份欄位，傳回月份的日期（以1-31 範圍內的整數值為准）。|  
|**DAYOFWEEK (** *DATE_EXP* **) ** (ODBC 1.0) |根據 *date_exp* 中的周欄位，傳回一周的哪一天做為1-7 範圍內的整數值，其中1代表星期日。|  
|**DAYOFYEAR (** *DATE_EXP* **) ** (ODBC 1.0) |根據 *date_exp* 中的年份欄位，傳回一年中的日期，作為1-366 範圍內的整數值。|  
|**EXTRACT (** *從**解壓縮來源* **) **解壓縮 (解壓縮-來源 (ODBC 3.0) |傳回*解壓縮來源*的*解壓縮欄位*部分。 *解壓縮來源*引數是 datetime 或 interval 運算式。 *解壓縮欄位*引數可以是下列其中一個關鍵字：<br /><br /> YEAR MONTH DAY HOUR 分鐘<br /><br /> 傳回值的有效位數是實作為定義。 除非指定了第二個，否則小數位數為0，在此情況下，小數位數不小於 *解壓縮來源* 欄位的小數秒精確度。|  
|** (** *TIME_EXP* **) ** (ODBC 1.0) |根據 *time_exp* 中的小時欄位，傳回以0-23 範圍內的整數值為依據的小時。|  
|**分鐘 (** *TIME_EXP* **) ** (ODBC 1.0) |根據 *time_exp* 中的分鐘欄位，以0-59 範圍內的整數值傳回分鐘。|  
|** (** *DATE_EXP* **) ** (ODBC 1.0) |根據 *date_exp* 中的月份欄位，傳回月份範圍1-12 中的整數值。|  
|**MONTHNAME (** *DATE_EXP* **) ** (ODBC 2.0) |傳回包含月份之資料來源特定名稱的字元字串 (例如，一月到十二月或 Jan. 至 Dec. 至 Dec。針對使用英文的資料來源，或則為 januar 至使用德文) 的資料來源（ *date_exp*的月份部分）。|  
|**現在 ( ) ** (ODBC 1.0) |傳回目前的日期和時間做為時間戳記值。|  
|**季 (** *DATE_EXP* **) ** (ODBC 1.0) |傳回 *date_exp* 中的季作為1-4 範圍內的整數值，其中1代表1月1日到3月31日。|  
|**第二 (** *TIME_EXP* **) ** (ODBC 1.0) |根據 *time_exp* 中的第二個欄位，傳回第二個欄位，其為0-59 範圍內的整數值。|
|**TIMESTAMPADD (** *間隔*、 *INTEGER_EXP*、 *timestamp_exp* **) ** (ODBC 2.0) |藉由將類型*間隔*的*integer_exp*間隔新增至*timestamp_exp*，來傳回計算的時間戳記。 有效的 *interval* 值為下列關鍵字：<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 其中小數秒會以 billionths 的秒數表示。 例如，下列 SQL 語句會傳回每個員工的名稱以及其一年週年日：<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> 如果 *timestamp_exp* 是時間值，而且 *間隔* 指定為天、周、月、季或年，則在計算產生的時間戳記之前， *timestamp_exp* 的日期部分會設定為目前的日期。<br /><br /> 如果 *timestamp_exp* 是日期值，而且 *間隔* 指定小數秒、秒、分鐘或小時，則在計算產生的時間戳記之前， *timestamp_exp* 的時間部分會設定為0。<br /><br /> 應用程式會使用 SQL_TIMEDATE_ADD_INTERVALS 選項來呼叫 **SQLGetInfo** ，以決定資料來源支援的間隔。|  
|**TIMESTAMPDIFF (** *間隔*、 *TIMESTAMP_EXP1*、 *timestamp_exp2* **) ** (ODBC 2.0) |傳回*timestamp_exp2*大於*timestamp_exp1*之*間隔*的整數間隔整數數目。 有效的 *interval* 值為下列關鍵字：<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 其中小數秒會以 billionths 的秒數表示。 例如，下列 SQL 語句會傳回每個員工的名稱，以及其所採用的年份數：<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> 如果時間戳記運算式是時間值，而且 *間隔* 指定天數、周、月、季或年，則時間戳記的日期部分會設定為目前的日期，然後才計算時間戳記之間的差異。<br /><br /> 如果其中一個時間戳記運算式是日期值，而且 *間隔* 指定小數秒、秒、分鐘或小時，則時間戳記的時間部分會設定為0，然後才計算時間戳記之間的差異。<br /><br /> 應用程式會使用 SQL_TIMEDATE_DIFF_INTERVALS 選項來呼叫 **SQLGetInfo** ，以決定資料來源支援的間隔。|  
|**WEEK (** *DATE_EXP* **) ** (ODBC 1.0) |根據 *date_exp* 中的周欄位，傳回一年中的第幾周，做為1-53 範圍內的整數值。|  
|**YEAR (** *DATE_EXP* **) ** (ODBC 1.0) |根據 *date_exp* 中的年份欄位，傳回以整數值為基礎的年份。 範圍與資料來源相依。|
