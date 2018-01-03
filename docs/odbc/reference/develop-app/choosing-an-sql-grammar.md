---
title: "選擇 SQL 文法 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], SQL grammar
- SQL grammar [ODBC], selecting
ms.assetid: 4e0d189b-e407-47e0-92a9-f9982230dd0e
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6eedc2466842d922e1b10445500f05ad904d1a0b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="choosing-an-sql-grammar"></a>選擇 SQL 文法
當建構 SQL 陳述式的第一個決策是要使用的文法。 除了可從各種標準內文，例如 Open Group、 ANSI 和 ISO 文法幾乎 DBMS 廠商定義自己的文法，其中每個稍有不同於標準。  
  
 [附錄 c: SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)，描述所有的 ODBC 驅動程式必須支援的最小 SQL 文法。 此文法是 sql-92 的項目層級的子集。 驅動程式可能支援其他以符合中繼、 完整或由 SQL 92 FIPS 127-2 過渡期的層級定義的文法。 如需詳細資訊，請參閱[SQL 最小值文法](../../../odbc/reference/appendixes/sql-minimum-grammar.md)附錄 c: SQL 文法和 sql-92 中。  
  
 附錄 C 也會定義*逸出序列*包含通常可用的語言功能，例如外部聯結中，標準文法，未涵蓋的 SQL 92 文法。 如需詳細資訊，請參閱[ODBC 逸出序列](../../../odbc/reference/appendixes/odbc-escape-sequences.md)附錄 c: SQL 文法中, 和[逸出序列](../../../odbc/reference/develop-app/escape-sequences.md)稍後這一節。  
  
 文法會選擇會影響此驅動程式如何處理陳述式。 SQL 92 SQL 和特定 DBMS 的 sql ODBC 定義的逸出序列，則必須修改驅動程式。 由於大部分的 SQL 文法會依據一或多個各種標準，因此大部分的驅動程式會執行少量或沒有符合此需求的工作。 它通常只包含定義的逸出序列搜尋 ODBC，並將其取代為特定 DBMS 的文法。 當驅動程式遇到無法辨識的文法時，它會假設文法 DBMS 專屬，並且將傳送的 SQL 陳述式，而不需執行的資料來源的修改。  
  
 因此，其實文法的要使用的兩個選擇： sql-92 文法 （和 ODBC 逸出序列） 和特定 DBMS 的文法。 兩個 SQL 92 文法是互通性最佳、，因此所有互通的應用程式應該使用這個方法。 並不互通的應用程式可以使用 sql-92 文法或特定 DBMS 的文法。 DBMS 專屬文法中有兩個優點： 其可以利用任何 sql-92，未涵蓋的功能，而且它們投資速度會因為驅動程式不需要加以修改。 後者的功能可以藉由設定 SQL_ATTR_NOSCAN 陳述式屬性，它會阻止驅動程式搜尋和取代逸出序列部分強制執行。  
  
 如果使用 sql-92 文法時，應用程式可以探索如何修改驅動程式透過呼叫**SQLNativeSql**。 偵錯應用程式時，這是很有用。 **SQLNativeSql**接受 SQL 陳述式並傳回它之後，驅動程式已修改過它。 此函式是核心介面的一致性層級中，因為它支援所有的驅動程式。
