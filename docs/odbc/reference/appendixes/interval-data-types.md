---
title: "Interval 資料類型 |Microsoft 文件"
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
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f1e19ac3f7c14326524ab7cbaa60f499c5d81e91
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="interval-data-types"></a>Interval 資料類型
間隔會定義為兩個日期和時間之間的差異。 間隔被以兩種不同方式的其中一個。 其中一個是*年-月*表示根據年份和月份的整數間隔的間隔。 另一個則*天時間*表達方面天、 分和秒的時間間隔的間隔。 這兩種類型的間隔相異，且不能混用，因為月份中可以擁有不同數字的天數。  
  
 間隔是由一組欄位所組成。 沒有欄位之間的隱含的順序。 例如，在年-月間隔內，年份是第一次，後面接著每月。 同樣地，在一天到分鐘間隔內，欄位位於訂單日、 小時和分鐘。 間隔類型的第一個欄位稱為*前置* 欄位中，或*高序位*欄位。 最後一個欄位稱為*尾端*欄位。  
  
 所有的間隔中前置的欄位不會受限於西曆的規則。 例如，在小時分鐘間隔內，小時欄位不是限制必須介於 0 到 23 之間 （含），因為它通常是。 前置的欄位之後的尾端欄位遵循西曆的一般條件約束。 如需詳細資訊，請參閱[西曆的條件約束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)稍後在本附錄中。  
  
 有 13 間隔 SQL 資料類型和 13 間隔 C 資料類型。 每個間隔 C 資料類型使用相同的結構，SQL_INTERVAL_STRUCT，以包含間隔的資料。 (如需詳細資訊，請參閱下節中， [C 間隔結構](../../../odbc/reference/appendixes/c-interval-structure.md)。)如需有關 SQL 資料類型的詳細資訊，請參閱[SQL 資料型別](../../../odbc/reference/appendixes/sql-data-types.md); 若為 C 資料類型上的詳細資訊，請參閱[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)。  
  
|類型識別碼|類別|Description|  
|---------------------|-----------|-----------------|  
|MONTH|年-月|兩個日期之間的月數。|  
|YEAR|年-月|兩個日期之間的年數。|  
|YEAR_TO_MONTH|年-月|年份和兩個日期之間的月數。|  
|DAY|日期時間|兩個日期之間的日數。|  
|HOUR|日期時間|兩個小時數將日期/時間。|  
|MINUTE|日期時間|兩個之間的分鐘數將日期/時間。|  
|SECOND|日期時間|兩個之間的秒數將日期/時間。|  
|DAY_TO_HOUR|日期時間|日期/之間的小時數兩個日期/時間。|  
|DAY_TO_MINUTE|日期時間|天/小時/之間的分鐘數兩個日期/時間。|  
|DAY_TO_SECOND|日期時間|數天/小時/分鐘/秒兩個日期/時間。|  
|HOUR_TO_MINUTE|日期時間|小時/之間的分鐘數兩個日期/時間。|  
|HOUR_TO_SECOND|日期時間|兩個小時/分鐘/秒數將日期/時間。|  
|MINUTE_TO_SECOND|日期時間|分鐘/之間的秒數兩個日期/時間。|  
  
 此章節包含下列主題。  
  
-   [C 間隔結構](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [間隔資料類型有效位數](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [間隔資料類型長度](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [間隔常值](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [覆寫間隔資料類型的預設前置和秒數有效位數](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)

