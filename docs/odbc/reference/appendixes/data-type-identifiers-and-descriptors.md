---
title: 資料類型識別碼與描述符 :微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f65bc86213f99112daf17c67a4ca522490d32149
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284481"
---
# <a name="data-type-identifiers-and-descriptors"></a>資料類型識別碼和描述項
本附錄前面列出的[SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)和[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)部分是「簡明」數據類型:每個識別符引用單個數據類型。 標識碼和資料類型之間存在一對一的對應關係。 但是,描述符並非在所有情況下都使用單個值來標識數據類型。 在某些情況下,它們使用"詳細"數據類型和類型子代碼。 對於除日期時間和間隔數據類型之外的所有數據類型,詳細類型標識符與簡潔類型標識符相同,SQL_DESC_DATETIME_INTERVAL_CODE中的值等於 0。 但是,對於日期時間和間隔數據類型,詳細類型(SQL_DATETIME或SQL_INTERVAL)存儲在SQL_DESC_TYPE中,簡潔類型存儲在SQL_DESC_CONCISE_TYPE中,每個簡潔類型的子代碼存儲在SQL_DESC_DATETIME_INTERVAL_CODE中。 設置這些欄位之一會影響其他欄位。 有關這些欄位的詳細資訊,請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)函數說明。  
  
 為某些資料類型設置SQL_DESC_TYPE或SQL_DESC_CONCISE_TYPE欄位時,SQL_DESC_DATETIME_INTERVAL_PRECISION、SQL_DESC_LENGTH、SQL_DESC_PRECISION和SQL_DESC_SCALE欄位將自動設置為預設值,這適用於資料類型。 有關詳細資訊,請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中SQL_DESC_TYPE欄位的說明。 如果設置的任何預設值不合適,則應用程式應通過調用**SQLSetDescField**顯式設置描述符欄位。  
  
 下表顯示了每個日期時間和間隔 SQL 和 C 類型識別碼的簡潔類型識別碼、詳細類型識別碼和類型子代碼。 正如此表所示,對於日期時間和間隔數據類型,對於 SQL 資料類型(在實現描述符中)和 C 資料類型(在應用程式描述符中),SQL_DESC_TYPE和SQL_DESC_DATETIME_INTERVAL_CODE欄位具有相同的清單常量。  
  
|簡潔的 SQL 類型|簡潔 C 類型|詳細型態|DATETIME_INTERVAL_CODE|  
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
