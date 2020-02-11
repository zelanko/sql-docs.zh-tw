---
title: 間隔資料類型 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a42c8767228c75d3b7b0da308d739516875cf966
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67947550"
---
# <a name="interval-data-types"></a>間隔資料類型
間隔會定義為兩個日期和時間之間的差異。 間隔是以兩種不同方式的其中一種來表示。 一個*月*的間隔是以年為單位，而整數個月的月份表示間隔。 另一個則是以天、分鐘和秒為單位來表示間隔的*日期時間*間隔。 這兩種間隔類型是相異的，不能混用，因為月份可能會有不同的天數。  
  
 間隔是由一組欄位所組成。 欄位之間有隱含的順序。 例如，在年到月的間隔中，年份會先出現，後面接著月份。 同樣地，在每分鐘的間隔中，欄位的順序為日、小時和分鐘。 間隔類型中的第一個欄位稱為「*前置*欄位」，或「*高序位*」欄位。 最後一個欄位稱為*尾端*欄位。  
  
 在所有間隔中，前置欄位不會受到西曆規則的限制。 例如，在一個小時到分鐘的間隔中，小時欄位不會限制為介於0和23（含）之間，因為它通常是。 前置欄位後面的尾端欄位會遵循西曆的一般條件約束。 如需詳細資訊，請參閱本附錄稍後的[西曆條件約束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)。  
  
 有13個間隔的 SQL 資料類型和13個 interval C 資料類型。 每個間隔 C 資料類型都會使用相同的結構（SQL_INTERVAL_STRUCT）來包含間隔資料。 （如需詳細資訊，請參閱下一節[C Interval 結構](../../../odbc/reference/appendixes/c-interval-structure.md)）。如需 SQL 資料類型的詳細資訊，請參閱[Sql 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)。如需 C 資料類型的詳細資訊，請參閱[c 資料類型](../../../odbc/reference/appendixes/c-data-types.md)。  
  
|類型識別碼|類別|描述|  
|---------------------|-----------|-----------------|  
|月|年-月|兩個日期之間的月數。|  
|年|年-月|兩個日期之間的年數。|  
|YEAR_TO_MONTH|年-月|兩個日期之間的年份和月份數。|  
|DAY|日期時間|兩個日期之間的天數。|  
|HOUR|日期時間|兩個日期/時間之間的時數。|  
|MINUTE|日期時間|兩個日期/時間之間的分鐘數。|  
|SECOND|日期時間|兩個日期/時間之間的秒數。|  
|DAY_TO_HOUR|日期時間|兩個日期/時間之間的天數/小時數。|  
|DAY_TO_MINUTE|日期時間|兩個日期/時間之間的天數/小時/分鐘數。|  
|DAY_TO_SECOND|日期時間|兩個日期/時間之間的天數/小時/分鐘數/秒。|  
|HOUR_TO_MINUTE|日期時間|兩個日期/時間之間的小時/分鐘數。|  
|HOUR_TO_SECOND|日期時間|兩個日期/時間之間的小時/分鐘數/秒。|  
|MINUTE_TO_SECOND|日期時間|兩個日期/時間之間的分鐘數/秒。|  
  
 此章節包含下列主題。  
  
-   [C 間隔結構](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [間隔資料類型精確度](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [間隔資料類型長度](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [間隔常值](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [覆寫間隔資料類型的預設前置和秒精確度](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)
