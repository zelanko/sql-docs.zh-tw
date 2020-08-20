---
description: 覆寫數值資料類型的預設精確度和小數位數
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 798e607ff6584bde27791a29e4b20aeb1d7bb3cf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466080"
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>覆寫數值資料類型的預設精確度和小數位數
當 ARD 中的 SQL_DESC_TYPE 欄位設定為 SQL_C_NUMERIC 時，藉由呼叫 **SQLBindCol** 或 **SQLSetDescField**，ARD 中的 SQL_DESC_SCALE 欄位會設定為0，而且 SQL_DESC_PRECISION 欄位會設定為驅動程式定義的預設精確度。 當 APD 中的 SQL_DESC_TYPE 欄位設定為 SQL_C_NUMERIC （藉由呼叫 **SQLBindParameter** 或 **SQLSetDescField**）時，也會發生這種情況。 這對輸入、輸入/輸出或輸出參數而言是如此。  
  
 如果應用程式無法接受先前所述的其中一個預設值，應用程式應該呼叫 **SQLSetDescField** 或 **SQLSetDescRec**來設定 SQL_DESC_SCALE 或 SQL_DESC_PRECISION 欄位。  
  
 如果應用程式呼叫 **SQLGetData** 將資料傳回到 SQL_C_NUMERIC 結構，則會使用預設的 SQL_DESC_SCALE 和 SQL_DESC_PRECISION 欄位。 如果預設值不是可接受的，應用程式必須呼叫**SQLSetDescRec**或**SQLSetDescField**來設定欄位，然後使用 SQL_ARD_TYPE 的*TargetType*來呼叫**SQLGetData** ，以使用描述項欄位中的值。  
  
 呼叫 **SQLPutData** 時，呼叫會使用對應于資料執行中參數或資料行之描述項記錄的 SQL_DESC_SCALE 和 SQL_DESC_PRECISION 欄位，也就是呼叫 **SQLExecute** 或 **SQLExecDirect**的 APD 欄位，或呼叫 **ARD** 或 **SQLBulkOperations**的 SQLSetPos 欄位。
