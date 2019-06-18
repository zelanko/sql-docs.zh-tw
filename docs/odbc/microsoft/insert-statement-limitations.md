---
title: INSERT 陳述式限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, INSERT statement limitations
- INSERT statement limitations [ODBC]
- truncation of data [ODBC]
ms.assetid: dea05698-527a-41ab-8729-bbed85556185
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26d4be96ca4dabebd93ee96e2888e18d39257412
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62471823"
---
# <a name="insert-statement-limitations"></a>INSERT 陳述式限制
如果太長而無法放入資料行，插入的資料會截斷在右側，而不發出警告。  
  
 嘗試插入超過資料行的資料類型範圍的值將會導致要插入到資料行的 NULL。  
  
 DBASE、 Microsoft Excel、 Paradox、 或 Textdriver 使用時，長度為零的字串插入資料行實際插入 null 值改為。  
  
 使用 Microsoft Excel 驅動程式時，如果空字串插入資料行，則為空字串會轉換成 null 值;搜尋的 SELECT 陳述式，會用 WHERE 子句中的空字串執行在該資料行，將會失敗。  
  
 資料表不是由兩個情況下 Paradox 驅動程式可更新的：  
  
-   當資料表上未定義唯一索引。 這不適用於空的資料表，可以更新單一資料列中，即使未在資料表上定義唯一索引。 若沒有唯一索引的空白資料表中插入單一資料列，應用程式無法建立唯一索引，或在插入單一資料列之後插入額外的資料。  
  
-   如果未實作 Borland Database Engine，只能讀取和附加 Paradox 資料表上允許使用陳述式。  
  
 使用文字驅動程式時，NULL 值都由固定長度的檔案中的空白填補字串，但都由不含空格分隔的檔案中。 例如，在包含三個欄位的下列資料列，第二個欄位是 NULL 值：  
  
```  
"Smith:,, 123  
```  
  
 使用文字驅動程式時，所有資料行值可以被填補空格。 任何資料列的長度必須小於或等於 65,543 個位元組。
