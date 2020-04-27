---
title: 間隔資料類型精確度 |Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81290738"
---
# <a name="interval-data-type-precision"></a>間隔資料類型精確度
間隔資料類型的有效位數包括間隔前置精確度、間隔精確度和秒數有效位數。  
  
 間隔的前置欄位是帶正負號的數位。 前置欄位的最大位數是由稱為「*間隔前置精確度*」的數量所決定，這是資料類型宣告的一部分。 例如，宣告：間隔小時（5）到分鐘的間隔前置精確度為 5;[小時] 欄位可以接受-99999 到99999之間的值。 間隔前置精確度會包含在描述項記錄的 SQL_DESC_DATETIME_INTERVAL_PRECISION 欄位中。  
  
 間隔資料類型所組成的欄位清單稱為「*間隔精確度*」。 這不是數值，因為「精確度」一詞可能會隱含。 例如，類型 INTERVAL DAY 到 SECOND 的間隔有效位數是清單 DAY、HOUR、MINUTE、SECOND。 沒有包含此值的描述項欄位。間隔有效位數一律可以由 interval 資料類型決定。  
  
 具有第二個欄位的任何間隔資料類型都有*秒有效位數*。 這是秒數值小數部分允許的十進位數。 這與其他資料類型不同，其中 precision 表示小數點前面的位數。 Interval 資料類型的秒數精確度是小數點之後的位數。 例如，如果秒數有效位數設定為6，則 [分數] 欄位中的數位123456會解讀為123456，而數位1230會解讀為. 001230。 對於其他資料類型，這稱為「小數值」。 間隔秒數精確度會包含在描述項的 SQL_DESC_PRECISION 欄位中。 如果 SQL 間隔值的小數秒數部分的有效位數大於 C 間隔結構中可保留的數值，則會定義驅動程式，不論在轉換成 C 間隔結構時，SQL 間隔中的小數秒值是否會四捨五入或截斷。  
  
 當 [SQL_DESC_CONCISE_TYPE] 欄位設定為 [間隔] 資料類型時，[SQL_DESC_TYPE] 欄位會設定為 [SQL_INTERVAL]，而 [SQL_DESC_DATETIME_INTERVAL_CODE] 會設定為 [interval] 資料類型的程式碼。 [SQL_DESC_DATETIME_INTERVAL_PRECISION] 欄位會自動設為預設間隔的有效位數2，而 [SQL_DESC_PRECISION] 欄位會自動設為預設的間隔秒數有效位數6。 如果這些值都不適合，應用程式應該透過呼叫**SQLSetDescField**來明確設定描述項欄位。
