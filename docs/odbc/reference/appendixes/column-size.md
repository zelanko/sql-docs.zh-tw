---
title: 資料行的大小 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], column size
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
ms.assetid: 541b83ab-b16d-4714-bcb2-3c3daa9a963b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 22271cd37069123d0e11a3d0ab660134c61e283b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47665536"
---
# <a name="column-size"></a>資料行大小
數值資料類型的資料行 （或參數） 大小定義為資料行或參數的資料類型或資料的精確度所使用的數字的最大數目。 字元類型，這是以字元為單位的資料; 長度二進位資料類型資料行大小被定義為資料的位元組長度。 時間、 時間戳記，和所有的間隔資料類型，這是此資料的字元表示法中的字元數。 下表顯示每種精簡的 SQL 資料類型所定義的資料行大小。  
  
|SQL 型別識別項|資料行大小|  
|-------------------------|-----------------|  
|所有字元類型 [a]、 [b]。|定義或最大資料行大小以字元為單位的資料行或參數 （如 SQL_DESC_LENGTH 描述項欄位中包含）。 例如，定義為 CHAR(10) 單一位元組字元資料行的資料行大小為 10。|  
|SQL_DECIMAL SQL_NUMERIC|定義的數字數目。 例如，定義為 NUMERIC(10,3) 的資料行的有效位數是 10。|  
|SQL_BIT [c]|1|  
|SQL_TINYINT [c]|3|  
|SQL_SMALLINT [c]|5|  
|SQL_INTEGER [c]|10|  
|SQL_BIGINT [c]|19 （如果帶正負號） 或 20 （如果不帶正負號）|  
|SQL_REAL [c]|7|  
|SQL_FLOAT [c]|15|  
|SQL_DOUBLE [c]|15|  
|所有二進位型別 [a]、 [b]。|定義或最大長度以位元組為單位的資料行或參數。 例如，定義為 BINARY(10) 資料行的長度為 10。|  
|SQL_TYPE_DATE [c]|10 (中的字元數*yyyy-mm-dd 的-* 格式)。|  
|SQL_TYPE_TIME [c]|8 (中的字元數*hh 分秒*格式)，或 9 + *s* (中的字元數*hh: mm:*[.fff]] 格式，其中*的*的秒數有效位數)。|  
|SQL_TYPE_TIMESTAMP|16 (中的字元數*yyyy 為 yyyy-mm-dd hh: mm*格式)<br /><br /> 19 (中的字元數*yyyy 為 yyyy-mm-dd* *hh: mm:* 格式)<br /><br /> 中的多個<br /><br /> 20 + *s* (中的字元數*yyyy 為 yyyy-mm-dd hh: mm:*[.fff]] 格式，其中*s*是秒數有效位數)。|  
|SQL_INTERVAL_SECOND|何處*p*是間隔開頭有效位數並*s*是秒數有效位數*p* (如果*s*= 0) 或*p* + *s*+ 1 (如果*s*> 0)。 [d]|  
|SQL_INTERVAL_DAY_TO_SECOND|何處*p*是間隔開頭有效位數並*s*是秒數有效位數 9 +*p* (如果*s*= 0) 或 10 +*p*+ *s* (如果*s*> 0)。 [d]|  
|SQL_INTERVAL_HOUR_TO_SECOND|何處*p*是間隔開頭有效位數並*s*是秒數有效位數 6 +*p* (如果*s*= 0) 或 7 +*p* + *s* (如果*s*> 0)。 [d]|  
|SQL_INTERVAL_MINUTE_TO_SECOND|何處*p*是間隔開頭有效位數並*s*是秒數有效位數 3 +*p* (如果*s*= 0) 或 4 +*p* + *s* (如果*s*> 0)。 [d]|  
|SQL_INTERVAL_YEAR SQL_INTERVAL_MONTH SQL_INTERVAL_DAY SQL_INTERVAL_HOUR SQL_INTERVAL_MINUTE|*p*，其中*p*是間隔開頭有效位數。 [d]|  
|SQL_INTERVAL_YEAR_TO_MONTH SQL_INTERVAL_DAY_TO_HOUR|3 +*p*，其中*p*是間隔開頭有效位數。 [d]|  
|SQL_INTERVAL_DAY_TO_MINUTE|6 +*p*，其中*p*是間隔開頭有效位數。 [d]|  
|SQL_INTERVAL_HOUR_TO_MINUTE|3 +*p*，其中*p*是間隔開頭有效位數。 [d]|  
|SQL_GUID|36 (中的字元數*aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee*格式)|  
  
 [a] 的 ODBC 1.0 應用程式呼叫**SQLSetParam** ODBC 2.0 驅動程式，以及 ODBC 2.0 應用程式呼叫**SQLBindParameter** ODBC 1.0 驅動程式中時\* *StrLen_or_IndPtr* SQL_LONGVARCHAR 或 SQL_LONGVARBINARY 類型，是 SQL_DATA_AT_EXEC *ColumnSize*必須設定為資料的總長度，以傳送，不是有效位數此表格中所定義。  
  
 [b] 如果驅動程式無法判斷資料行或參數的長度變數的類型，它會傳回 SQL_NO_TOTAL。  
  
 [c] *ColumnSize*引數**SQLBindParameter**會忽略此資料型別。  
  
 [d] 的一般資料行長度，以間隔資料類型的詳細規則，請參閱[間隔資料類型長度](../../../odbc/reference/appendixes/interval-data-type-length.md)稍早在本附錄中。  
  
 傳回的資料行 （或參數） 大小的值不符中任何一個的描述項欄位的值。 值可以來自 SQL_DESC_PRECISION 或 SQL_DESC_LENGTH 欄位中，類型的資料，根據下表所示。  
  
|SQL 類型|對應到描述項欄位<br /><br /> 資料行或參數的大小|  
|--------------|--------------------------------------------------------------------|  
|所有的字元和二進位類型|LENGTH|  
|所有數字類型|PRECISION|  
|所有日期時間和間隔類型|LENGTH|  
|SQL_BIT|LENGTH|
