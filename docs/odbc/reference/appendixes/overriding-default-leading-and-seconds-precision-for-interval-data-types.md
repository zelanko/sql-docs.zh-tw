---
title: 間隔資料類型的超控前導和秒精度 |微軟文件
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
ms.openlocfilehash: 1e60d5d8fc696ad8e2bd4cfb0c082ff214e066d0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303599"
---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>覆寫間隔資料類型的預設前置和秒精確度
當 ARD 的SQL_DESC_TYPE欄位設定為日期時間或間隔 C 類型時,通過調用**SQLBindCol**或**SQLSetDescField,SQL_DESC_PRECISION**欄位(包含間隔秒精度)設定為以下預設值:  
  
-   6 表示時間戳和具有第二個元件的所有間隔數據類型。  
  
-   0 表示所有其他數據類型。  
  
 對於所有間隔數據類型,包含間隔前導欄位精度SQL_DESC_DATETIME_INTERVAL_PRECISION描述符欄位設置為預設值 2。  
  
 當 APD 中的SQL_DESC_TYPE欄位設定為日期時間或間隔 C 類型時,透過呼叫**SQLBind 參數**或**SQLSetDescField,APD**中的SQL_DESC_PRECISION和SQL_DESC_DATETIME_INTERVAL_PRECISION欄位設定為之前給出的預設值。 輸入參數也是如此,但輸入/輸出或輸出參數則不然。  
  
 對**SQLSetDescRec**的呼叫將間隔前導精度設置為預設值,但將間隔秒精度(在SQL_DESC_PRECISION欄位中)設置為其*精度*參數的值。  
  
 如果以前給出的任一預設值都不允許應用程式接受,則應用程式應通過調用**SQLSetDescField**來設置SQL_DESC_PRECISION或SQL_DESC_DATETIME_INTERVAL_PRECISION欄位。  
  
 如果應用程式調用**SQLGetData**將數據返回到日期時間或間隔 C 類型,則使用預設間隔前導精度和間隔秒精度。 如果任一預設值不可接受,則應用程式必須調用**SQLSetDescField**來設置描述符欄位,或者**SQLSetDescRec**以設置SQL_DESC_PRECISION。 對**SQLGetData 的**呼叫應具有*一個目標類型*SQL_ARD_TYPE,用於使用描述符欄位中的值。  
  
 當調用**SQLPutData**時,從對應於執行時的資料參數或列的描述符記錄的欄位讀取間隔前導精度和間隔秒精度,這些欄位是調用**SQLExecute**或**SQLExecDirect**的 APD 欄位,或調用**SQLBulk 操作**或**SQLSetPos**的 ARD 欄位。
