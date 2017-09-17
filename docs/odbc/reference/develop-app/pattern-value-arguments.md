---
title: "模式值引數 |Microsoft 文件"
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
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], pattern value
- pattern value arguments [ODBC]
ms.assetid: 1d3f0ea6-87af-4836-807f-955e7df2b5df
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6935d0e94b931451aba5940db60877c8443df7c4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="pattern-value-arguments"></a>模式值引數
在目錄中的某些引數函式，例如*TableName*引數中的**SQLTables**，接受搜尋模式。 這些引數接受搜尋模式如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_FALSE。它們是這個屬性設定為 SQL_TRUE，如果不接受之搜尋模式的識別項引數。  
  
 搜尋模式的字元如下：  
  
-   底線 (_)，表示任何單一字元。  
  
-   百分比符號 （%），它代表任何字元零或多個序列。  
  
-   逸出字元，是特定驅動程式，用來加上了底線，百分比簽署，並做為常值的逸出字元。 如果逸出字元之前的非特殊字元，逸出字元會有任何特殊的意義。 如果逸出字元之前的特殊字元，它會逸出特殊字元。 "\A"會視為兩個字元，例如，"\\"和"a"，但"\\%」 會視為非特殊的單一字元"%"。  
  
 逸出字元會擷取中的 SQL_SEARCH_PATTERN_ESCAPE 選項**SQLGetInfo**。 它必須在任何底線、 百分比符號或逸出字元之前接受要包含該字元作為常值的搜尋模式的引數。 下表顯示範例。  
  
|搜尋模式|Description|  
|--------------------|-----------------|  
|%A%|所有包含字母 A 的識別項|  
|ABC_|所有四個字元的識別項開頭為 ABC|  
|ABC\\_|ABC_，假設逸出字元的識別項是反斜線 (\\)|  
|\\\\%|反斜線為開頭的所有識別項 (\\)，假設逸出字元是反斜線|  
  
 特殊必須小心來逸出接受搜尋模式的引數中的搜尋模式字元。 特別是針對底線的字元，常用於識別項。 在應用程式中常見的錯誤是擷取一個目錄函式的值，並將該值傳遞至另一個類別目錄函式中搜尋 pattern 引數。 例如，假設應用程式擷取 MY_TABLE 從結果集的資料表名稱**SQLTables**並傳遞此**SQLColumns**擷取 MY_TABLE 中的資料行清單。 而不是資料行取得 MY_TABLE，應用程式會取得符合搜尋模式 MY_TABLE，例如 MY_TABLE、 MY1TABLE、 MY2TABLE，等等的所有資料表的資料行。  
  
> [!NOTE]  
>  ODBC 2。*x*驅動程式不會支援中的搜尋模式*CatalogName*引數中的**SQLTables**。 ODBC 3*.x*如果 SQL_ATTR_ ODBC_VERSION 環境屬性設定為 sql_ov_odbc3 時，驅動程式會接受此引數中的搜尋模式; 它們不接受此引數中的搜尋模式如果設定為 SQL_OV_ODBC2。  
  
 傳遞的 null 指標來搜尋 pattern 引數不會限制該引數; 搜尋也就是 null 指標，搜尋模式 %（任何字元） 是相等的。 不過，長度為零的搜尋模式-也就是字串的長度為零的有效指標，會比對空的字串 ("")。
