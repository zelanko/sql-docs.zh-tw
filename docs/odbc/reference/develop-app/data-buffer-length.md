---
title: 資料緩衝區長度 |Microsoft 文件
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
- data buffers [ODBC], length
- buffers [ODBC], data
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 7288d143-f9e5-4f90-9b31-2549df79c109
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a8f48565b36b821ebcfffd14a89162d75c90e7bc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="data-buffer-length"></a>資料緩衝區長度
應用程式傳遞引數，名為的驅動程式的資料緩衝區的位元組長度*Columnsize*或類似的名稱。 例如，在下列呼叫**SQLBindCol**，應用程式指定的長度*ValuePtr*緩衝區 (**sizeof (***ValuePtr***)**):  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 驅動程式一定會傳回任何具有輸出的字串引數的函式的緩衝區長度引數中的位元組數，不是字元的數目。  
  
 資料緩衝區的長度所需的輸出緩衝區; 只有驅動程式會使用它們來避免寫入緩衝區的結尾。 不過，驅動程式的緩衝區包含可變長度的資料，例如字元或二進位資料時，才會檢查資料緩衝區長度。 如果緩衝區包含固定長度的資料，例如整數或日期的結構，驅動程式會忽略資料緩衝區長度，並假設緩衝區已足夠容納資料。也就是說，它永遠不會截斷固定長度的資料。 因此務必應用程式為固定長度的資料配置夠大的緩衝區。  
  
 非資料截斷輸出字串時，就會發生 (例如資料指標名稱傳回**SQLGetCursorName**)，傳回的緩衝區的長度引數中的長度是可能的最大字元長度。  
  
 因為驅動程式不會寫入這些緩衝區，並不需要輸入緩衝區的資料緩衝區長度。  
  
 此章節包含下列主題。  
  
-   [使用長度/指標值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
-   [資料長度、緩衝區長度和截斷](../../../odbc/reference/develop-app/data-length-buffer-length-and-truncation.md)  
  
-   [字元資料和 C 字串](../../../odbc/reference/develop-app/character-data-and-c-strings.md)
