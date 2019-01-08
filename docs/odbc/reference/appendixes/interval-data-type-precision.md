---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a8df4339ae30b9058e5a5864c37807c6b02e4fdd
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52532125"
---
# <a name="interval-data-type-precision"></a>間隔資料類型精確度
間隔資料類型的有效位數，其中包括間隔開頭有效位數、 間隔精確度和秒數有效位數。  
  
 間隔的開頭欄位是帶正負號的數值。 [前置] 欄位的數字的最大數目取決於呼叫的數量*間隔開頭有效位數，* 這是資料型別宣告的一部分。 例如，宣告：間隔 HOUR(5) 分鐘有間隔開頭有效位數 5;[小時] 欄位可以接受從-99999 到 99999 之間的值。 間隔開頭有效位數欄位中包含 SQL_DESC_DATETIME_INTERVAL_PRECISION 的描述項記錄。  
  
 間隔資料類型組成的欄位清單會呼叫*間隔精確度*。 它不數值，因為 「 精確度 」 一詞可能暗示。 間隔類型的有效位數 INTERVAL DAY TO 比方說，第二個是清單日、 小時、 分、 秒。 沒有保存此值的描述項欄位時間間隔有效位數一律取決間隔資料類型。  
  
 任何具有第二個欄位間隔資料型別都*秒數有效位數*。 這是允許的秒值的小數部分的十進位數字的數目。 這是不同於其他資料類型，其中的有效位數表示的小數點前面的位數。 間隔資料類型的秒數有效位數是小數點後的數字數目。 比方說，如果秒數有效位數設定為 6，數目 123456，在 [分數] 欄位會解譯為.123456 和數字 1230年會解譯為.001230。 對於其他資料類型，這被指小數位數。 間隔秒數有效位數欄位中包含 SQL_DESC_PRECISION 的描述元。 如果 SQL 間隔值的小數秒數元件的有效位數大於什麼可以保留 C 間隔結構中，它是驅動程式定義 SQL 間隔中的小數秒值會四捨五入或截斷時轉換成 C間隔結構。  
  
 SQL_DESC_TYPE 欄位時 SQL_DESC_CONCISE_TYPE 欄位設定為間隔資料類型，設定為 SQL_INTERVAL SQL_DESC_DATETIME_INTERVAL_CODE 設間隔資料類型的程式碼。 SQL_DESC_DATETIME_INTERVAL_PRECISION 欄位會自動設為預設間隔開頭有效位數為 2，，和 SQL_DESC_PRECISION 欄位會自動設為預設的間隔秒數有效位數為 6。 如果其中一個值不適當，應用程式應該明確設定描述項欄位，透過呼叫**SQLSetDescField**。
