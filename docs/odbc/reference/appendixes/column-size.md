---
title: 資料行大小 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07b6151c723cb5e05189791100338e9e343c28aa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306579"
---
# <a name="column-size"></a>資料行大小
數值資料類型的資料行（或參數）大小會定義為數據行或參數的資料類型所使用的最大位數，或資料的精確度。 對於字元類型，這是資料的長度（以字元為單位）;對於二進位資料類型，資料行大小會定義為以位元組為單位的資料長度。 針對時間、時間戳記和所有間隔資料類型，這是此資料的字元表示中的字元數。 下表顯示每個簡潔 SQL 資料類型所定義的資料行大小。  
  
|SQL 類型識別碼|資料行大小|  
|-------------------------|-----------------|  
|所有字元類型 [a]、[b]|以資料行或參數的字元數定義或最大資料行大小（如 [SQL_DESC_LENGTH 描述元] 欄位所包含）。 例如，定義為 CHAR （10）之單一位元組字元資料行的資料行大小為10。|  
|SQL_DECIMAL SQL_NUMERIC|定義的數位數目。 例如，定義為 NUMERIC （10，3）之資料行的有效位數為10。|  
|SQL_BIT [c]|1|  
|SQL_TINYINT [c]|3|  
|SQL_SMALLINT [c]|5|  
|SQL_INTEGER [c]|10|  
|SQL_BIGINT [c]|19（如果帶正負號）或20（如果不帶正負號）|  
|SQL_REAL [c]|7|  
|SQL_FLOAT [c]|15|  
|SQL_DOUBLE [c]|15|  
|所有二進位類型 [a]、[b]|資料行或參數的已定義或最大長度（以位元組為單位）。 例如，定義為 BINARY （10）的資料行長度為10。|  
|SQL_TYPE_DATE [c]|10（以*yyyy-mm-dd*格式的字元數）。|  
|SQL_TYPE_TIME [c]|8（ *hh-mm-ss*格式的字元數），或 9 + *s* （ *hh： mm： ss*[. fff ...] 格式的字元數，其中*s*是秒的精確度）。|  
|SQL_TYPE_TIMESTAMP|16（ *yyyy-dd hh： mm*格式的字元數）<br /><br /> 19（ *yyyy-dd* *hh： mm： ss*格式的字元數）<br /><br /> 或<br /><br /> 20 + *s* （ *yyyy-mm-dd hh： mm： ss*[. fff ...] 格式的字元數，其中*s*是秒的精確度）。|  
|SQL_INTERVAL_SECOND|其中*p*是間隔的有效位數，而*s*是秒有效位數， *p* （*如果 s*= 0）或*p*+*s*+ 1 （如果*s*>0）。d|  
|SQL_INTERVAL_DAY_TO_SECOND|其中*p*是間隔的有效位數，*而 s*是秒有效位數，9 *+ p* （如果*s*= 0）或 10 +*p*+*s* （如果*s*>0）。d|  
|SQL_INTERVAL_HOUR_TO_SECOND|其中*p*是間隔的有效位數，*而 s*是秒有效位數，6 *+ p* （如果*s*= 0）或 7 +*p*+*s* （如果*s*>0）。d|  
|SQL_INTERVAL_MINUTE_TO_SECOND|其中*p*是間隔的有效位數，*而 s*是秒有效位數，3 *+ p* （如果*s*= 0）或 4 +*p*+*s* （如果*s*>0）。d|  
|SQL_INTERVAL_YEAR SQL_INTERVAL_MONTH SQL_INTERVAL_DAY SQL_INTERVAL_HOUR SQL_INTERVAL_MINUTE|*p*，其中*p*是間隔的前置精確度。d|  
|SQL_INTERVAL_YEAR_TO_MONTH SQL_INTERVAL_DAY_TO_HOUR|3 +*p*，其中*p*是間隔的前置精確度。d|  
|SQL_INTERVAL_DAY_TO_MINUTE|6 +*p*，其中*p*是間隔的前置精確度。d|  
|SQL_INTERVAL_HOUR_TO_MINUTE|3 +*p*，其中*p*是間隔的前置精確度。d|  
|SQL_GUID|36（ *aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee*格式的字元數）|  
  
 [a] 若為 odbc 1.0 應用程式呼叫 odbc 2.0 驅動程式中的**SQLSetParam** ，以及針對在 odbc 1.0 驅動程式中呼叫**SQLBindParameter**的 odbc 2.0 \*應用程式，則當 SQL_LONGVARCHAR 或 SQL_LONGVARBINARY 類型的*StrLen_or_IndPtr*為 SQL_DATA_AT_EXEC 時， *ColumnSize*必須設定為要傳送之資料的總長度，而不是此資料表中所定義的有效位數。  
  
 [b] 如果驅動程式無法判斷變數類型的資料行或參數長度，就會傳回 SQL_NO_TOTAL。  
  
 [c] 這個資料類型會忽略**SQLBindParameter**的*ColumnSize*引數。  
  
 [d] 如需間隔資料類型中的資料行長度一般規則，請參閱本附錄稍早的[Interval 資料類型長度](../../../odbc/reference/appendixes/interval-data-type-length.md)。  
  
 針對資料行（或參數）大小傳回的值不會對應到任何一個描述項欄位中的值。 視資料類型而定，值可能來自 SQL_DESC_PRECISION 或 SQL_DESC_LENGTH 欄位，如下表所示。  
  
|SQL 類型|對應至的描述項欄位<br /><br /> 資料行或參數大小|  
|--------------|--------------------------------------------------------------------|  
|所有字元和二進位類型|LENGTH|  
|所有數數值型別|PRECISION|  
|所有日期時間和間隔類型|LENGTH|  
|SQL_BIT|LENGTH|
