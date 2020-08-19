---
description: 資料緩衝區位址
title: 資料緩衝區位址 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- address of data buffers [ODBC]
- buffers [ODBC], data
- data buffers [ODBC], address
ms.assetid: f2426d68-71bc-4ef7-a5cb-ee9d6c1c9671
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 301202933ae9cb0206100b6bbf10dda305495be1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429380"
---
# <a name="data-buffer-address"></a>資料緩衝區位址
應用程式會將資料緩衝區的位址傳遞給引數中的驅動程式，通常稱為 *ValuePtr* 或類似的名稱。 例如，在下列對 **SQLBindCol**的呼叫中，應用程式會指定 *日期* 變數的位址：  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 如「配置 [和釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md) 」一節所述，延遲緩衝區的位址必須保持有效，直到緩衝區解除系結為止。  
  
 除非明確禁止，否則資料緩衝區的位址可以是 null 指標。 針對用來將資料傳送至驅動程式的緩衝區，這會導致驅動程式忽略通常包含在緩衝區中的資訊。 針對用來從驅動程式取出資料的緩衝區，這會導致驅動程式不會傳回值。 在這兩種情況下，驅動程式都會忽略對應的資料緩衝區長度引數。
