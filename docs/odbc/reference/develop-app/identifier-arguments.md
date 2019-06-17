---
title: 識別碼引數 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- identifier arguments [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], identifier
ms.assetid: b9de003f-cb49-4dec-b528-14a5b8ff12bd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 156dfaf5c6a6a4ec06a0c96b5f726383cba32ba6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62447547"
---
# <a name="identifier-arguments"></a>識別碼引數
如果已加上引號的識別碼引數的字串，驅動程式會移除開頭和尾端空白，並將解譯為常值的引號內的字串。 如果字串不加上引號，驅動程式會移除尾端的空白和摺疊成大寫的字串。 識別碼引數設定為 null 指標會傳回 SQL_ERROR，而且 SQLSTATE HY009 （使用無效的 null 指標），除非引數是類別目錄名稱，而且不支援目錄。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE，這些引數會被視為識別碼引數。 在此情況下，底線 (_) 和百分比符號 （%）將會視為實際的字元不是搜尋模式字元。 這些引數會被視為一般引數或模式引數，根據引數，如果此屬性設定為 SQL_FALSE。  
  
 雖然包含特殊字元的識別項必須加上引號，SQL 陳述式中，它們必須不加上引號時目錄函式引數傳遞，因為傳遞至目錄函式的引號字元會解譯為常值。 例如，假設識別項引號字元 (這是由特定驅動程式，以及透過傳回**SQLGetInfo**) 是雙引號 （"）。 第一次呼叫**SQLTables**傳回的結果集包含 Accounts Payable 資料表的相關資訊，而第二次呼叫會傳回"Accounts Payable"資料表，也就是可能不預期目的的相關資訊。  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 引號識別項用來區別相同的名稱，例如 ROWID 在 Oracle 中的虛擬資料行，則為 true 的資料行名稱。 如果目錄函式的引數中傳遞 「 ROWID"，則此函式可使用 ROWID 虛擬資料行若有的話。 如果虛擬資料行不存在，函式會使用"ROWID 」 資料行中。 如果目錄函式的引數中傳遞 ROWID，則函式會使用 ROWID 資料行中。  
  
 如需引號識別項的詳細資訊，請參閱[加上引號的識別項](../../../odbc/reference/develop-app/quoted-identifiers.md)。
