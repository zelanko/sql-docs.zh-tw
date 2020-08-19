---
description: 覆寫間隔資料類型的預設前置和秒精確度
title: 覆寫間隔資料類型的前置和秒精確度 |Microsoft Docs
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
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: 3d65493f-dce7-4d29-9f59-c63a4e47918c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97375bf23a8530d78dea65dc75ce487cc4f807dd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425000"
---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>覆寫間隔資料類型的預設前置和秒精確度
當 ARD 的 SQL_DESC_TYPE 欄位設定為 datetime 或 interval C 類型時，藉由呼叫 **SQLBindCol** 或 **SQLSetDescField**，包含間隔秒精確度) 的 SQL_DESC_PRECISION 欄位 (會設定為下列預設值：  
  
-   6代表時間戳記，而所有間隔資料類型具有第二個元件。  
  
-   0代表所有其他資料類型。  
  
 針對所有間隔資料類型，包含間隔前置欄位精確度的 SQL_DESC_DATETIME_INTERVAL_PRECISION 描述項欄位會設定為預設值2。  
  
 當 APD 中的 SQL_DESC_TYPE 欄位設定為 datetime 或 interval C 類型時，藉由呼叫 **SQLBindParameter** 或 **SQLSetDescField**，APD 中的 SQL_DESC_PRECISION 和 SQL_DESC_DATETIME_INTERVAL_PRECISION 欄位會設定為先前指定的預設值。 這適用于輸入參數，但不適用於輸入/輸出或輸出參數。  
  
 對 **SQLSetDescRec** 的呼叫會將間隔前置精確度設定為預設值，但會將 SQL_DESC_PRECISION) 欄位中的間隔秒數精確度 (設定為其 *precision* 引數的值。  
  
 如果應用程式無法接受先前指定的任一個預設值，應用程式應該呼叫 **SQLSetDescField**來設定 SQL_DESC_PRECISION 或 SQL_DESC_DATETIME_INTERVAL_PRECISION 欄位。  
  
 如果應用程式呼叫 **SQLGetData** 來將資料傳回 datetime 或 interval C 型別，則會使用預設的間隔精確度和間隔秒數有效位數。 如果這兩個預設值都不是可接受的，應用程式必須呼叫 **SQLSetDescField** 來設定描述項欄位或 **SQLSetDescRec** ，以設定 SQL_DESC_PRECISION。 對 **SQLGetData** 的呼叫應該要有 SQL_ARD_TYPE 的 *TargetType* ，才能使用描述項欄位中的值。  
  
 當呼叫 **SQLPutData** 時，系統會從對應至資料執行中參數或資料行的描述項記錄欄位（這些是 APD 欄位來呼叫 **SQLExecute** 或 **SQLExecDirect**，或 ARD 欄位以呼叫 **SQLBulkOperations** 或 **SQLSetPos**），讀取間隔前置精確度和間隔秒精確度。
