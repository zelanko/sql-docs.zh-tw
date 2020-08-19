---
description: 資料緩衝區長度
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4ad4f083d9f08c744dd6f832638a49b57c04e6c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429370"
---
# <a name="data-buffer-length"></a>資料緩衝區長度
應用程式會在名為 *BufferLength* 或類似名稱的引數中，將資料緩衝區的位元組長度傳遞給驅動程式。 例如，在下列對 **SQLBindCol**的呼叫中，應用程式會指定 *ValuePtr* 緩衝區的長度 (**sizeof (***ValuePtr***) **) ：  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 驅動程式一律會傳回任何具有輸出字串引數之函式的緩衝區長度引數中的位元組數目，而不是字元數。  
  
 只有輸出緩衝區需要資料緩衝區長度;驅動程式會使用它們來避免寫入超過緩衝區的結尾。 不過，只有當緩衝區包含可變長度的資料（例如字元或二進位資料）時，驅動程式才會檢查資料緩衝區長度。 如果緩衝區包含固定長度的資料（例如整數或日期結構），驅動程式會忽略資料緩衝區長度，並假設緩衝區夠大，足以容納資料。也就是說，它永遠不會截斷固定長度的資料。 因此，應用程式必須為固定長度的資料配置夠大的緩衝區。  
  
 當非資料輸出字串的截斷發生 (（例如針對 **SQLGetCursorName**) 傳回的資料指標名稱）時，緩衝區長度引數中傳回的長度會是可能的最大字元長度。  
  
 輸入緩衝區不需要資料緩衝區長度，因為驅動程式不會寫入這些緩衝區。  
  
 此章節包含下列主題。  
  
-   [使用長度/指標值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
-   [資料長度、緩衝區長度和截斷](../../../odbc/reference/develop-app/data-length-buffer-length-and-truncation.md)  
  
-   [字元資料和 C 字串](../../../odbc/reference/develop-app/character-data-and-c-strings.md)
