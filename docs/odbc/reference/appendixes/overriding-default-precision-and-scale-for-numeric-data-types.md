---
title: 數位資料類型的壓倒預設精度和縮放 |微軟文件
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
ms.openlocfilehash: 365c5f69d21dd3a4ad8e89805d81f1b3b0c9dcba
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303589"
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>覆寫數值資料類型的預設精確度和小數位數
當ARD中的SQL_DESC_TYPE欄位設置為SQL_C_NUMERIC,通過調用**SQLBindCol**或**SQLSetDescField,ARD**中的SQL_DESC_SCALE欄位設置為 0,SQL_DESC_PRECISION欄位設置為驅動程式定義的預設精度。 當 APD 中的SQL_DESC_TYPE欄位設定為SQL_C_NUMERIC時,透過調用**SQLBind 參數**或**SQLSetDescField,** 也是如此。 對於輸入、輸入/輸出或輸出參數,情況也是如此。  
  
 如果應用程式不能接受前面描述的任一預設值,則應用程式應通過調用**SQLSetDescField**或**SQLSetDescRec**來設置SQL_DESC_SCALE或SQL_DESC_PRECISION欄位。  
  
 如果應用程式調用**SQLGetData**將數據返回到SQL_C_NUMERIC結構中,則使用預設SQL_DESC_SCALE和SQL_DESC_PRECISION欄位。 如果預設值不可接受,則應用程式必須調用**SQLSetDescRec**或**SQLSetDescField**來設置欄位,然後使用*目標類型*SQL_ARD_TYPE調用**SQLGetData**以使用描述符位中的值。  
  
 呼叫**SQLPutData**時,呼叫使用與執行時的資料參數或列對應的描述符記錄SQL_DESC_SCALE和SQL_DESC_PRECISION欄位,這些欄位是呼叫**SQLExecute**或**SQLExecDirect**的 APD 字段,或調用**SQLBulk 操作**或**SQLSetPos**的 ARD 字段。
