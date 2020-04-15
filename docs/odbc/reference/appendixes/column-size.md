---
title: 欄大小 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306579"
---
# <a name="column-size"></a>資料行大小
數位資料類型的列(或參數)大小定義為列或參數的數據類型使用的最大位數或數據的精度。 對於字元類型,這是數據的長度;對於二進位資料類型,列大小定義為數據的長度(以位元組為單位)。 對於時間、時間戳和所有間隔數據類型,這是此數據字元表示中的字元數。 為每種簡潔的 SQL 數據類型定義的列大小顯示在下表中。  
  
|SQL 類型識別碼|欄大小|  
|-------------------------|-----------------|  
|所有字元類型[a],[b]|以列或參數的字元表示定義的或最大列大小(如SQL_DESC_LENGTH描述符欄位中所示)。 例如,定義為 CHAR (10) 的單位元組位元列的列大小為 10。|  
|SQL_DECIMALSQL_NUMERIC|定義的位數。 例如,定義為數位(10,3)的列的精度為 10。|  
|SQL_BIT[c]|1|  
|SQL_TINYINT[c]|3|  
|SQL_SMALLINT[c]|5|  
|SQL_INTEGER[c]|10|  
|SQL_BIGINT[c]|19 (如果簽署) 或 20 (如果未簽署 )|  
|SQL_REAL[c]|7|  
|SQL_FLOAT[c]|15|  
|SQL_DOUBLE[c]|15|  
|所有二進位類型[a],[b]|列或參數的已定義長度或最大長度(以位元組為單位)。 例如,定義為 BINARY(10) 的列的長度為 10。|  
|SQL_TYPE_DATE[c]|*10(yyyy-mm-dd*格式的字元數)。|  
|SQL_TYPE_TIME[c]|*8(hh-mm-s 格式*的字元數)或*s*9 = s(hh:mm:ss [.fff...] 格式的字元數,其中*hh:mm:ss**s*是秒精度)。|  
|SQL_TYPE_TIMESTAMP|16 *(yyyy-mm-dd hh:mm*格式的字元)<br /><br /> 19 *(yyyy-mm-dd* *hh:mm:ss*格式中的字元數)<br /><br /> 或<br /><br /> 20+ *s* *(yyyy-mm-dd hh:mm:ss*[.fff...] 格式的字元數,其中*s*是秒精度)。|  
|SQL_INTERVAL_SECOND|*p*是間隔前導精度 *,s*是秒精度 *,p(* 如果*s*=0)或*p*+*s*=1(如果*s*>0)。[d]|  
|SQL_INTERVAL_DAY_TO_SECOND|*p*是間隔前導精度 *,s*是秒精度,9+*p(* 如果*s*=0)或 10°*p*+*s(* 如果*s*>0)。[d]|  
|SQL_INTERVAL_HOUR_TO_SECOND|*p*是間隔前導精度 *,s*是秒精度,6°*p(* 如果*s*=0)或 7°*p*+*s(* 如果*s*>0)。[d]|  
|SQL_INTERVAL_MINUTE_TO_SECOND|*p*是間隔前導精度 *,s*是秒精度,3+*p(* 如果*s*=0)或 4°*p*+*s(* 如果*s*>0)。[d]|  
|SQL_INTERVAL_MONTH SQL_INTERVAL_DAYSQL_INTERVAL_MONTHSQL_INTERVAL_HOURSQL_INTERVAL_MINUTESQL_INTERVAL_YEAR|*p*,其中*p*是間隔前導精度。[d]|  
|SQL_INTERVAL_YEAR_TO_MONTHSQL_INTERVAL_DAY_TO_HOUR|3+*p*,其中*p*是間隔前導精度。[d]|  
|SQL_INTERVAL_DAY_TO_MINUTE|6+*p*,其中*p*是間隔前導精度。[d]|  
|SQL_INTERVAL_HOUR_TO_MINUTE|3+*p*,其中*p*是間隔前導精度。[d]|  
|SQL_GUID|36 *(aaaaaaa-bbbb-cccc-ddd-eeeeeeeeeee*格式的字元數)|  
  
 [a] 對於在 ODBC 2.0 驅動程式中調用**SQLSetParam**的 ODBC 1.0 應用程式,對於在 ODBC 1.0 驅動程式中調用**SQLBind 參數**的 ODBC 2.0 應用程式,當\**StrLen_or_IndPtrSQL_LONGVARCHAR*或SQL_LONGVARBINARY類型SQL_DATA_AT_EXEC時,列*Size*必須設置為要發送的數據的總長度,而不是本表中定義的精度。  
  
 [b] 如果驅動程式無法確定變數類型的列或參數長度,則返回SQL_NO_TOTAL。  
  
 [c] 此資料類型將忽略**SQLBind 參數**的*列大小*參數。  
  
 [d] 有關間隔資料類型中的欄長度的一般規則,請參閱本附錄前面段[的間隔資料類型長度](../../../odbc/reference/appendixes/interval-data-type-length.md)。  
  
 為列(或參數)大小返回的值與任何一個描述符欄位中的值不對應。 這些值可以來自SQL_DESC_PRECISION或SQL_DESC_LENGTH欄位,具體取決於數據類型,如下表所示。  
  
|SQL 類型|與<br /><br /> 欄位或參數大小|  
|--------------|--------------------------------------------------------------------|  
|所有字元與二進位型態|LENGTH|  
|所有數值類型|PRECISION|  
|所有日期時間與間隔型態|LENGTH|  
|SQL_BIT|LENGTH|
