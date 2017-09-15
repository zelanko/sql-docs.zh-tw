---
title: "INSERT 陳述式的限制 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC SQL grammar, INSERT statement limitations
- INSERT statement limitations [ODBC]
- truncation of data [ODBC]
ms.assetid: dea05698-527a-41ab-8729-bbed85556185
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f9233e7582083ba08fb1239120e63db819b8724b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="insert-statement-limitations"></a>INSERT 陳述式的限制
如果太長而無法放入資料行，插入的資料會截斷在右側，而不發出警告。  
  
 嘗試插入值超出資料行的資料類型，這個值會造成插入資料行的 NULL。  
  
 使用 dBASE、 Microsoft Excel、 Paradox 或 Textdriver 時，將插入的資料行的零長度字串實際插入 null 值改為。  
  
 使用 Microsoft Excel 驅動程式時，如果空字串插入資料行，則為空字串會轉換成 null 值;搜尋 SELECT 陳述式執行時以空字串的 WHERE 子句中該資料行上，將會失敗。  
  
 資料表不是由兩個情況下 Paradox 驅動程式可更新的：  
  
-   當資料表上未定義唯一索引。 這不適用於空的資料表，即使未在資料表上定義唯一索引可更新的單一資料列。 若在單一資料列插入空的資料表沒有唯一索引中，應用程式無法建立唯一索引，或在插入單一資料列之後插入額外的資料。  
  
-   如果未實作 Borland Database Engine，只能讀取和附加 Paradox 資料表上允許陳述式。  
  
 使用文字驅動程式時，NULL 值都由固定長度檔案中的空白填補字串，但會以分隔檔案中沒有任何空格。 例如，下列資料列包含三個欄位，在第二個欄位是 NULL 值：  
  
```  
"Smith:,, 123  
```  
  
 使用文字驅動程式時，所有資料行值可以以填補前置空格。 任何資料列的長度必須小於或等於 65,543 個位元組。
