---
title: 間隔資料類型 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- second intervals [ODBC]
- data types [ODBC], interval data types
- interval data type [ODBC]
- day-time intervals [ODBC]
- intervals [ODBC], about intervals
- minute intervals [ODBC]
- day intervals [ODBC]
- year intervals [ODBC]
- month intervals [ODBC]
- interval data type [ODBC], about interval data types
- SQL data types [ODBC], interval
- year-month intervals [ODBC]
- C data types [ODBC], interval
- interval fields [ODBC]
ms.assetid: fba93f65-c1db-44f4-91ba-532f87241cf7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ee4a6e845e0bc0830f514b2e768075dd75bcf6e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304964"
---
# <a name="interval-data-types"></a>間隔資料類型
間隔定義為兩個日期和時間之間的差異。 間隔以兩種不同的方式之一表示。 一個是*年月*間隔,以年數表示間隔,以月數表示整數。 另一個是以天、分鐘和秒表示間隔的*日間*間隔。 這兩種類型的間隔是截然不同的,不能混合,因為月份可以有不同的天數。  
  
 間隔由一組欄位組成。 欄位之間存在隱含排序。 例如,在一年到月之間,年份先到一個,然後是月份。 同樣,在一天的到分鐘的間隔中,欄位按順序按天、小時和分鐘的順序排列。 間隔類型中的第一個字段稱為*前導*欄位或*高階*欄位。 最後一個字段稱為*尾隨*欄位。  
  
 在所有間隔中,前導欄位不受公曆規則的約束。 例如,在小時到分鐘的間隔內,小時欄位不限制為 0 和 23(包括)之間,因為它通常如此。 前導欄位後面的尾隨字段遵循公曆的通常約束。 有關詳細資訊,請參閱[公曆的約束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md),請參閱本附錄後面的限制。  
  
 有 13 個間隔 SQL 資料類型和 13 個間隔 C 數據類型。 每個間隔 C 數據類型都使用相同的結構,SQL_INTERVAL_STRUCT,以包含間隔數據。 (有關詳細資訊,請參閱下一節 C[間隔結構](../../../odbc/reference/appendixes/c-interval-structure.md)。有關 SQL 資料類型的詳細資訊,請參考[SQL 資料型態](../../../odbc/reference/appendixes/sql-data-types.md)。關於 C 資料型態的詳細資訊,請參考[C 資料型態](../../../odbc/reference/appendixes/c-data-types.md)。  
  
|型態識別碼|類別|描述|  
|---------------------|-----------|-----------------|  
|月|年月|兩個日期之間的月數。|  
|年|年月|兩個日期之間的年數。|  
|YEAR_TO_MONTH|年月|兩個日期之間的年數和月數。|  
|DAY|白天|兩個日期之間的天數。|  
|HOUR|白天|兩個日期/時間之間的小時數。|  
|MINUTE|白天|兩個日期/時間之間的分鐘數。|  
|SECOND|白天|兩個日期/時間之間的秒數。|  
|DAY_TO_HOUR|白天|兩個日期/時間之間的天數/小時數。|  
|DAY_TO_MINUTE|白天|兩個日期/時間之間的天數/小時/分鐘數。|  
|DAY_TO_SECOND|白天|兩個日期/時間之間的天數/小時/分鐘/秒數。|  
|HOUR_TO_MINUTE|白天|兩個日期/時間之間的小時/分鐘數。|  
|HOUR_TO_SECOND|白天|兩個日期/時間之間的小時/分鐘/秒數。|  
|MINUTE_TO_SECOND|白天|兩個日期/時間之間的分鐘/秒數。|  
  
 此章節包含下列主題。  
  
-   [C 間隔結構](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [間隔資料類型精確度](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [間隔資料類型長度](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [間隔常值](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [覆寫間隔資料類型的預設前置和秒精確度](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)
