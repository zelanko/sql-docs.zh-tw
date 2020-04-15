---
title: 數據緩衝區位址 |微軟文件
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
ms.openlocfilehash: 578e4e37a78818cb640d9f32e2480cec5951df63
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305269"
---
# <a name="data-buffer-address"></a>資料緩衝區位址
應用程式將數據緩衝區的位址傳遞給參數中的驅動程式,通常名稱為*ValuePtr*或類似名稱。 例如,在以下對**SQLBindCol**的呼叫中,應用程式指定*Date*變數的位址:  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 如[分配和釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)部分所述,延遲緩衝區的位址必須保持有效,直到緩衝區未綁定。  
  
 除非特別禁止,否則數據緩衝區的位址可以是空指標。 對於用於將數據發送到驅動程式的緩衝區,這將導致驅動程式忽略緩衝區中通常包含的資訊。 對於用於從驅動程式檢索數據的緩衝區,這將導致驅動程式不返回值。 在這兩種情況下,驅動程式都忽略相應的數據緩衝區長度參數。
