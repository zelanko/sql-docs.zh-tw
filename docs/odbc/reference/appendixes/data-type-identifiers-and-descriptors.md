---
title: 資料類型識別碼和描述元 |Microsoft Docs
ms.custom: ''
ms.date: 02/02/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- identifiers [ODBC], data types
- descriptors [ODBC], data types
- verbose data types [ODBC]
- data types [ODBC], descriptors
- concise data types [ODBC]
ms.assetid: f0077c9b-8eb2-4b5f-8c4c-7436fdef37ab
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 748f2452d20b618ae0011e2e1ac4e24af098ac06
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019054"
---
# <a name="data-type-identifiers-and-descriptors"></a>資料類型識別碼和描述項
本附錄稍早的[SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)和[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)區段中所列的資料類型是「精簡」資料類型：每個識別碼都會參考單一資料類型。 識別碼與資料類型之間有一對一的對應關係。 不過，描述項不會在所有情況下使用單一值來識別資料類型。 在某些情況下，它們會使用「詳細資訊」資料類型和類型子代碼。 對於 datetime 和 interval 資料類型以外的所有資料類型，verbose 類型識別碼與精簡類型識別碼相同，而 SQL_DESC_DATETIME_INTERVAL_CODE 中的值等於0。 不過，針對 datetime 和 interval 資料類型，詳細資訊類型（SQL_DATETIME 或 SQL_INTERVAL）會儲存在 SQL_DESC_TYPE 中，精簡的類型會儲存在 SQL_DESC_CONCISE_TYPE 中，而每個精確類型的子代碼會儲存在 SQL_DESC_DATETIME_INTERVAL_CODE 中。 設定其中一個欄位會影響其他欄位。 如需這些欄位的詳細資訊，請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)函數描述。  
  
 針對某些資料類型設定 [SQL_DESC_TYPE] 或 [SQL_DESC_CONCISE_TYPE] 欄位時，SQL_DESC_DATETIME_INTERVAL_PRECISION、SQL_DESC_LENGTH、SQL_DESC_PRECISION 和 SQL_DESC_SCALE 欄位會自動設定為預設值（適用于資料）型. 如需詳細資訊，請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中的 [SQL_DESC_TYPE] 欄位的描述。 如果任何設定的預設值都不適合，應用程式應該透過呼叫**SQLSetDescField**來明確設定描述項欄位。  
  
 下表顯示每個 datetime 和 interval SQL 和 C 類型識別碼的簡潔類型識別碼、詳細資訊類型識別碼和類型子代碼。 如下表所示，對於 datetime 和 interval 資料類型，SQL_DESC_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE 欄位對於 SQL 資料類型（在執行描述項中）和 C 資料類型（在應用程式中）都具有相同的資訊清單常數。描述項）。  
  
|簡潔的 SQL 類型|簡潔的 C 類型|詳細資訊類型|DATETIME_INTERVAL_CODE|  
|----------------------|--------------------|------------------|------------------------------|  
|SQL_TYPE_DATE|SQL_C_TYPE_DATE|SQL_DATETIME|SQL_CODE_DATE|  
|SQL_TYPE_TIME|SQL_C_TYPE_TIME|SQL_DATETIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_DATETIME|SQL_CODE_TIMESTAMP|  
|SQL_INTERVAL_MONTH|SQL_C_INTERVAL_MONTH|SQL_INTERVAL|SQL_CODE_MONTH|  
|SQL_INTERVAL_YEAR|SQL_C_INTERVAL_YEAR|SQL_INTERVAL|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH|SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_INTERVAL|SQL_CODE_YEAR_TO_MONTH|  
|SQL_INTERVAL_DAY|SQL_C_INTERVAL_DAY|SQL_INTERVAL|SQL_CODE_DAY|  
|SQL_INTERVAL_HOUR|SQL_C_INTERVAL_HOUR|SQL_INTERVAL|SQL_CODE_HOUR|  
|SQL_INTERVAL_MINUTE|SQL_C_INTERVAL_MINUTE|SQL_INTERVAL|SQL_CODE_MINUTE|  
|SQL_INTERVAL_SECOND|SQL_C_INTERVAL_SECOND|SQL_INTERVAL|SQL_CODE_SECOND|  
|SQL_INTERVAL_DAY_TO_HOUR|SQL_C_INTERVAL_DAY_TO_HOUR|SQL_INTERVAL|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE|SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_INTERVAL|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND|SQL_C_INTERVAL_DAY_TO_SECOND|SQL_INTERVAL|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR_TO_MINUTE|SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_INTERVAL|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND|SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_INTERVAL|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE_TO_SECOND|SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_INTERVAL|SQL_CODE_MINUTE_TO_SECOND|
