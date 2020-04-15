---
title: 選擇敘述限制 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, SELECT statement limitations
- SELECT statement limitations [ODBC]
ms.assetid: c6b05955-f8fd-4706-a1a7-a8dbd74870c2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d91e93076a67287cbbd2b64b2ad0d6414a0aea6d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300918"
---
# <a name="select-statement-limitations"></a>SELECT 陳述式限制
聚合函數列不能與 SELECT 語句中的非聚合列混合。  
  
 具有 GROUP BY 子句的 SELECT 語句的選擇清單只能具有來自 GROUP BY 子句或集函數的運算式。  
  
 不支援在包含 GROUP BY 子句的 SELECT 語句中使用星號(以選擇所有列)。 必須指定要選擇的列的名稱。  
  
 不支援在 SELECT 語句中使用垂直條。 如果需要引用包含垂直條的數據值,請使用 SELECT 語句中的參數。  
  
 在 SELECT 語句中使用列別名時,「as」一詞必須位於別名之前。 例如,"SELECT col1 作為 a 從 b"。 如果沒有"as",語句將返回錯誤。  
  
 如果在 SELECT 語句中輸入了不正確的列名稱,則傳回 SQLSTATE 07001 錯誤「錯誤參數數」,而不是 SQLSTATE S0022 錯誤「未找到列」。  
  
 使用 Microsoft Excel 驅動程式時,如果將空字串插入到列中,則空字串將轉換為 NULL;如果將空字串插入到列中,則將空字串轉換為 NULL。使用 WHERE 子句中的空字串執行的搜索 SELECT 語句將不會在該列上成功。
