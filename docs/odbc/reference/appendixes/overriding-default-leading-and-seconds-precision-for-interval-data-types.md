---
title: 覆寫間隔資料類型的前置和秒數有效位數 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: 3d65493f-dce7-4d29-9f59-c63a4e47918c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca22fe0d3153fc5ea4f0c5594ff537d65d60c066
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>覆寫間隔資料類型的預設前置和秒數有效位數
當 ARD 的 SQL_DESC_TYPE 欄位設定為日期時間或間隔 C 類型時，藉由呼叫**SQLBindCol**或**SQLSetDescField**，SQL_DESC_PRECISION 欄位 （其中包含間隔秒數有效位數） 設定為下列的預設值：  
  
-   6 是時間戳記以及與第二個元件的所有間隔資料類型。  
  
-   0 代表所有其他資料類型。  
  
 所有的間隔資料型別 SQL_DESC_DATETIME_INTERVAL_PRECISION 描述項欄位，其中包含間隔開頭的欄位有效位數，設定為預設值為 2。  
  
 當 APD 中的 SQL_DESC_TYPE 欄位設定為日期時間或間隔 C 類型時，藉由呼叫**SQLBindParameter**或**SQLSetDescField**，SQL_DESC_PRECISION 和 SQL_DESC_DATETIME_INTERVAL_APD 中的有效位數欄位會設定為先前提供的預設值。 這適用於輸入參數，但不適用於輸入/輸出或輸出參數。  
  
 呼叫**SQLSetDescRec**設定間隔開頭有效位數為預設值，但設定的間隔秒數有效位數 （中的 SQL_DESC_PRECISION 欄位） 的值及其*精確度*引數。  
  
 如果其中一個指定的預設值之前不是可接受的應用程式，應用程式應該藉由呼叫設定 SQL_DESC_PRECISION 或 SQL_DESC_DATETIME_INTERVAL_PRECISION 欄位**SQLSetDescField**。  
  
 如果應用程式呼叫**SQLGetData**傳回日期時間或間隔 C 類型資料，預設間隔開頭有效位數和間隔秒數有效位數使用。 如果其中一個預設值不是可接受的應用程式必須呼叫**SQLSetDescField**設定其中一個描述元欄位，或**SQLSetDescRec**設定 SQL_DESC_PRECISION。 呼叫**SQLGetData**應有*TargetType*的 SQL_ARD_TYPE 至使用中的描述項欄位的值。  
  
 當**SQLPutData**呼叫時，間隔開頭有效位數和間隔秒數有效位數會讀取描述項記錄的欄位對應的資料在執行中參數或資料行，也就是呼叫 APD 欄位若要**SQLExecute**或**SQLExecDirect**，或呼叫的 ARD 欄位**SQLBulkOperations**或**SQLSetPos**。
