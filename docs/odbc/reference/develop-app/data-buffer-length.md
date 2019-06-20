---
title: 資料緩衝區長度 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- buffers [ODBC], data
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 7288d143-f9e5-4f90-9b31-2549df79c109
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 57f4fd34cfe3896bb29ed31f02906ce675e4b854
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62640504"
---
# <a name="data-buffer-length"></a>資料緩衝區長度
應用程式將傳遞的引數，名為驅動程式的資料緩衝區的位元組長度*Columnsize*或其他類似的名稱。 例如，在下列呼叫來**SQLBindCol**，應用程式指定的長度*ValuePtr*緩衝區 (**sizeof (***ValuePtr***)** ):  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 驅動程式一定會傳回任何具有輸出的字串引數的函式的緩衝區長度引數中的位元組數目，不是字元的數目。  
  
 資料緩衝區長度是只需要輸出緩衝區中;驅動程式會使用它們來避免寫入超過緩衝區結尾。 不過，此驅動程式，緩衝區會包含可變長度的資料，例如字元或二進位資料時，才會檢查資料緩衝區長度。 如果緩衝區包含固定長度的資料，例如整數或日期的結構，驅動程式會忽略資料緩衝區長度，並假設緩衝區夠大，無法保存資料;也就是它永遠不會截斷固定長度的資料。 因此務必為固定長度的資料配置夠大的緩衝區應用程式。  
  
 非資料截斷輸出字串時，就會發生 (例如資料指標名稱傳回**SQLGetCursorName**)，緩衝區長度的引數中傳回的長度是可能的最大字元長度。  
  
 因為驅動程式不會將寫入的緩衝區，並不需要輸入緩衝區的資料緩衝區長度。  
  
 此章節包含下列主題。  
  
-   [使用長度/指標值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
-   [資料長度、緩衝區長度和截斷](../../../odbc/reference/develop-app/data-length-buffer-length-and-truncation.md)  
  
-   [字元資料和 C 字串](../../../odbc/reference/develop-app/character-data-and-c-strings.md)
