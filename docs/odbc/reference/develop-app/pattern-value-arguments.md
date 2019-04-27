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
manager: craigg
ms.openlocfilehash: 8f4a32d9ab637de5b52466cfcb628a57ff6c044b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62861724"
---
# <a name="pattern-value-arguments"></a>模式值引數
在目錄中的某些引數函式，例如*TableName*中的引數**SQLTables**，接受搜尋模式。 這些引數接受搜尋模式如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_FALSE。也就是如果這個屬性設定為 SQL_TRUE 不接受搜尋模式的識別項引數。  
  
 搜尋模式的字元如下：  
  
-   底線 (_)，這表示任何單一字元。  
  
-   百分比符號 （%），它代表任何零或多個字元序列。  
  
-   逸出字元，這是特定驅動程式，用來加上了底線，百分之登入，並做為常值的逸出字元。 如果逸出字元前面的非特殊字元，逸出字元會有任何特殊的意義。 如果逸出字元在之前的特殊字元，它會逸出特殊字元。 比方說，"\a"會被視為兩個字元，"\\"和"a"，但"\\%"會被視為非特殊的單一字元"%"。  
  
 逸出字元會擷取使用中的 SQL_SEARCH_PATTERN_ESCAPE 選項**SQLGetInfo**。 它必須在任何底線、 百分比符號或逸出字元之前接受搜尋模式，以包含該字元做為常值的引數。 下表顯示範例。  
  
|搜尋模式|描述|  
|--------------------|-----------------|  
|%A%|所有包含字母 A 的識別項|  
|ABC_|所有四個字元的識別項開頭為 ABC|  
|ABC\\_|ABC_，假設逸出字元的識別項是反斜線 (\\)|  
|\\\\%|所有的識別項開頭為反斜線 (\\)，假設逸出字元是反斜線|  
  
 特別小心來逸出接受搜尋模式的引數中的搜尋模式字元。 這特別適用於底線字元，這常用的識別項。 在應用程式中常見的錯誤是從一個目錄函式擷取值，並將該值傳遞至另一個目錄函式中的搜尋模式引數。 例如，假設應用程式擷取 MY_TABLE，從結果集的資料表名稱**SQLTables** ，並將此選項以傳遞**SQLColumns**擷取 MY_TABLE 中的資料行清單。 應用程式會取得符合搜尋模式 MY_TABLE，例如 MY_TABLE、 MY1TABLE、 MY2TABLE，等等的所有資料表的資料行而非資料行的 MY_TABLE。  
  
> [!NOTE]
>  ODBC 2。*x*驅動程式不支援中的搜尋模式*CatalogName*中的引數**SQLTables**。 ODBC 3 *.x*如果 SQL_ATTR_ ODBC_VERSION&AMP;LT 環境屬性設定為 sql_ov_odbc3 時，驅動程式會接受此引數中的搜尋模式; 他們不要接受這個引數中的搜尋模式，如果設定為 SQL_OV_ODBC2。  
  
 傳遞的 null 指標來搜尋模式引數不會限制該引數; 搜尋也就是 null 指標，搜尋模式 %（任何字元） 相等。 不過，長度為零搜尋模式-也就是長度為零的字串的有效指標-比對空字串 ("")。
