---
title: 識別項引數 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- identifier arguments [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], identifier
ms.assetid: b9de003f-cb49-4dec-b528-14a5b8ff12bd
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5cbeb7d146cf82a752beed19befca0cf52eeb2ab
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="identifier-arguments"></a>識別項引數
如果已加上引號的字串識別項引數中，驅動程式會移除開頭和尾端空白，並將常值引號內的字串。 如果字串不加上引號，驅動程式會移除尾端的空白和摺疊成大寫的字串。 設定識別項引數為 null 指標會傳回 SQL_ERROR 並 SQLSTATE HY009 （使用無效的 null 指標），除非引數是目錄名稱，而且不支援類別目錄。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE，這些引數會被視為識別碼引數。 在此情況下，底線 (_) 百分比符號 （%） 會視為與實際的字元不是搜尋模式的字元。 這些引數會被視為一般引數或模式引數，根據的引數，如果此屬性設為 SQL_FALSE。  
  
 雖然包含特殊字元的識別項必須在 SQL 陳述式加上引號，它們必須不加上引號做為目錄函式引數，傳遞時因為傳遞至型錄函式的引號字元會解譯為常值。 例如，假設識別項引號字元 (這是驅動程式專屬，傳回透過**SQLGetInfo**) 是雙引號 （"）。 第一次呼叫**SQLTables**傳回的結果集包含 Accounts Payable 資料表的相關資訊，而第二個呼叫會傳回"Accounts Payable"資料表，可能不是想要的結果的相關資訊。  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 引號的識別碼用來區別相同的名稱，例如 ROWID 在 Oracle 中的虛擬資料行，則為 true 的資料行名稱。 如果 「 ROWID"傳入目錄函數的引數，函式將使用 ROWID 虛擬資料行若有的話。 虛擬資料行不存在，如果函式會使用"ROWID 」 資料行。 如果 ROWID 傳入目錄函數的引數，函式會使用 ROWID 資料行。  
  
 如需引號識別項的詳細資訊，請參閱[引號識別項](../../../odbc/reference/develop-app/quoted-identifiers.md)。
