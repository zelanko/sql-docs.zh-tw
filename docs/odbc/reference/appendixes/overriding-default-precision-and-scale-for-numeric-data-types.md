---
title: 覆寫數值資料類型的預設有效位數和小數位數 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], precision and scale
- precision [ODBC], numeric data types
- data types [ODBC], numeric data types
- numeric data type [ODBC]
- numeric literals [ODBC]
ms.assetid: 84292334-0e33-4a1b-84de-8c018dd787f3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 66fc728440808314dbdaa30065c68232f4a89fba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100607"
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>覆寫數值資料類型的預設精確度和小數位數
當 ARD 中的 SQL_DESC_TYPE 欄位設定為 SQL_C_NUMERIC，藉由呼叫**SQLBindCol**或是**SQLSetDescField**，ARD SQL_DESC_SCALE 欄位設定為 0，而 SQL_DESC_PRECISION 欄位會設定以驅動程式定義的預設有效位數。 這也是，則為 true 時 APD 中的 SQL_DESC_TYPE 欄位設定為 SQL_C_NUMERIC，藉由呼叫**SQLBindParameter**或是**SQLSetDescField**。 這是適用於輸入、 輸入/輸出或輸出參數。  
  
 如果其中一個所述的預設值之前不是可接受的應用程式，應用程式應該呼叫設定 SQL_DESC_SCALE 或 SQL_DESC_PRECISION 欄位**SQLSetDescField**或**SQLSetDescRec**.  
  
 如果應用程式會呼叫**SQLGetData**為了 SQL_C_NUMERIC 結構傳回資料，會使用預設 SQL_DESC_SCALE 和 SQL_DESC_PRECISION 欄位。 如果無法接受預設值，應用程式必須呼叫**SQLSetDescRec**或是**SQLSetDescField**設定欄位，然後呼叫**SQLGetData** 與*TargetType*的 SQL_ARD_TYPE 至使用中的描述項欄位的值。  
  
 當**SQLPutData**是呼叫，呼叫使用 SQL_DESC_SCALE 和 SQL_DESC_PRECISION 欄位的描述項記錄對應至資料在執行中參數或資料行，這是呼叫 APD 欄位**SQLExecute**或是**SQLExecDirect**，或呼叫 ARD 欄位**SQLBulkOperations**或是**SQLSetPos**。
