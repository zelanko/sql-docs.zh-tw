---
description: 間隔資料類型精確度
title: 間隔資料類型有效位數 |Microsoft Docs
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
ms.openlocfilehash: 138cb4cae21b1c1fc0fd742cefac1b6f3a3e5978
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483272"
---
# <a name="interval-data-type-precision"></a>間隔資料類型精確度
Interval 資料類型的有效位數包括間隔前置精確度、間隔精確度和秒數有效位數。  
  
 間隔的前置欄位是帶正負號的數位。 前置欄位的最大位數是由稱為「 *間隔前置精確度」（* 資料類型宣告的一部分）的數量所決定。 例如，宣告：間隔小時 (5) 分鐘的間隔有效位數為 5;[小時] 欄位可以取得-99999 到99999之間的值。 間隔前置精確度是包含在描述項記錄的 SQL_DESC_DATETIME_INTERVAL_PRECISION 欄位中。  
  
 間隔資料類型所組成的欄位清單，稱為 *間隔精確度*。 它不是數值，因為「精確度」一詞可能暗示。 例如，類型間隔日到秒的間隔精確度是清單 DAY、HOUR、MINUTE、SECOND。 沒有保留此值的描述項欄位;間隔精確度可以永遠由 interval 資料類型來決定。  
  
 具有第二個欄位的任何間隔資料類型都有 *秒數有效位數*。 這是秒值小數部分中允許的小數位數。 這與其他資料類型不同，其中 precision 表示小數點之前的位數。 間隔資料類型的秒數有效位數是小數點後的位數。 例如，如果秒數有效位數設定為6，則 [分數] 欄位中的數位123456會轉譯為123456，而數位1230會轉譯為. 001230。 對於其他資料類型，這稱為「調整」。 間隔秒數有效位數會包含在描述項的 SQL_DESC_PRECISION 欄位中。 如果 SQL 間隔值的小數秒數部分的有效位數大於 C 間隔結構中可保留的值，則會定義驅動程式，不論 SQL 間隔中的小數秒數值是否會在轉換成 C interval 結構時四捨五入或截斷。  
  
 當 SQL_DESC_CONCISE_TYPE 欄位設定為 interval 資料類型時，會將 [SQL_DESC_TYPE] 欄位設定為 [SQL_INTERVAL]，並將 SQL_DESC_DATETIME_INTERVAL_CODE 設定為 [interval] 資料類型的程式碼。 [SQL_DESC_DATETIME_INTERVAL_PRECISION] 欄位會自動設為預設的間隔，預設值為2，而 SQL_DESC_PRECISION 欄位會自動設為預設的間隔秒精確度6。 如果其中一個值不適當，則應用程式應該透過呼叫 **SQLSetDescField**來明確設定描述項欄位。
