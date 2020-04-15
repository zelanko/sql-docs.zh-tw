---
title: 模式值參數 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], pattern value
- pattern value arguments [ODBC]
ms.assetid: 1d3f0ea6-87af-4836-807f-955e7df2b5df
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0b8e7b7de64d8051118089a54cf14eb45dc96f74
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282378"
---
# <a name="pattern-value-arguments"></a>模式值引數
目錄函數中的某些參數(如**SQLTables**中的*表名稱*參數)接受搜尋模式。 如果SQL_ATTR_METADATA_ID語句屬性設置為SQL_FALSE,則這些參數接受搜索模式;如果此屬性設置為SQL_TRUE,它們是不接受搜索模式的標識符參數。  
  
 搜尋模式字元為:  
  
-   表示任何單個字元的下劃線 (*)。  
  
-   百分比符號 (%),表示任何零個或多個字串序列。  
  
-   轉義字元,它是特定於驅動程式的,用於將下劃線、百分比符號和轉義字元作為文本。 如果轉義字元位於非特殊字元之前,則轉義字元沒有特殊含義。 如果轉義字元位於特殊字元前面,則它將轉義特殊字元。 例如,"\a"將被視為兩個字元""\\和"a",但"%"\\將被視為非特殊單個字元"%"。  
  
 轉義符使用**SQLGetInfo**中的SQL_SEARCH_PATTERN_ESCAPE選項進行檢索。 它必須位於接受搜索模式的參數中的任何下劃線、百分比符號或轉義字元之前,才能將該字元作為文本包含。 下表中顯示了示例。  
  
|搜尋模式|描述|  
|--------------------|-----------------|  
|%A%|包含字母 A 的所有識別碼|  
|ABC_|所有四個字元識別碼以 ABC 開頭|  
|ABC\\||識別符ABC_,假設轉義字元是反斜杠\\( )|  
|\\\\%|假定轉義字元是反斜杠,\\則以反斜杠 () 開頭的所有識別子|  
  
 必須特別注意在接受搜索模式的參數中轉義搜索模式字元。 對於標識符中常用的下劃線字元尤其如此。 應用程式中的一個常見錯誤是從一個目錄函數中檢索值,並將該值傳遞給另一個目錄函數中的搜索模式參數。 例如,假設應用程式從**SQLTables**的結果集中檢索表名稱MY_TABLE並將其傳遞給**SQLColumns**以檢索MY_TABLE中的列清單。 應用程式將獲取與搜索模式匹配的所有表的列,MY_TABLE(如MY_TABLE、MY1TABLE、MY2TABLE等)而不是獲取MY_TABLE列。  
  
> [!NOTE]
>  ODBC 2.*x*驅動程式不支援**SQLTables**中的*目錄名稱*參數中的搜尋模式。 如果SQL_ATTR_ODBC_VERSION環境屬性設置為SQL_OV_ODBC3,則 ODBC 3 *.x*驅動程式在此參數中接受搜索模式;如果搜索模式設置為SQL_OV_ODBC2,則不接受此參數中的搜索模式。  
  
 將空指標傳遞給搜尋模式參數不會限制該參數的搜索;因此,將空指標傳遞給搜尋模式參數。也就是說,空指標和搜尋模式% (任何字元) 是等效的。 但是,零長度搜索模式(即指向長度為零的字串的有效指標)僅匹配空字串 ("")。
