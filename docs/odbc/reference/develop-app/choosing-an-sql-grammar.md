---
title: 選擇 SQL 文法 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], SQL grammar
- SQL grammar [ODBC], selecting
ms.assetid: 4e0d189b-e407-47e0-92a9-f9982230dd0e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 670ed0adbbd5ad993af0942d492ee19f75fa9628
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63026578"
---
# <a name="choosing-an-sql-grammar"></a>選擇 SQL 文法
首先要建構 SQL 陳述式時決定是要使用的文法。 除了可從各種不同的標準組織，例如 Open Group、 ANSI 和 ISO、 文法幾乎每個 DBMS 廠商會定義它自己的文法，其中每個標準略有不同。  
  
 [附錄 C：SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)，告訴您所有的 ODBC 驅動程式必須支援的最小 SQL 文法。 此文法是 SQL-92 的項目層級的子集。 驅動程式可能支援其他符合中繼、 完整 或 FIPS 127-2 過渡期的層級定義的 SQL-92 的文法。 如需詳細資訊，請參閱 < [SQL 最小文法](../../../odbc/reference/appendixes/sql-minimum-grammar.md)附錄 c:SQL 文法和 SQL-92。  
  
 附錄 C 也會定義*逸出序列*包含常用的語言功能，例如外部聯結中，標準的文法，未涵蓋的 SQL-92 文法。 如需詳細資訊，請參閱 < [ODBC 逸出序列](../../../odbc/reference/appendixes/odbc-escape-sequences.md)附錄 c:SQL 文法，以及[逸出序列](../../../odbc/reference/develop-app/escape-sequences.md)稍後這一節。  
  
 文法會選擇會影響此驅動程式如何處理陳述式。 SQL-92 SQL 和特定 DBMS 的 SQL ODBC 定義的逸出序列，則必須修改驅動程式。 由於大部分的 SQL 文法會依據一或多個各種標準，因此大部分的驅動程式就會執行幾乎沒有任何工作，以符合此需求。 它通常只包含搜尋所定義的逸出序列的 ODBC 和它們取代為特定 DBMS 的文法。 當驅動程式遇到它無法辨識的文法時，它會假設文法的 DBMS 特定作業，並傳遞不需要修改資料來源，以便執行的 SQL 陳述式。  
  
 因此，實際上有兩個選擇的文法，若要使用： SQL-92 文法 （和 ODBC 逸出序列） 及特定 DBMS 的文法。 兩個 SQL-92 文法是互通性最佳、 的因此互通性的所有應用程式應該使用它。 不具互通性的應用程式可以使用 SQL-92 文法或特定 DBMS 的文法。 DBMS 專屬文法會有兩個優點：它們可以利用任何未涵蓋的 SQL-92 的功能，它們是稍微更快，因為驅動程式不需要加以修改。 後者的功能可以藉由 SQL_ATTR_NOSCAN 陳述式屬性，這會停止將驅動程式搜尋和取代逸出序列從部分強制執行。  
  
 如果使用 SQL-92 文法，則應用程式可以探索如何修改驅動程式透過呼叫**SQLNativeSql**。 偵錯應用程式時，這是很有用。 **SQLNativeSql**接受 SQL 陳述式，並傳回它之後，驅動程式已修改過它。 此函式是在核心介面一致性層級，因為它支援所有的驅動程式。
