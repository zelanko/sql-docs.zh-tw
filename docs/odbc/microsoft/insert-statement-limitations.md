---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1676af6216ac703e9a8976951ec2888b9e940b67
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085517"
---
# <a name="insert-statement-limitations"></a>INSERT 陳述式限制
插入的資料會在右側截斷，如果太長而無法放入資料行中，則不會發出警告。  
  
 嘗試插入超出資料行資料類型範圍的值，會導致將 Null 插入資料行。  
  
 使用 dBASE、Microsoft Excel、Paradox 或 Textdriver 時，將長度為零的字串插入資料行中，實際上會改為插入 Null。  
  
 使用 Microsoft Excel 驅動程式時，如果將空字串插入至資料行，則會將空字串轉換成 Null;在 WHERE 子句中使用空字串執行的搜尋 SELECT 語句將不會在該資料行上成功。  
  
 在兩個情況下，Paradox 驅動程式無法更新資料表：  
  
-   未在資料表上定義唯一索引時。 空白資料表的這種情況並不適用，即使資料表上未定義唯一索引，也可以使用單一資料列更新。 如果在沒有唯一索引的空白資料表中插入單一資料列，應用程式就無法在插入單一資料列之後，建立唯一的索引或插入其他資料。  
  
-   如果未執行 Borland 資料庫引擎，Paradox 資料表上只允許 read 和 append 語句。  
  
 使用文字驅動程式時，Null 值會由固定長度檔案中以空白填補的字串表示，但在分隔的檔案中不會以空格表示。 例如，在包含三個欄位的下列資料列中，第二個欄位是 Null 值：  
  
```  
"Smith:,, 123  
```  
  
 使用文字驅動程式時，所有的資料行值都可以填補開頭的空格。 任何資料列的長度都必須小於或等於65543個位元組。
