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
manager: craigg
ms.openlocfilehash: f07f835361fcf29143376fe468a55f0bf26e31e3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601276"
---
# <a name="data-buffer-address"></a>資料緩衝區位址
應用程式會將資料緩衝區的位址傳遞至驅動程式的引數，通常名為*ValuePtr*或其他類似的名稱。 例如，在下列呼叫來**SQLBindCol**，應用程式指定的地址*日期*變數：  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 中所述[Allocating 及釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md) 區段中，延後的緩衝區位址一定會保持有效，直到緩衝區未繫結。  
  
 特別是禁止，除非資料緩衝區的位址可以是 null 指標。 用來將資料傳送至驅動程式的緩衝區，這會導致驅動程式略過通常在緩衝區中所包含的資訊。 用來從驅動程式擷取資料的緩衝區，這會導致驅動程式傳回的值。 在這兩種情況下，驅動程式會忽略對應的資料緩衝區長度引數。
