---
description: INSERT 陳述式限制
title: INSERT 語句限制 |Microsoft Docs
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
ms.openlocfilehash: 71364b7972fa9d6a0ae6a48909f7c840830ff3eb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449480"
---
# <a name="insert-statement-limitations"></a>INSERT 陳述式限制
如果插入資料太長而無法放入資料行，則會在右側截斷插入的資料，而不會發出警告。  
  
 如果嘗試插入的值超出資料行資料類型的範圍，則會將 Null 插入資料行中。  
  
 使用 dBASE、Microsoft Excel、Paradox 或 Textdriver 時，在資料行中插入長度為零的字串實際上會插入 Null。  
  
 使用 Microsoft Excel 驅動程式時，如果將空字串插入資料行中，則空字串會轉換為 Null。在 WHERE 子句中使用空字串執行的搜尋 SELECT 語句，在該資料行上將無法成功。  
  
 在兩種情況下，Paradox 驅動程式無法更新資料表：  
  
-   當資料表上未定義唯一索引時。 這對空白資料表而言並不是如此，即使資料表上未定義唯一索引，也可以使用單一資料列進行更新。 如果在沒有唯一索引的空白資料表中插入單一資料列，則應用程式無法在插入單一資料列之後，建立唯一索引或插入其他資料。  
  
-   如果未執行 Borland 資料庫引擎，則只允許在 Paradox 資料表上使用 read 和 append 語句。  
  
 使用文字驅動程式時，系統會在固定長度的檔案中以空白填補的字串表示 Null 值，但以分隔的檔案中沒有空格表示。 例如，在包含三個欄位的下列資料列中，第二個欄位為 Null 值：  
  
```  
"Smith:,, 123  
```  
  
 使用文字驅動程式時，所有的資料行值都可以使用開頭的空格填補。 任何資料列的長度必須小於或等於65543個位元組。
