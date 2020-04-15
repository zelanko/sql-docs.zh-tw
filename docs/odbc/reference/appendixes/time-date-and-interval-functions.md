---
title: 時間、日期和間隔函數 |微軟文件
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
ms.openlocfilehash: aec3d6b23383edcc9659ff884e8cd71b0595dae1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302819"
---
# <a name="time-date-and-interval-functions"></a>時間、日期和間隔函數
下表列出了 ODBC 標量函數集中包括的時間和日期函數。 應用程式可以通過使用SQL_TIMEDATE_FUNCTIONS*的資訊類型*呼叫**SQLGetInfo**來確定驅動程式支援哪些時間和日期函數。  
  
 表示為*timestamp_exp*的參數可以是列的名稱、另一個標量函數的結果或*ODBC 時間轉義**、ODBC-日期轉義*或*ODBC 時間戳轉義*,其中基礎數據類型可以表示為SQL_CHAR、SQL_VARCHAR、SQL_TYPE_TIME、SQL_TYPE_DATE 或SQL_TYPE_TIMESTAMP。  
  
 表示為*date_exp*的參數可以是列的名稱、另一個標量函數的結果或*ODBC 日期轉義*或*ODBC 時間戳轉義*,其中基礎數據類型可以表示為SQL_CHAR、SQL_VARCHAR、SQL_TYPE_DATE 或SQL_TYPE_TIMESTAMP。  
  
 表示為*time_exp*的參數可以是列的名稱、另一個標量函數的結果或*ODBC 時間轉義*或*ODBC 時間戳轉義*,其中基礎數據類型可以表示為SQL_CHAR、SQL_VARCHAR、SQL_TYPE_TIME 或SQL_TYPE_TIMESTAMP。  
  
 在 ODBC 3.0 中添加了CURRENT_DATE、CURRENT_TIME和CURRENT_TIMESTAMP時間日期標量函數,以便與 SQL-92 對齊。  
  
|函式|描述|  
|--------------|-----------------|  
|**CURRENT_DATE(** ODBC 3.0)|傳回目前的日期。|  
|**CURRENT_TIME[(***時間精度***)]** (ODBC 3.0)|傳回目前的當地時間。 *時間精度*參數確定返回值的秒精度。|  
|**CURRENT_TIMESTAMP**<br /> **[ (***時間戳精度***)]** (ODBC 3.0)|將當前本地日期和本地時間作為時間戳值返回。 *時間戳精度*參數確定返回的時間戳的秒精度。|  
|**(ODBC** 1.0)|傳回目前的日期。|  
|**CURTIME( (ODBC** 1.0)|傳回目前的當地時間。|  
|**天名稱(** *date_exp* **)** (ODBC 2.0)|返回包含當天數據來源特定名稱的字串(例如,星期日到星期六或周日)。 到 Sat.； 對於使用英語的數據源,或 Sonntag 通過 Samstag 的數據源,使用德語)的*date_exp*日部分。|  
|**月日(** *date_exp* **)** (ODBC 1.0)|根據*date_exp*中的月份欄位返回月份中的天,作為 1-31 範圍內的整數值。|  
|**週日(date_exp** *date_exp* **)** (ODBC 1.0)|根據*date_exp*中的周欄位返回星期數,作為 1-7 範圍內的整數值,其中 1 表示星期日。|  
|**日 (date_exp** *date_exp* **)** (ODBC 1.0)|根據*date_exp*中的年份欄位將一年中的天作為 1-366 範圍內的整數值返回。|  
|**擷取(***從擷取物來源提取欄位**extract-source* **)(ODBC** 3.0)|返回*提取源*的*提取欄位*部分。 *提取源*參數是日期時間或間隔運算式。 *提取欄位*參數可以是以下關鍵字之一:<br /><br /> 年月小時分鐘秒<br /><br /> 返回值的精度是實現定義的。 除非指定了"秒",否則比例為 0,在這種情況下,比例不小於*提取源*欄位的小數秒精度。|  
|**小時 time_exp** *time_exp* **)** (BC 1.0)|根據*time_exp*中的小時欄位返回小時,作為 0-23 範圍內的整數值。|  
|**分鐘(time_exp** *time_exp* **)** (ODBC 1.0)|返回基於*time_exp*中的分鐘欄位的分鐘,作為 0-59 範圍內的整數值。|  
|**月(date_exp** *date_exp* **)** (ODBC 1.0)|基於*date_exp*中的月份欄位返回月份,作為 1-12 範圍內的整數值。|  
|**月名稱(** *date_exp* **)** (ODBC 2.0)|返回包含該月特定於數據源名稱的字串(例如,1月至 12 月或 1 月到 12 月,對於使用英語的數據源,或使用德語的數據源的 Januar 通過 Dezember)返回 date_exp*的月份*部分。|  
|**現在(** ODBC 1.0)|將當前日期和時間作為時間戳值返回。|  
|**零(date_exp** *date_exp* **)** (ODBC 1.0)|*將 date_exp*中的季度作為 1-4 範圍內的整數值返回,其中 1 表示 1 月 1 日至 3 月 31 日。|  
|**秒(** *time_exp* **)** (ODBC 1.0)|返回基於*time_exp*中的第二個字段,作為 0-59 範圍內的整數值。|
|**時間戳(***間隔*, *integer_exp*, *timestamp_exp* **)** (ODBC 2.0)|使用*integer_exp**類型間隔間隔*, 將*timestamp_exp,* 傳回計算的時間戳。 *間隔*的有效值如下關鍵字:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 其中分數秒以十億分之一秒表示。 例如,以下 SQL 語句返回每個員工的姓名及其一周年日期:<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> 如果*timestamp_exp*是時間值,*並且間隔*指定了天、周、月、季度或年,則*timestamp_exp*的日期部分在計算結果的時間戳之前設置為當前日期。<br /><br /> 如果*timestamp_exp*是日期值,*並且間隔*指定分數秒、秒、分鐘或小時,則在計算結果的時間戳之前 *,timestamp_exp*的時間部分設置為 0。<br /><br /> 應用程式通過使用SQL_TIMEDATE_ADD_INTERVALS選項調用**SQLGetInfo**來確定數據來源支援哪個間隔。|  
|**時間戳(***間隔**,timestamp_exp1,timestamp_exp2)*(ODBC *timestamp_exp2* **)** 2.0)|返回*timestamp_exp2*大於*timestamp_exp1*的類型*間隔*的整數。 *間隔*的有效值如下關鍵字:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 其中分數秒以十億分之一秒表示。 例如,以下 SQL 語句返回每個員工的姓名及其雇用的年數:<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> 如果時間戳表示式是時間值,*並且間隔*指定日期、周、月、季度或年,則該時間戳的日期部分在計算時間戳之間的差異之前設置為當前日期。<br /><br /> 如果時間戳表示式是日期值,*並且間隔*指定分數秒、秒、分鐘或小時,則在計算時間戳之間的差異之前,該時間戳的時間部分設置為 0。<br /><br /> 應用程式通過使用SQL_TIMEDATE_DIFF_INTERVALS選項調用**SQLGetInfo**來確定數據來源支援哪個間隔。|  
|**週(date_exp** *date_exp* **)** (ODBC 1.0)|根據*date_exp*中的周欄位返回一年中的周,作為 1-53 範圍內的整數值。|  
|**年份 (date_exp** *date_exp* **)** (ODBC 1.0)|基於*date_exp*中的年份欄位作為整數值返回年份。 範圍與數據源相關。|
