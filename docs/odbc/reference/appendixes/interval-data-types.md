---
description: 間隔資料類型
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5b54996c2f2897e47e05088b1985d190acafaad3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429670"
---
# <a name="interval-data-types"></a>間隔資料類型
間隔定義為兩個日期和時間之間的差異。 間隔是以兩種不同方式的其中一種來表示。 其中一個是 *以年* 計的間隔，以及整數個月的月數。 另一個則是以天、分和碼錶示間隔的 *日期時間* 間隔。 這兩種類型的間隔是相異的，且不能混用，因為月份可能會有不同的天數。  
  
 間隔是由一組欄位所組成。 欄位之間會有隱含的順序。 例如，在年度到月的間隔中，年份會先出現，然後是月份。 同樣地，在每日的間隔中，欄位會在訂單日、小時和分鐘。 間隔型別中的第一個欄位稱為「 *前置* 欄位」或「 *高序位* 」欄位。 最後一個欄位稱為 *尾端* 欄位。  
  
 在所有的間隔中，前置欄位不受西曆規則所限制。 例如，在每小時到一分鐘的間隔中，[小時] 欄位不會限制為介於0到 23 (內含) ，如同一般情況。 前置欄位後面的尾端欄位會遵循西曆的一般條件約束。 如需詳細資訊，請參閱本附錄稍後的「 [西曆條件約束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)」。  
  
 SQL 資料類型有13個間隔和13個間隔 C 資料類型。 每個間隔 C 資料類型都會使用相同的結構 SQL_INTERVAL_STRUCT，以包含間隔資料。 如需詳細資訊，請參閱下一節： [C Interval 結構](../../../odbc/reference/appendixes/c-interval-structure.md)) 。如需有關 SQL 資料類型的詳細資訊，請參閱 [sql 資料類型](../../../odbc/reference/appendixes/sql-data-types.md); (如需 C 資料類型的詳細資訊，請參閱 [c 資料類型](../../../odbc/reference/appendixes/c-data-types.md)。  
  
|類型識別碼|類別|描述|  
|---------------------|-----------|-----------------|  
|月|年月|兩個日期之間的月數。|  
|年|年月|兩個日期之間的年數。|  
|YEAR_TO_MONTH|年月|兩個日期之間的年和月數。|  
|DAY|日期時間|兩個日期之間的天數。|  
|HOUR|日期時間|兩個日期/時間之間的時數。|  
|MINUTE|日期時間|兩個日期/時間之間的分鐘數。|  
|SECOND|日期時間|兩個日期/時間之間的秒數。|  
|DAY_TO_HOUR|日期時間|兩個日期/時間之間的天數/小時數。|  
|DAY_TO_MINUTE|日期時間|兩個日期/時間之間的天數/小時/分鐘數。|  
|DAY_TO_SECOND|日期時間|兩個日期/時間之間的天數/小時/分鐘/秒數。|  
|HOUR_TO_MINUTE|日期時間|兩個日期/時間之間的小時數/分鐘數。|  
|HOUR_TO_SECOND|日期時間|兩個日期/時間之間的小時/分鐘/秒數。|  
|MINUTE_TO_SECOND|日期時間|兩個日期/時間之間的分鐘數/秒數。|  
  
 此章節包含下列主題。  
  
-   [C 間隔結構](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [間隔資料類型精確度](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [間隔資料類型長度](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [間隔常值](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [覆寫間隔資料類型的預設前置和秒精確度](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)
