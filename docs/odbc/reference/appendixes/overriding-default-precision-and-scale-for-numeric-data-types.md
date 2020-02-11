---
title: 覆寫數值資料類型的預設精確度和小數位數 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100607"
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>覆寫數值資料類型的預設精確度和小數位數
當 ARD 中的 SQL_DESC_TYPE 欄位設定為 SQL_C_NUMERIC 時，藉由呼叫**SQLBindCol**或**SQLSetDescField**，ARD 中的 [SQL_DESC_SCALE] 欄位會設定為0，而 [SQL_DESC_PRECISION] 欄位會設定為驅動程式定義的預設有效位數。 當 APD 中的 SQL_DESC_TYPE 欄位設定為 SQL_C_NUMERIC （藉由呼叫**SQLBindParameter**或**SQLSetDescField**）時，也會發生這種情況。 這適用于輸入、輸入/輸出或輸出參數。  
  
 如果應用程式無法接受先前所述的其中一個預設值，應用程式應該藉由呼叫**SQLSetDescField**或**SQLSetDescRec**來設定 SQL_DESC_SCALE 或 SQL_DESC_PRECISION 欄位。  
  
 如果應用程式呼叫**SQLGetData**將資料傳回 SQL_C_NUMERIC 結構中，則會使用預設的 SQL_DESC_SCALE 和 SQL_DESC_PRECISION 欄位。 如果預設值不是可接受的，應用程式必須呼叫**SQLSetDescRec**或**SQLSetDescField**來設定欄位，然後以 SQL_ARD_TYPE 的*TargetType*呼叫**SQLGetData** ，以使用描述項欄位中的值。  
  
 呼叫**SQLPutData**時，呼叫會使用對應于資料執行中參數或資料行之描述項記錄的 SQL_DESC_SCALE 和 SQL_DESC_PRECISION 欄位，這是呼叫**SQLExecute**或**SQLExecDirect**的 APD 欄位，或是呼叫**ARD**或**SQLBulkOperations**的 SQLSetPos 欄位。
