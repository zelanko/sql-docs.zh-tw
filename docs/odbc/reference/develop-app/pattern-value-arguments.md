---
title: 模式值引數 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 53c091fd0b7a6cfdf390997fb5163fbc9d98e18c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68023352"
---
# <a name="pattern-value-arguments"></a>模式值引數
目錄函式中的某些引數（例如**SQLTables**中的*TableName*引數）接受搜尋模式。 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_FALSE，這些引數會接受搜尋模式;如果此屬性設定為 SQL_TRUE，它們就是不接受搜尋模式的識別碼引數。  
  
 搜尋模式字元如下：  
  
-   表示任何單一字元的底線（_）。  
  
-   百分比符號（%），代表零或多個字元的任何序列。  
  
-   針對特定驅動程式，用來包含底線、百分比符號和 escape 字元做為常值的換用字元。 如果逸出字元在非特殊字元前面，則 escape 字元沒有特殊意義。 如果逸出字元在特殊字元之前，則會將特殊字元轉義。 例如，"\a" 會被視為兩個字元 "\\" 和 "a"，但 "\\%" 會被視為非特殊的單一字元 "%"。  
  
 在**SQLGetInfo**中，會使用 SQL_SEARCH_PATTERN_ESCAPE 選項來抓取 escape 字元。 它必須在接受搜尋模式的引數中，加上任何底線、百分比符號或 escape 字元，以包含該字元做為常值。 下表顯示範例。  
  
|搜尋模式|描述|  
|--------------------|-----------------|  
|為|包含字母 A 的所有識別碼|  
|ABC_|開頭為 ABC 的所有四個字元識別碼|  
|ABC\\_|ABC_ 的識別碼，假設 escape 字元是反斜線（\\）|  
|\\\\%|所有以反斜線（\\）開頭的識別碼，假設 escape 字元是反斜線|  
  
 必須特別小心，才能在接受搜尋模式的引數中，以轉義搜尋模式字元。 這特別適用于在識別碼中常用的底線字元。 應用程式中常見的錯誤是從一個目錄函數抓取值，並將該值傳遞至另一個目錄函式中的搜尋模式引數。 例如，假設應用程式會從**SQLTables**的結果集抓取資料表 MY_TABLE 名稱，並將它傳遞至**SQLColumns** ，以取得 MY_TABLE 中的資料行清單。 應用程式會取得符合搜尋模式 MY_TABLE 的所有資料表的資料行，例如 MY_TABLE、MY1TABLE、MY2TABLE 等等，而不是取得 MY_TABLE 的資料行。  
  
> [!NOTE]
>  ODBC 2。*x*驅動程式不支援**SQLTables**中*CatalogName*引數的搜尋模式。 如果 SQL_ATTR_ ODBC_VERSION 環境屬性設定為 SQL_OV_ODBC3，ODBC*3.x 驅動程式*會接受此引數中的搜尋模式。如果設定為 SQL_OV_ODBC2，則不接受此引數中的搜尋模式。  
  
 將 null 指標傳遞至搜尋模式引數，並不會限制搜尋該引數;也就是 null 指標和搜尋模式% （任何字元）是相等的。 但是，長度為零的字串的有效指標，即為零長度的搜尋模式，只符合空字串（""）。
