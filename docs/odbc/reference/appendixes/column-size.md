---
title: "資料行大小 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], column size
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
ms.assetid: 541b83ab-b16d-4714-bcb2-3c3daa9a963b
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2bc56113933e993b5748564a1c64ef1798ed8ef1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="column-size"></a>資料行大小
數值資料類型的資料行 （或參數） 的大小被定義為資料行或參數的資料類型或資料的精確度所使用的最大位數。 字元類型，這是以字元為單位的資料; 長度二進位資料類型資料行大小被定義為資料的長度以位元組為單位。 針對時間、 時間戳記和所有間隔資料型別，這是中的這項資料的字元表示法的字元數。 下表顯示每個簡潔的 SQL 資料類型所定義的資料行大小。  
  
|SQL 類型識別碼|資料行大小|  
|-------------------------|-----------------|  
|所有的字元類型 [a]、 [b]。|定義或最大資料行的大小，以字元為單位的資料行或參數 （和 SQL_DESC_LENGTH 描述項欄位中包含）。 例如，單一位元組字元資料行定義為 char （10） 的資料行大小為 10。|  
|SQL_DECIMAL SQL_NUMERIC|定義數字的數目。 例如，定義為 NUMERIC(10,3) 的資料行的有效位數為 10。|  
|SQL_BIT [c]|@shouldalert|  
|SQL_TINYINT [c]|3|  
|SQL_SMALLINT [c]|5|  
|SQL_INTEGER [c]|10|  
|SQL_BIGINT [c]|19 （如果帶正負號） 或 20 （如果不帶正負號）|  
|SQL_REAL [c]|7|  
|SQL_FLOAT [c]|15|  
|SQL_DOUBLE [c]|15|  
|所有二進位型別 [a]、 [b]。|定義或最大長度以位元組為單位的資料行或參數。 例如，定義為 binary （10） 的資料行的長度為 10。|  
|SQL_TYPE_DATE [c]|10 (中的字元數*yyyy-mm-dd*格式)。|  
|SQL_TYPE_TIME [c]|8 (中的字元數*時分秒*格式)，或 9 + *s* (中的字元數*hh: mm:*[.fff …] 格式，其中*的*的秒數有效位數)。|  
|SQL_TYPE_TIMESTAMP|16 (中的字元數*yyyy-mm-dd hh: mm*格式)<br /><br /> 19 (中的字元數*yyyy-mm-dd* *hh: mm:*格式)<br /><br /> 中的多個<br /><br /> 20 + *s* (中的字元數*yyyy-mm-dd hh: mm:*[.fff …] 格式，其中*s*的秒數有效位數)。|  
|SQL_INTERVAL_SECOND|其中*p*是間隔開頭有效位數和*s*的秒數有效位數， *p* (如果*s*= 0) 或*p* + *s*+ 1 (如果*s*> 0)。 [d]|  
|SQL_INTERVAL_DAY_TO_SECOND|其中*p*是間隔開頭有效位數和*s*是秒數有效位數 9 +*p* (如果*s*= 0)，或 10 +*p*+ *s* (如果*s*> 0)。 [d]|  
|SQL_INTERVAL_HOUR_TO_SECOND|其中*p*是間隔開頭有效位數和*s*是秒數有效位數 6 +*p* (如果*s*= 0) 或 7 +*p* + *s* (如果*s*> 0)。 [d]|  
|SQL_INTERVAL_MINUTE_TO_SECOND|其中*p*是間隔開頭有效位數和*s*是秒數有效位數 3 +*p* (如果*s*= 0) 或 4 +*p* + *s* (如果*s*> 0)。 [d]|  
|SQL_INTERVAL_YEAR SQL_INTERVAL_MONTH SQL_INTERVAL_DAY SQL_INTERVAL_HOUR SQL_INTERVAL_MINUTE|*p*，其中*p*是間隔開頭有效位數。 [d]|  
|SQL_INTERVAL_YEAR_TO_MONTH SQL_INTERVAL_DAY_TO_HOUR|3 +*p*，其中*p*是間隔開頭有效位數。 [d]|  
|SQL_INTERVAL_DAY_TO_MINUTE|6 +*p*，其中*p*是間隔開頭有效位數。 [d]|  
|SQL_INTERVAL_HOUR_TO_MINUTE|3 +*p*，其中*p*是間隔開頭有效位數。 [d]|  
|SQL_GUID|36 (中的字元數*aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee*格式)|  
  
 [a] 的 ODBC 1.0 應用程式呼叫**SQLSetParam** ODBC 2.0 驅動程式中，並用於 ODBC 2.0 應用程式呼叫**SQLBindParameter** ODBC 1.0 驅動程式中時\* *StrLen_or_IndPtr* SQL_LONGVARCHAR 或 SQL_LONGVARBINARY 類型，是 SQL_DATA_AT_EXEC *ColumnSize*必須設定為資料的總長度，要傳送的有效位數不這個資料表中所定義。  
  
 [b] 如果驅動程式無法判斷資料行或參數的長度變數的類型，它會傳回 SQL_NO_TOTAL。  
  
 [c] *ColumnSize*引數的**SQLBindParameter**會忽略此資料類型。  
  
 [d] 的相關間隔資料型別中的資料行長度的一般規則，請參閱[間隔資料類型長度](../../../odbc/reference/appendixes/interval-data-type-length.md)稍早在本附錄中。  
  
 傳回的資料行 （或參數） 大小的值中任何一個描述元欄位的值不符。 下表所示，這些值可以取自 SQL_DESC_PRECISION 或 SQL_DESC_LENGTH 欄位中的，根據資料類型而定。  
  
|SQL 類型|對應至描述項欄位<br /><br /> 資料行或參數的大小|  
|--------------|--------------------------------------------------------------------|  
|所有的字元和二進位的型別|LENGTH|  
|所有數字類型|PRECISION|  
|所有日期時間和間隔類型|LENGTH|  
|SQL_BIT|LENGTH|
