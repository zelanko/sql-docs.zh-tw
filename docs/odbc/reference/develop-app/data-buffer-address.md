---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7cd157edd6111dec29ae238a1c383879e66ac0b3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68067435"
---
# <a name="data-buffer-address"></a>資料緩衝區位址
應用程式會將資料緩衝區的位址傳遞至引數中的驅動程式，通常名為*valueptr 是*或類似的名稱。 例如，在下列對**SQLBindCol**的呼叫中，應用程式會指定*日期*變數的位址：  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 如配置[和釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)一節中所述，延遲緩衝區的位址必須維持有效，直到緩衝區解除系結為止。  
  
 除非特別禁止，否則資料緩衝區的位址可以是 null 指標。 對於用來將資料傳送到驅動程式的緩衝區，這會導致驅動程式忽略一般包含在緩衝區中的資訊。 針對用來從驅動程式抓取資料的緩衝區，這會導致驅動程式不傳回值。 在這兩種情況下，驅動程式都會忽略對應的資料緩衝區長度引數。
