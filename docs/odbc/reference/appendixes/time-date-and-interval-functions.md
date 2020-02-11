---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ae10946be501adb16fdda5fa9f053e389eea4bed
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070077"
---
# <a name="time-date-and-interval-functions"></a>時間、日期和間隔函數
下表列出 ODBC 純量函數集內所包含的時間和日期函數。 應用程式可以藉由使用 SQL_TIMEDATE_FUNCTIONS 的*資訊類型*來呼叫**SQLGetInfo** ，以判斷驅動程式支援哪些時間和日期函數。  
  
 表示為*timestamp_exp*的引數可以是資料行的名稱、另一個純量函數的結果，*或 odbc-*-escape、 *Odbc 日期-escape*或*odbc-時間戳記-escape*，其中基礎資料類型可能會表示為 SQL_CHAR、SQL_VARCHAR、SQL_TYPE_TIME、SQL_TYPE_DATE 或 SQL_TYPE_TIMESTAMP。  
  
 表示為*date_exp*的引數可以是資料行的名稱、另一個純量函數的結果，或*odbc-* --escape 或*odbc-時間戳記-escape*，其中基礎資料類型可能會表示為 SQL_CHAR、SQL_VARCHAR、SQL_TYPE_DATE 或 SQL_TYPE_TIMESTAMP。  
  
 表示為*time_exp*的引數可以是資料行的名稱、另一個純量函數的結果，或*odbc* ---escape 或*odbc-時間戳記-escape*，其中基礎資料類型可能會表示為 SQL_CHAR、SQL_VARCHAR、SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP。  
  
 ODBC 3.0 中已加入 CURRENT_DATE、CURRENT_TIME 和 CURRENT_TIMESTAMP timedate 時間純量函數，以配合 SQL-92。  
  
