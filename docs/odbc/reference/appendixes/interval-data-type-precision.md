---
title: 間隔資料型態精度 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- precision [ODBC]
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: eb73bd77-2e7e-4498-a266-4d7c990a0d56
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 746293c545c47917abd084ec3eb105051fc2fbcf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290738"
---
# <a name="interval-data-type-precision"></a>間隔資料類型精確度
間隔數據類型的精度包括間隔前導精度、間隔精度和秒精度。  
  
 間隔的領先欄位是已簽名的數位。 前導欄位的最大位數由稱為*間隔前導精度*的數量確定,該量是數據類型聲明的一部分。 例如,聲明:INTERVAL HOUR(5)到分鐘的間隔前置精度為5;HOUR 欄位可以獲取 -99999 到 99999 的值。 間隔前導精度包含在描述符記錄的SQL_DESC_DATETIME_INTERVAL_PRECISION欄位中。  
  
 間隔資料型態組成的欄位列表稱為*間隔精度*。 它不是數值,因為術語"精度"可能暗示。 例如,「間隔日到秒」類型的間隔精度是清單天、小時、分鐘、秒。 沒有包含此值的描述符欄位;因此,沒有描述符欄位。間隔精度始終可以通過間隔數據類型確定。  
  
 具有「秒」 欄位的任何間隔資料類型都有*秒精度*。 這是秒值小數部分允許的小數位數。 這與其他數據類型不同,其中精度指示小數點之前的數字數。 間隔數據類型的秒精度是小數點之後的位數。 例如,如果秒精度設置為 6,則分數位段中的數位 123456 將解釋為 .123456,數位 1230 將解釋為 .001230。 對於其他數據類型,這稱為縮放。 間隔秒精度包含在描述符的SQL_DESC_PRECISION欄位中。 如果 SQL 間隔值的小數秒分量的精度大於 C 間隔結構中可以保留的精度,則驅動程式定義 SQL 間隔中的小數秒值在轉換為 C 間隔結構時是四捨五入還是截斷。  
  
 當SQL_DESC_CONCISE_TYPE欄位設置為間隔數據類型時,SQL_DESC_TYPE欄位設置為SQL_INTERVAL,SQL_DESC_DATETIME_INTERVAL_CODE設置為間隔數據類型的代碼。 SQL_DESC_DATETIME_INTERVAL_PRECISION欄位將自動設定為預設間隔前導精度為 2,SQL_DESC_PRECISION欄位將自動設置為預設間隔秒精度為 6。 如果其中任一值不合適,則應用程式應通過調用**SQLSetDescField**顯式設置描述符欄位。
