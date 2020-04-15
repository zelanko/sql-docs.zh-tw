---
title: 插入敘述限制 :微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f903f15ec13baa28a789891c1527dc742daa68ac
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300000"
---
# <a name="insert-statement-limitations"></a>INSERT 陳述式限制
如果插入的數據太長,無法放入列,則在右側截斷數據,恕不另行通知。  
  
 嘗試插入欄資料類型範圍外的值會導致將 NULL 插入到列中。  
  
 當使用 dBASE、Microsoft Excel、悖論或文本驅動程式時,將零長度字串插入列實際上插入 NULL。  
  
 使用 Microsoft Excel 驅動程式時,如果將空字串插入到列中,則空字串將轉換為 NULL;如果將空字串插入到列中,則將空字串轉換為 NULL。使用 WHERE 子句中的空字串執行的搜索 SELECT 語句將不會在該列上成功。  
  
 在以下兩個條件下,悖論驅動程式無法啟動表:  
  
-   未在表上定義唯一索引時。 對於空表,情況並非如此,即使表上未定義唯一索引,也可以用單個行進行更新。 如果單行插入於沒有唯一索引的空表中,則應用程式無法創建唯一索引或在插入單行后插入其他數據。  
  
-   如果未實現 Borland 資料庫引擎,則僅允許在 Paradox 表上讀取和追加語句。  
  
 使用 Text 驅動程式時,NULL 值由固定長度檔中的空白填充字串表示,但由分隔檔中的空格表示。 例如,在包含三個字段的行中,第二個字段是 NULL 值:  
  
```  
"Smith:,, 123  
```  
  
 使用文本驅動程式時,可以使用前導空格填充所有列值。 任何行的長度必須小於或等於65,543位元組。
