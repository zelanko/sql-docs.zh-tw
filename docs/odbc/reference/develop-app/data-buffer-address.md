---
title: 資料緩衝區位址 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- address of data buffers [ODBC]
- buffers [ODBC], data
- data buffers [ODBC], address
ms.assetid: f2426d68-71bc-4ef7-a5cb-ee9d6c1c9671
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fbf649d075f0a28f3d488d5ccde11de9680ffb9e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="data-buffer-address"></a>資料緩衝區的位址
應用程式會將資料緩衝區的位址傳遞給引數，通常名為的驅動程式*ValuePtr*或類似的名稱。 例如，在下列呼叫**SQLBindCol**，應用程式指定的位址*日期*變數：  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 中所述[Allocating 和釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md) 區段中，延後的緩衝區的位址必須保持有效，直到緩衝區未繫結。  
  
 特別是禁止，除非資料緩衝區的位址可以是 null 指標。 用來將資料傳送至驅動程式的緩衝區，這會導致驅動程式略過通常在緩衝區中包含的資訊。 用來從驅動程式擷取資料的緩衝區，這會使驅動程式傳回值。 在這兩種情況下，驅動程式會忽略對應資料緩衝區的長度引數。
