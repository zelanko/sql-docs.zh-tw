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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947550"
---
# <a name="interval-data-types"></a>間隔資料類型
間隔被定義為兩個日期和時間之間的差異。 間隔被以兩種不同方式的其中一個。 其中一個是*年月*表示年和月數的整數間隔的時間間隔。 另一個則是*日期時間*表示時間間隔，以天、 分和秒為單位的間隔。 這兩種類型的間隔相異，且不能混用，因為月份可以有不同的數字的天數。  
  
 間隔是由一組欄位所組成。 沒有欄位之間隱含的順序。 例如，在年-月間隔內，年份何者先，後面接著每月。 同樣地，在一天到分鐘間隔內，這些欄位會訂單日、 小時和分鐘。 間隔類型的第一個欄位稱為*領先*欄位中，或有*高序位*欄位。 最後一個欄位稱為*尾端*欄位。  
  
 中所有的間隔，[前置] 欄位不會受到西曆的規則。 例如，在小時到分鐘間隔內，[小時] 欄位不受限制會介於 0 到 23 （含），因為它通常是。 前置的欄位之後尾端的欄位會依西曆的一般條件約束。 如需詳細資訊，請參閱 <<c0> [ 西曆的條件約束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)稍後在本附錄中。  
  
 有 13 間隔 SQL 資料類型和 13 間隔 C 資料類型。 每個間隔 C 資料類型會使用相同的結構，SQL_INTERVAL_STRUCT，來包含資料的間隔。 (如需詳細資訊，請參閱下一步 區段中， [C 間隔結構](../../../odbc/reference/appendixes/c-interval-structure.md)。)如需有關 SQL 資料類型的詳細資訊，請參閱 < [SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md); 如上的 C 資料類型的詳細資訊，請參閱[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)。  
  
|型別識別項|類別|描述|  
|---------------------|-----------|-----------------|  
|MONTH|年月|兩個日期之間的月數。|  
|YEAR|年月|兩個日期之間的年數。|  
|YEAR_TO_MONTH|年月|年數和兩個日期之間的月數。|  
|DAY|日期時間|兩個日期之間的日數。|  
|HOUR|日期時間|兩個之間的小時數的日期/時間。|  
|MINUTE|日期時間|兩個之間的分鐘數的日期/時間。|  
|SECOND|日期時間|兩個之間的秒數的日期/時間。|  
|DAY_TO_HOUR|日期時間|兩個之間的天數或時數的數字日期/時間。|  
|DAY_TO_MINUTE|日期時間|天/小時/之間的分鐘數兩個日期/時間。|  
|DAY_TO_SECOND|日期時間|數天/小時/分鐘/秒之間兩個日期/時間。|  
|HOUR_TO_MINUTE|日期時間|小時/之間的分鐘數兩個日期/時間。|  
|HOUR_TO_SECOND|日期時間|兩個小時/分鐘/秒鐘的日期/時間。|  
|MINUTE_TO_SECOND|日期時間|分鐘/之間的秒數兩個日期/時間。|  
  
 此章節包含下列主題。  
  
-   [C 間隔結構](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [間隔資料類型精確度](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [間隔資料類型長度](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [間隔常值](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [覆寫間隔資料類型的預設前置和秒精確度](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)
