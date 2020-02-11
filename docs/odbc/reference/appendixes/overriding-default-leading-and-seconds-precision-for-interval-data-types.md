---
title: 覆寫間隔資料類型的前置和秒有效位數 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 13adfb16b772acc5fac30cf3d10c6199f16f479d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100618"
---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>覆寫間隔資料類型的預設前置和秒精確度
當 ARD 的 SQL_DESC_TYPE 欄位設定為 datetime 或 interval C 類型時，藉由呼叫**SQLBindCol**或**SQLSetDescField**，SQL_DESC_PRECISION 欄位（包含間隔秒數有效位數）會設定為下列預設值：  
  
-   6用於 timestamp，而所有間隔資料類型具有第二個元件。  
  
-   0適用于所有其他資料類型。  
  
 對於所有間隔資料類型，[SQL_DESC_DATETIME_INTERVAL_PRECISION 描述項] 欄位（其中包含間隔前置欄位精確度）會設定為預設值2。  
  
 當 APD 中的 SQL_DESC_TYPE 欄位設定為 datetime 或 interval C 類型時，藉由呼叫**SQLBindParameter**或**SQLSetDescField**，APD 中的 [SQL_DESC_PRECISION] 和 [SQL_DESC_DATETIME_INTERVAL_PRECISION] 欄位會設定為先前指定的預設值。 這適用于輸入參數，但不適用於輸入/輸出或輸出參數。  
  
 呼叫**SQLSetDescRec**時，會將間隔的有效位數設定為預設值，但會將間隔秒數精確度（在 SQL_DESC_PRECISION 欄位中）設定為其*precision*引數的值。  
  
 如果應用程式無法接受先前指定的任何預設值，應用程式應該藉由呼叫**SQLSetDescField**來設定 SQL_DESC_PRECISION 或 SQL_DESC_DATETIME_INTERVAL_PRECISION 欄位。  
  
 如果應用程式呼叫**SQLGetData**將資料傳回 datetime 或 interval C 類型，則會使用預設的間隔前置精確度和間隔秒數有效位數。 如果其中一個預設值不是可接受的，應用程式就必須呼叫**SQLSetDescField**來設定其中一個描述項欄位，或將**SQLSetDescRec**設定為 SQL_DESC_PRECISION。 對**SQLGetData**的呼叫應具有 SQL_ARD_TYPE 的*TargetType* ，才能使用描述項欄位中的值。  
  
 當呼叫**SQLPutData**時，會從對應到資料執行中參數或資料行的描述項記錄欄位讀取間隔的有效位數和間隔秒數，這是 APD 欄位，用於呼叫**SQLExecute**或**SQLExecDirect**，或 ARD 欄位用於呼叫**SQLBulkOperations**或**SQLSetPos**。
