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
ms.openlocfilehash: 93cf744cf105762fb90a92049d6698e67a19d58c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68139001"
---
# <a name="identifier-arguments"></a>識別碼引數
如果識別碼引數中的字串是以引號括住，驅動程式會移除開頭和尾端空白，並將字串逐字地視為在引號內。 如果字串未加上引號，驅動程式會移除尾端空白，並將字串折迭為大寫。 除非引數是目錄名稱，而且不支援目錄，否則將 identifier 引數設定為 null 指標會傳回 SQL_ERROR 和 SQLSTATE HY009 （null 指標的用法無效）。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，則會將這些引數視為識別碼引數。 在此情況下，底線（_）和百分比符號（%）會被視為實際的字元，而不是搜尋模式字元。 視引數而定，如果此屬性設定為 SQL_FALSE，則會將這些引數視為一般引數或模式引數。  
  
 雖然包含特殊字元的識別碼必須括在 SQL 語句中，但在當做目錄函式引數傳遞時，不能加上引號，因為傳遞至目錄函式的引號字元會以字面方式轉譯。 例如，假設識別碼引號字元（它是驅動程式特有的，並透過**SQLGetInfo**傳回）是雙引號（"）。 第一次呼叫**SQLTables**時，會傳回包含 [應付帳款] 資料表相關資訊的結果集，而第二個呼叫則會傳回「帳戶應付」資料表的相關資訊，這可能不是預期的情況。  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 引號識別碼是用來區分 true 資料行名稱與相同名稱的虛擬資料行，例如 Oracle 中的 ROWID。 如果在目錄函數的引數中傳遞 "ROWID"，函式會使用 ROWID 虛擬資料行（如果存在的話）。 如果虛擬資料行不存在，函數將會使用「ROWID」資料行。 如果在目錄函數的引數中傳遞 ROWID，此函數將會使用 ROWID 資料行。  
  
 如需引號識別碼的詳細資訊，請參閱[引號識別碼](../../../odbc/reference/develop-app/quoted-identifiers.md)。
