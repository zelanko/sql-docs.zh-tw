---
title: 時間、 日期和間隔函數 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 52d0aba10c3e01ddd5cbcc709235f4f483907fb3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47712612"
---
# <a name="time-date-and-interval-functions"></a>時間、日期和間隔函數
下表列出 ODBC 純量函式集合中包含的日期和時間的函式。 應用程式可以判斷驅動程式支援的日期和時間函式藉由呼叫**SQLGetInfo**具有*資訊類型*SQL_TIMEDATE_FUNCTIONS。  
  
 引數可以分成*timestamp_exp*可以是資料行的名稱，另一個的純量函式的結果或有*ODBC 時間逸出*， *ODBC 日期逸出*，或*ODBC 時間戳記逸出*，其中可能表示基礎資料類型為 SQL_CHAR、 SQL_VARCHAR、 SQL_TYPE_TIME、 SQL_TYPE_DATE 或 SQL_TYPE_TIMESTAMP。  
  
 引數可以分成*date_exp*可以是資料行的名稱，另一個的純量函式的結果或*ODBC 日期逸出*或是*ODBC 時間戳記逸出*，其中基礎資料類型可以表示成 SQL_CHAR、 SQL_VARCHAR、 SQL_TYPE_DATE 或 SQL_TYPE_TIMESTAMP。  
  
 引數可以分成*time_exp*可以是資料行的名稱，另一個的純量函式的結果或*ODBC 時間逸出*或是*ODBC 時間戳記逸出*，其中基礎資料類型可以表示成 SQL_CHAR、 SQL_VARCHAR、 SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP。  
  
 CURRENT_DATE、 CURRENT_TIME 和 CURRENT_TIMESTAMP timedate 純量函式已加入在 ODBC 3.0，才能符合 SQL-92。  
  
