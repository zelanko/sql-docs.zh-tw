---
title: "時間、 日期和間隔函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- functions [ODBC], time functions
- functions [ODBC], date functions
- interval functions [ODBC]
- functions [ODBC], interval functions
- time functions [ODBC]
- date functions [ODBC]
ms.assetid: bdf054a0-7aba-4e99-a34a-799917376fd5
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: b6d6655b1640eff66182c78ea919849194d9714c
ms.openlocfilehash: 54a471846953e7afffa74fe910ae7376731e517b
ms.contentlocale: zh-tw
ms.lasthandoff: 10/05/2017

---
# <a name="time-date-and-interval-functions"></a>時間、日期和間隔函數
下表列出 ODBC 純量函式集合中包含的日期和時間函式。 應用程式就可以判斷驅動程式支援的日期和時間函式呼叫**SQLGetInfo**與*資訊類型*SQL_TIMEDATE_FUNCTIONS。  
  
 引數表示為*timestamp_exp*可以是資料行的名稱，另一個純量函數的結果或*ODBC 時間-逸出*， *ODBC 日期-逸出*，或*ODBC 時間戳記-逸出*，其中基礎資料類型可以表示為 SQL_CHAR、 SQL_VARCHAR、 SQL_TYPE_TIME、 SQL_TYPE_DATE 或 SQL_TYPE_TIMESTAMP。  
  
 引數表示為*date_exp*可以是資料行的名稱，另一個純量函數的結果或*ODBC 日期-逸出*或*ODBC 時間戳記-逸出*，其中無法以如 SQL_CHAR、 SQL_VARCHAR、 SQL_TYPE_DATE 或 SQL_TYPE_TIMESTAMP 表示基礎資料類型。  
  
 引數表示為*time_exp*可以是資料行的名稱，另一個純量函數的結果或*ODBC 時間-逸出*或*ODBC 時間戳記-逸出*，其中無法以如 SQL_CHAR、 SQL_VARCHAR、 SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP 表示基礎資料類型。  
  
 CURRENT_DATE、 CURRENT_TIME 和 CURRENT_TIMESTAMP timedate 純量函式已加入在 ODBC 3.0 以配合 SQL 92。  
  
