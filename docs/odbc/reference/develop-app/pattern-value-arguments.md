---
description: 模式值引數
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a014c63c7fff6b82bbdd26d9fd5b4391c29d0ce2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465750"
---
# <a name="pattern-value-arguments"></a>模式值引數
目錄函式中的部分引數，例如**SQLTables**中的*TableName*引數，接受搜尋模式。 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_FALSE，這些引數會接受搜尋模式;如果這個屬性設定為 SQL_TRUE，則它們是不接受搜尋模式的識別碼引數。  
  
 搜尋模式字元包括：  
  
-   底線 (_) ，代表任何單一字元。  
  
-   百分比符號 (% ) ，代表零或多個字元的任何序列。  
  
-   Escape 字元，它是驅動程式專用的，用來包含底線、百分比符號和 escape 字元做為常值。 如果 escape 字元在非特殊字元之前，則 escape 字元沒有特殊意義。 如果 escape 字元在特殊字元之前，則會將特殊字元轉義。 例如，"\a" 會視為兩個字元，" \\ " 和 "a"，但 " \\ %" 會被視為非特殊的單一字元 "%"。  
  
 使用 **SQLGetInfo**中的 SQL_SEARCH_PATTERN_ESCAPE 選項來抓取 escape 字元。 它必須在接受搜尋模式的引數中的任何底線、百分比符號或 escape 字元之前，以將該字元包含為常值。 下表顯示範例。  
  
|搜尋模式|描述|  
|--------------------|-----------------|  
|的|所有包含字母 A 的識別碼|  
|ABC_|以 ABC 開頭的四個字元識別碼|  
|ABC \\ _|ABC_ 的識別碼，假設 escape 字元是反斜線 (\\) |  
|\\\\%|所有以反斜線 (開頭的識別碼 \\ 都會) ，假設 escape 字元是反斜線。|  
  
 請特別注意，在接受搜尋模式的引數中，將搜尋模式字元換用。 這特別適用于底線字元，通常用於識別碼中。 應用程式中常見的錯誤是從一個目錄函式取出值，並將該值傳遞給另一個目錄函數中的搜尋模式引數。 例如，假設應用程式從 **SQLTables** 的結果集抓取資料表名稱 MY_TABLE，並將此名稱傳遞至 **SQLColumns** ，以取出 MY_TABLE 中的資料行清單。 應用程式不會取得 MY_TABLE 的資料行，而是會取得符合搜尋模式 MY_TABLE 的所有資料表的資料行，例如 MY_TABLE、MY1TABLE、MY2TABLE 等等。  
  
> [!NOTE]
>  ODBC 2。*x*驅動程式不支援在**SQLTables**的*CatalogName*引數中搜尋模式。 如果 SQL_ATTR_ ODBC_VERSION 環境屬性設定為 SQL_OV_ODBC3，ODBC*3.x 驅動程式* 會在這個引數中接受搜尋模式;如果設定為 SQL_OV_ODBC2，則不接受此引數中的搜尋模式。  
  
 將 null 指標傳遞給搜尋模式引數不會限制搜尋該引數;也就是說，null 指標和搜尋模式% (任何) 的字元都相等。 不過，零長度的搜尋模式，也就是長度為零之字串的有效指標，只符合空字串 ( "" ) 。
