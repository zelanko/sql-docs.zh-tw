---
title: "數值資料類型覆寫預設有效位數和小數位數 |Microsoft 文件"
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
- numeric data type [ODBC], precision and scale
- precision [ODBC], numeric data types
- data types [ODBC], numeric data types
- numeric data type [ODBC]
- numeric literals [ODBC]
ms.assetid: 84292334-0e33-4a1b-84de-8c018dd787f3
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 613ec65d838a525251b6682cca477c5c8d24a162
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>覆寫預設有效位數和小數位數值資料類型
當 ARD 中的 SQL_DESC_TYPE 欄位設定為 SQL_C_NUMERIC，藉由呼叫**SQLBindCol**或**SQLSetDescField**、 ARD SQL_DESC_SCALE 欄位設定為 0，而且設定 SQL_DESC_PRECISION 欄位至驅動程式定義的預設有效位數。 這也是如此當 APD 中的 SQL_DESC_TYPE 欄位設為 SQL_C_NUMERIC，藉由呼叫**SQLBindParameter**或**SQLSetDescField**。 這是輸入、 輸入/輸出或輸出參數，則為 true。  
  
 如果其中一個所述的預設值之前不是可接受的應用程式，應用程式應該藉由呼叫設定 SQL_DESC_SCALE 或 SQL_DESC_PRECISION 欄位**SQLSetDescField**或**SQLSetDescRec**.  
  
 如果應用程式呼叫**SQLGetData** SQL_C_NUMERIC 結構傳回資料，使用預設 SQL_DESC_SCALE 和 SQL_DESC_PRECISION 欄位。 預設值不是可接受的如果應用程式必須呼叫**SQLSetDescRec**或**SQLSetDescField** ，設定欄位，然後再呼叫**SQLGetData**與*TargetType*的 SQL_ARD_TYPE 至使用中的描述項欄位的值。  
  
 當**SQLPutData**是呼叫，呼叫使用 SQL_DESC_SCALE 和 SQL_DESC_PRECISION 的欄位對應至資料在執行中參數或資料行，描述項記錄所呼叫的 APD 欄位**SQLExecute**或**SQLExecDirect**，或呼叫的 ARD 欄位**SQLBulkOperations**或**SQLSetPos**。