|函式|描述|  
|--------------|-----------------|  
|**CURRENT_DATE （）** （ODBC 3.0）|傳回目前的日期。|  
|**CURRENT_TIME [（** *時間精確度* **）]** （ODBC 3.0）|傳回目前的當地時間。 *時間精確度*引數會判斷傳回值的秒數有效位數。|  
|**CURRENT_TIMESTAMP**<br /> **[（** *時間戳記-精確度* **）]** （ODBC 3.0）|以時間戳記值傳回目前的本機日期和本地時間。 *時間戳記-precision*引數會決定所傳回之時間戳記的秒數有效位數。|  
|**CURDATE （）** （ODBC 1.0）|傳回目前的日期。|  
|**CURTIME （）** （ODBC 1.0）|傳回目前的當地時間。|  
|**DAYNAME （** *date_exp* **）** （ODBC 2.0）|傳回包含日期之資料來源特定名稱的字元字串（例如，星期日到星期六或 Sun。 到 Sat.； 若為使用英文的資料來源，或針對使用德文的資料來源則為 sonntag 至 Samstag，則為*date_exp*的日部分。|  
|**DAYOFMONTH （** *date_exp* **）** （ODBC 1.0）|根據*date_exp*中的月份欄位，傳回月份的日期，以1-31 範圍內的整數值為准。|  
|**DAYOFWEEK （** *date_exp* **）** （ODBC 1.0）|根據*date_exp*中的周欄位，傳回一周中的哪幾天做為介於1-7 範圍內的整數值，其中1代表星期日。|  
|**DAYOFYEAR （** *date_exp* **）** （ODBC 1.0）|根據*date_exp*中的 year 欄位，傳回一年中的日期，以1-366 範圍內的整數值為准。|  
|**解壓縮（** *從**解壓縮-來源*提取欄位 **）** （ODBC 3.0）|傳回*解壓縮來源*的*提取欄位*部分。 「*解壓縮-來源*」引數是 datetime 或 interval 運算式。 [*解壓縮欄位*] 引數可以是下列其中一個關鍵字：<br /><br /> 每月每小時分鐘秒<br /><br /> 傳回值的有效位數是實作為定義的。 除非指定第二個，否則小數位數為0，而在此情況下，小數位數不會小於 [*解壓縮來源*] 欄位的小數秒精確度。|  
|**小時（** *time_exp* **）** （ODBC 1.0）|根據*time_exp*中的小時欄位，傳回小時做為0-23 範圍內的整數值。|  
|**MINUTE （** *time_exp* **）** （ODBC 1.0）|根據*time_exp*中的分鐘欄位，傳回以0-59 範圍的整數值為基礎的分鐘。|  
|**MONTH （** *date_exp* **）** （ODBC 1.0）|根據*date_exp*中的月份欄位，傳回月份，以1-12 範圍內的整數值為准。|  
|**MONTHNAME （** *date_exp* **）** （ODBC 2.0）|傳回包含月份之資料來源特定名稱的字元字串（例如，1月到12月或 Jan. 到12月）。對於使用英文的資料來源，或則為 januar 至使用德文之資料來源的 Dezember，以取得*date_exp*的月份部分。|  
|**NOW （）** （ODBC 1.0）|以時間戳記值傳回目前的日期和時間。|  
|**季（** *date_exp* **）** （ODBC 1.0）|傳回*date_exp*中的季做為1-4 範圍中的整數值，其中1代表1月1日到3月31日。|  
|**SECOND （** *time_exp* **）** （ODBC 1.0）|根據*time_exp*中的第二個欄位，傳回秒數的整數值，其範圍為0-59。|
|**TIMESTAMPADD （** *interval*， *integer_exp*， *timestamp_exp* **）** （ODBC 2.0）|藉由將*interval*類型的*integer_exp*間隔加入*timestamp_exp*，來傳回所計算的時間戳記。 *Interval*的有效值為下列關鍵字：<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 小數秒數以 billionths 秒數表示。 例如，下列 SQL 語句會傳回每位員工的名稱和其一年的週年日：<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> 如果*timestamp_exp*是時間值，而*interval*指定了天、周、月、季或年，則*timestamp_exp*的日期部分會在計算產生的時間戳記之前，設定為目前的日期。<br /><br /> 如果*timestamp_exp*是日期值，而*interval*指定小數秒數、秒數、分鐘數或小時數，則在計算產生的時間戳記之前， *timestamp_exp*的時間部分會設定為0。<br /><br /> 應用程式會藉由使用 SQL_TIMEDATE_ADD_INTERVALS 選項來呼叫**SQLGetInfo** ，以決定資料來源支援的間隔。|  
|**TIMESTAMPDIFF （** *interval*， *timestamp_exp1*， *timestamp_exp2* **）** （ODBC 2.0）|傳回*timestamp_exp2*大於*timestamp_exp1*之類型*間隔*的整數間隔數。 *Interval*的有效值為下列關鍵字：<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 小數秒數以 billionths 秒數表示。 例如，下列 SQL 語句會傳回每個員工的名稱，以及他或她已雇用的年份數：<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> 如果其中一個時間戳記運算式是時間值，而*interval*指定了天、周、月、季或年，則該時間戳記的日期部分會設定為目前的日期，然後才計算時間戳記之間的差異。<br /><br /> 如果其中一個時間戳記運算式是日期值，而*interval*指定小數秒數、秒數、分鐘數或小時數，則該時間戳記的時間部分會設定為0，然後才計算時間戳記之間的差異。<br /><br /> 應用程式會藉由使用 SQL_TIMEDATE_DIFF_INTERVALS 選項來呼叫**SQLGetInfo** ，以決定資料來源支援的間隔。|  
|**周（** *date_exp* **）** （ODBC 1.0）|根據*date_exp*中的周欄位，傳回一年中的第幾周，做為1-53 範圍內的整數值。|  
|**YEAR （** *date_exp* **）** （ODBC 1.0）|根據*date_exp*中的 year 欄位，傳回以整數值為基礎的年份。 範圍與資料來源相關。|
