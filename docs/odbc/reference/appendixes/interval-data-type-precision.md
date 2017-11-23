---
title: "間隔資料類型有效位數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- precision [ODBC]
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: eb73bd77-2e7e-4498-a266-4d7c990a0d56
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ba46b5cc82fd2ac36e9a3cf920b81bc48b0d9baa
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="interval-data-type-precision"></a>間隔資料類型有效位數
間隔資料類型的有效位數包含間隔開頭有效位數、 間隔精確度和秒數有效位數。  
  
 間隔的開頭欄位是帶正負號的數值。 數字開頭的欄位數目上限取決於呼叫的數量*間隔開頭有效位數，*即屬於資料型別宣告。 例如，宣告： 間隔 HOUR(5) 分鐘有間隔開頭有效位數 5;[小時] 欄位可以接受從 –99999 到 99999 之間的值。 SQL_DESC_DATETIME_INTERVAL_PRECISION 之欄位的描述項記錄中包含間隔開頭有效位數。  
  
 間隔資料型別所組成的欄位清單稱為*間隔精確度*。 它不是數值，如"precision"一詞可能暗示。 例如，間隔之型別的精確度間隔一天到第二個是清單日、 小時、 分鐘、 秒。 保留此值; 沒有描述項欄位永遠可以間隔資料型別來判斷的間隔有效位數。  
  
 任何具有第二個欄位的間隔資料類型具有*秒數有效位數*。 這是允許的秒數值的小數部分的十進位數字的數目。 這是不同於其他資料類型，其有效位數，表示在小數點前的位數。 間隔資料類型的秒數有效位數是小數點後的數字位數。 例如，如果秒數有效位數設定為 6，123456 分數欄位中的編號會被解譯為.123456 和數字 1230年會解譯為.001230。 對於其他資料類型，這被指小數位數。 間隔秒數有效位數被包含在 SQL_DESC_PRECISION 欄位的描述元。 如果 SQL 間隔值的小數秒數元件的有效位數大於中 C 間隔結構可以保存什麼，它是驅動程式定義是否 SQL 間隔中的小數秒值四捨五入或截斷時轉換成 C間隔結構。  
  
 SQL_DESC_TYPE 欄位時 SQL_DESC_CONCISE_TYPE 欄位設定為間隔資料類型，設定為 SQL_INTERVAL 且 SQL_DESC_DATETIME_INTERVAL_CODE 設間隔的資料類型的程式碼。 SQL_DESC_DATETIME_INTERVAL_PRECISION 欄位會自動設為預設間隔開頭有效位數為 2，並 SQL_DESC_PRECISION 欄位會自動設為預設的間隔秒數有效位數為 6。 如果其中一個值不適當，應用程式應該明確設定描述項欄位，透過呼叫**SQLSetDescField**。
