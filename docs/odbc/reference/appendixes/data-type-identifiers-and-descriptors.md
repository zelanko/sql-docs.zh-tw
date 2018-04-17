---
title: 資料類型識別碼和描述元 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data types [ODBC], identifiers
- identifiers [ODBC], data types
- descriptors [ODBC], data types
- verbose data types [ODBC]
- data types [ODBC], descriptors
- concise data types [ODBC]
ms.assetid: f0077c9b-8eb2-4b5f-8c4c-7436fdef37ab
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f9d36c0308ae7afb12541a0f33f4d2b417dfb15e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="data-type-identifiers-and-descriptors"></a>資料類型識別碼和描述元
資料類型會列於[SQL 資料型別](../../../odbc/reference/appendixes/sql-data-types.md)和[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)稍早在本附錄中的區段都是 「 精簡 」 資料類型： 每個識別項是指單一資料類型。 沒有識別碼與資料類型之間的一對一對應。 描述元，不過，執行不會在所有情況下使用單一值來識別資料類型。 在某些情況下，他們會使用"verbose"的資料類型和類型的次要代碼。 除了 datetime 和間隔資料類型的所有資料型別的詳細資訊的類型識別項與相同的精簡型別識別碼，SQL_DESC_DATETIME_INTERVAL_CODE 中的值等於 0。 日期時間和間隔資料類型，不過，詳細資訊的類型 （如果是 SQL_DATETIME 或 SQL_INTERVAL） 會儲存在 SQL_DESC_TYPE、 精簡型別會儲存在 SQL_DESC_CONCISE_TYPE，，和子代碼，每一種精簡的類型會儲存在 SQL_DESC_DATETIME_INTERVAL_CODE。 設定一個欄位，會影響其他人。 如需有關這些欄位的詳細資訊，請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)函式描述。  
  
 當 SQL_DESC_TYPE 或 SQL_DESC_CONCISE_TYPE 欄位中設定某些資料類型時，SQL_DESC_DATETIME_INTERVAL_PRECISION、 SQL_DESC_LENGTH、 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 欄位會自動設定為預設值，視您的資料型別。 如需詳細資訊，請參閱中的 SQL_DESC_TYPE 欄位描述[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 如果設定的預設值的任何不適當，應用程式應該明確設定描述項欄位，透過呼叫**SQLSetDescField**。  
  
 下表顯示精簡型別識別項、 詳細資訊的類型識別碼和型別子代碼，每個日期時間和間隔 SQL 和 C 類型識別項。 日期時間和間隔資料類型，此表格指出 SQL_DESC_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE 欄位有相同的資訊清單常數 （在實作描述元） 的 SQL 資料類型和 C 資料類型 （在應用程式描述元）。  
  
|精簡的 SQL 型別|精簡的 C 類型|詳細資訊的類型|DATETIME_INTERVAL_CODE|  
|----------------------|--------------------|------------------|------------------------------|  
|SQL_TYPE_DATE|SQL_C_TYPE_DATE|SQL_DATETIME|SQL_CODE_DATE|  
|SQL_TYPE_TIME|SQL_C_TYPE_TIME|SQL_DATETIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_DATETIME|SQL_CODE_TIMESTAMP|  
|SQL_INTERVAL_MONTH|SQL_C_INTERVAL_MONTH|SQL_INTERVAL|SQL_CODE_MONTH|  
|SQL_INTERVAL_YEAR|SQL_C_INTERVAL_YEAR|SQL_INTERVAL|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH|SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_INTERVAL|SQL_CODE_YEAR_TO_MONTH|  
QL_INTERVAL_DAY|SQL_C_INTERVAL_DAY|SQL_INTERVAL|SQL_CODE_DAY|  
|SQL_INTERVAL_HOUR|SQL_C_INTERVAL_HOUR|SQL_INTERVAL|SQL_CODE_HOUR|  
|SQL_INTERVAL_MINUTE|SQL_C_INTERVAL_MINUTE|SQL_INTERVAL|SQL_CODE_MINUTE|  
|SQL_INTERVAL_SECOND|SQL_C_INTERVAL_SECOND|SQL_INTERVAL|SQL_CODE_SECOND|  
|SQL_INTERVAL_DAY_TO_HOUR|SQL_C_INTERVAL_DAY_TO_HOUR|SQL_INTERVAL|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE|SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_INTERVAL|SQL_CODE_DAY_TO_MINUTE|  
QL_INTERVAL_DAY_TO_SECOND|SQL_C_INTERVAL_DAY_TO_SECOND|SQL_INTERVAL|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR_TO_MINUTE|SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_INTERVAL|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND|SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_INTERVAL|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE_TO_SECOND|SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_INTERVAL|SQL_CODE_MINUTE_TO_SECOND|
