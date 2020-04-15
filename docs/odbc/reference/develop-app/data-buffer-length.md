---
title: 數據緩衝區長度 |微軟文件
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
ms.openlocfilehash: d4a4e9a739201d74cfc6c4f7c18e64b91e0fabe4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305259"
---
# <a name="data-buffer-length"></a>資料緩衝區長度
應用程式將數據緩衝區的位元組長度傳遞給參數中的驅動程式,稱為*BufferLength*或類似名稱。 例如,在以下對**SQLBindCol**的呼叫中,應用程式指定*ValuePtr*緩衝區的長度 **(sizeof(***ValuePtr):*** **  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 驅動程式將始終返回具有輸出字串參數的任何函數的緩衝區長度參數中的位元組數,而不是字元數。  
  
 數據緩衝區長度僅適用於輸出緩衝區;驅動程式使用它們來避免寫入緩衝區的末尾。 但是,驅動程式僅在緩衝區包含可變長度數據(如字元或二進位數據)時檢查數據緩衝區長度。 如果緩衝區包含固定長度數據(如整數或日期結構),則驅動程式將忽略數據緩衝區長度,並假定緩衝區足夠大以容納數據;如果緩衝區大小,則驅動程式將忽略數據緩衝區長度,並假定緩衝區足夠大,足以保存數據。也就是說,它永遠不會截截固定長度的數據。 因此,應用程式為固定長度數據分配足夠大的緩衝區非常重要。  
  
 當出現非資料輸出字串的截斷(例如為**SQLGetCursorName**傳回的游標名稱)時,緩衝區長度參數中返回的長度是可能的最大字元長度。  
  
 輸入緩衝區不需要數據緩衝區長度,因為驅動程式不寫入這些緩衝區。  
  
 此章節包含下列主題。  
  
-   [使用長度/指示器值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
-   [資料長度、緩衝區長度和截斷](../../../odbc/reference/develop-app/data-length-buffer-length-and-truncation.md)  
  
-   [字元資料和 C 字串](../../../odbc/reference/develop-app/character-data-and-c-strings.md)