|函數|Description|  
|--------------|-----------------|  
|**CURRENT_DATE （)** (ODBC 3.0)|傳回目前的日期。|  
|**CURRENT_TIME [(** *時間精確度* **)]** (ODBC 3.0)|傳回目前的當地時間。 *時間精確度*引數會決定傳回值的秒數有效位數。|  
|**CURRENT_TIMESTAMP**<br /> **[(** *時間戳記有效位數* **)]** (ODBC 3.0)|傳回目前的本地日期和本地時間做為時間戳記值。 *時間戳記有效位數*引數會決定傳回的時間戳記的秒數有效位數。|  
|**CURDATE （)** (ODBC 1.0)|傳回目前的日期。|  
|**CURTIME （)** (ODBC 1.0)|傳回目前的當地時間。|  
|**DAYNAME (** *date_exp* **)** (ODBC 2.0)|傳回字元字串，包含資料來源專用星期幾之名稱的 （例如，Sunday 到 Saturday 或 Sun。 到 Sat.； 針對資料來源，使用德文的資料來源會使用英文，則為 Sonntag 到 Samstag） 的日期部分*date_exp*。|  
|**DAYOFMONTH (** *date_exp* **)** (ODBC 1.0)|傳回根據 [月份] 欄位中的月份天數*date_exp*成為整數值 1-31 的範圍中。|  
|**DAYOFWEEK (** *date_exp* **)** (ODBC 1.0)|傳回根據中的週欄位的一週天數*date_exp*成為整數值範圍內的 1-7，其中 1 代表星期日。|  
|**DAYOFYEAR (** *date_exp* **)** (ODBC 1.0)|傳回根據 [year] 欄位中的年度日*date_exp*成為整數值 1 – 366 的範圍內。|  
|**擷取 (** *擷取欄位 FROM* *擷取來源* **)** (ODBC 3.0)|傳回*擷取欄位*部分*擷取來源*。 *擷取來源*引數是日期時間或間隔的運算式。 *擷取欄位*引數可以是下列關鍵字：<br /><br /> 年月日小時分第二個<br /><br /> 傳回值的精確度是由實作定義。 標尺為 0 除非另有指定第二，在此情況下小數位數不是小數秒數有效位數大於或等於*擷取來源*欄位。|  
|**小時 (** *time_exp* **)** (ODBC 1.0)|傳回根據 [小時] 欄位中的小時*time_exp*成為整數值範圍內的 0 – 23 之間。|  
|**分鐘 (** *time_exp* **)** (ODBC 1.0)|傳回根據 [分鐘] 欄位中的分鐘*time_exp*成為整數值範圍內的 0 – 59 之間。|  
|**月 (** *date_exp* **)** (ODBC 1.0)|傳回根據 [月份] 欄位中的月份*date_exp*成為整數值 1 – 12 的範圍中。|  
|**MONTHNAME (** *date_exp* **)** (ODBC 2.0)|傳回包含月份 （例如，January 到 December 或其中的資料來源，就會使用英文或為 Januar 到 Dezember 使用德文的資料來源） 資料來源特定名稱之字元字串之月份部分的*date_exp*。|  
|**現在 （)** (ODBC 1.0)|傳回目前的日期和時間的時間戳記值。|  
|**季 (** *date_exp* **)** (ODBC 1.0)|傳回當季中的*date_exp*成為整數值範圍內的 1 – 4，其中 1 代表月 1 日到 3 月 31 日。|  
|**第二個 (** *time_exp* **)** (ODBC 1.0)|傳回根據第二個欄位中的第二個*time_exp*成為整數值範圍內的 0 – 59 之間。|
|**TIMESTAMPADD (** *間隔*， *integer_exp*， *timestamp_exp* **)** (ODBC 2.0)|傳回計算方式是加入時間戳記*integer_exp*型別的間隔*間隔*至*timestamp_exp*。 有效的值*間隔*下列關鍵字：<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 其中的小數秒數是以表示十億分之一秒。 例如，下列 SQL 陳述式會傳回每位員工和他或她的一年的週年日的名稱：<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> 如果*timestamp_exp*為時間值和*間隔*指定日、 週、 月、 季或年的日期部分*timestamp_exp*設為目前日期之前在計算結果的時間戳記。<br /><br /> 如果*timestamp_exp*是日期值和*間隔*指定小數秒數、 秒、 分鐘或小時為單位的時間部分*timestamp_exp*設為 0 之前在計算結果的時間戳記。<br /><br /> 應用程式會決定哪些資料來源支援藉由呼叫的間隔**SQLGetInfo** SQL_TIMEDATE_ADD_INTERVALS 選項。|  
|**TIMESTAMPDIFF (** *間隔*， *timestamp_exp1*， *timestamp_exp2* **)** (ODBC 2.0)|傳回型別的間隔的整數數目*間隔*藉以*timestamp_exp2*大於*timestamp_exp1*。 有效的值*間隔*下列關鍵字：<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 其中的小數秒數是以表示十億分之一秒。 例如，下列 SQL 陳述式會傳回每位員工和採用他或她的年數的名稱：<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> 如果時間戳記的任一個運算式為時間值和*間隔*指定日、 週、 月、 季或年來，該時間戳記的日期部分設定為目前的日期，然後才計算時間戳記之間的差異。<br /><br /> 如果時間戳記的任一個運算式是日期值和*間隔*指定小數秒數、 秒、 分鐘或小時的時間戳記的時間部分設定為 0 之前計算時間戳記之間的差異。<br /><br /> 應用程式會決定哪些資料來源支援藉由呼叫的間隔**SQLGetInfo** SQL_TIMEDATE_DIFF_INTERVALS 選項。|  
|**週 (** *date_exp* **)** (ODBC 1.0)|傳回一週中的週欄位為基礎的*date_exp*成為整數值範圍內的 1 – 53。|  
|**年份 (** *date_exp* **)** (ODBC 1.0)|傳回根據 [year] 欄位中的年份*date_exp*成為整數值。 範圍是資料來源而定。|