|函數|描述|  
|--------------|-----------------|  
|**CURRENT_DATE （)** (ODBC 3.0)|傳回目前的日期。|  
|**CURRENT_TIME [(** *時間有效位數* **)]** (ODBC 3.0)|傳回目前的當地時間。 *時間有效位數*引數會決定傳回值的秒數有效位數。|  
|**CURRENT_TIMESTAMP**<br /> **[(** *時間戳記有效位數* **)]** (ODBC 3.0)|傳回目前本機日期和本地時間做為時間戳記值。 *時間戳記有效位數*引數會決定傳回的時間戳記的秒數有效位數。|  
|**CURDATE （)** (ODBC 1.0)|傳回目前的日期。|  
|**CURTIME （)** (ODBC 1.0)|傳回目前的當地時間。|  
|**DAYNAME (** *date_exp* **)** (ODBC 2.0)|傳回字元字串，包含資料來源特定的星期幾名稱 （例如，Sunday 到 Saturday 或 Sun。 到 Sat.； 針對資料來源使用德文的資料來源，使用英文，則為 Sonntag 到 Samstag） 的日期部份*date_exp*。|  
|**DAYOFMONTH (** *date_exp* **)** (ODBC 1.0)|傳回根據 [月份] 欄位中月份天數*date_exp*成為整數值 1 – 31 的範圍。|  
|**DAYOFWEEK (** *date_exp* **)** (ODBC 1.0)|傳回根據中的週欄位的一週天數*date_exp*範圍內的整數值 1-7，其中 1 代表星期日。|  
|**DAYOFYEAR (** *date_exp* **)** (ODBC 1.0)|傳回根據 [年] 欄位中的一年天數*date_exp*為範圍內的 1 – 366 的整數值。|  
|**擷取 (** *擷取欄位 FROM* *擷取來源* **)** (ODBC 3.0)|傳回*擷取欄位*一部分*擷取來源*。 *擷取來源*引數是日期時間或間隔的運算式。 *擷取欄位*引數可以是其中一個下列關鍵字：<br /><br /> 年月日小時分鐘秒<br /><br /> 傳回值的有效位數是由實作定義。 小數位數是 0 除非另有指定第二，在此情況下小數位數的小數秒數有效位數大於或等於*擷取來源*欄位。|  
|**小時 (** *time_exp* **)** (ODBC 1.0)|傳回小時中的小時欄位為基礎*time_exp*成為整數值 0 – 23 之間範圍中。|  
|**分鐘 (** *time_exp* **)** (ODBC 1.0)|傳回分鐘中的分鐘欄位為基礎*time_exp*成為整數值範圍內的 0 – 59 之間。|  
|**月 (** *date_exp* **)** (ODBC 1.0)|傳回月份中的月份欄位為基礎*date_exp*成為整數值 1 – 12 的範圍中。|  
|**MONTHNAME (** *date_exp* **)** (ODBC 2.0)|傳回包含資料來源 – 月份的特定名稱 （例如，January 到 December 或使用英文的資料來源的則為 Januar 到 Dezember 使用德文的資料來源） 的字元字串之月份部分*date_exp*。|  
|**現在 （)** (ODBC 1.0)|傳回目前日期和時間做為時間戳記值。|  
|**季 (** *date_exp* **)** (ODBC 1.0)|傳回在季*date_exp*成為整數值的範圍中，1 – 4，其中 1 代表月 1 日至 3 月 31 日。|  
|**第二個 (** *time_exp* **)** (ODBC 1.0)|傳回根據中的第二個欄位的第二個*time_exp*成為整數值範圍內的 0 – 59 之間。|
|**TIMESTAMPADD (** *間隔*， *integer_exp*， *timestamp_exp* **)** (ODBC 2.0)|傳回計算方式是加入時間戳記*integer_exp*型別的間隔*間隔*來*timestamp_exp*。 有效值*間隔*下列關鍵字：<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 其中的表示十億分之一秒的小數秒數。 例如，下列 SQL 陳述式會傳回每位員工和他或她的一年的週年日的名稱：<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> 如果*timestamp_exp*是一個時間值和*間隔*指定天、 週、 月、 季或年的日期部分*timestamp_exp*設為目前的日期之前計算產生的時間戳記。<br /><br /> 如果*timestamp_exp*是日期值和*間隔*指定小數秒數、 秒、 分鐘或小時為單位的 time 部分*timestamp_exp*設為 0 之前計算產生的時間戳記。<br /><br /> 應用程式判斷資料來源支援藉由呼叫的間隔**SQLGetInfo** SQL_TIMEDATE_ADD_INTERVALS 選項。|  
|**TIMESTAMPDIFF (** *間隔*， *timestamp_exp1*， *timestamp_exp2* **)** (ODBC 2.0)|傳回型別的間隔的整數數字*間隔*由此*timestamp_exp2*大於*timestamp_exp1*。 有效值*間隔*下列關鍵字：<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 其中的表示十億分之一秒的小數秒數。 例如，下列 SQL 陳述式會傳回每位員工和採用他或她的年數的名稱：<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> 如果任一個時間戳記運算式是一個時間值和*間隔*指定天、 週、 月、 季或年來，該時間戳記的日期部分設為目前的日期，然後才計算時間戳記之間的差異。<br /><br /> 如果任一個時間戳記運算式是日期值和*間隔*指定小數秒數、 秒、 分鐘或小時，該時間戳記的時間部分設為 0 之前計算時間戳記之間的差異。<br /><br /> 應用程式判斷資料來源支援藉由呼叫的間隔**SQLGetInfo** SQL_TIMEDATE_DIFF_INTERVALS 選項。|  
|**週 (** *date_exp* **)** (ODBC 1.0)|傳回年份中的週欄位為基礎的一週*date_exp*成為整數值 1 – 53 範圍中。|  
|**年 (** *date_exp* **)** (ODBC 1.0)|傳回根據 [年] 欄位中的年份*date_exp*成為整數值。 範圍是資料來源而定。|
