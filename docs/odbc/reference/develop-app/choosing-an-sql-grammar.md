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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2ca9911d3c88f2f540ff1332d77a2e1ebc6a4942
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299158"
---
# <a name="choosing-an-sql-grammar"></a>選擇 SQL 文法
在建立 SQL 語句時，第一個要做的決定是要使用哪一個文法。 除了可從各種標準本文取得的文法，例如開放式群組、ANSI 和 ISO，幾乎每個 DBMS 廠商都會定義自己的文法，而每個都有不同的標準。  
  
 [附錄 C： Sql 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)描述所有 ODBC 驅動程式都必須支援的最低 SQL 文法。 此文法是 SQL-92 進入層級的子集。 驅動程式可能會支援額外的文法，以符合 SQL-92 所定義的中繼、完整或 FIPS 127-2 轉換層級。 如需詳細資訊，請參閱附錄 C： SQL 文法和 SQL-92 中的[Sql 最低文法](../../../odbc/reference/appendixes/sql-minimum-grammar.md)。  
  
 附錄 C 也會針對常用的語言功能（例如外部聯結）定義包含非 SQL-92 文法所涵蓋之標準文法的*逸出序列*。 如需詳細資訊，請參閱本節稍後的附錄 C： SQL 文法和[Escape 序列](../../../odbc/reference/develop-app/escape-sequences.md)中的[ODBC Escape 序列](../../../odbc/reference/appendixes/odbc-escape-sequences.md)。  
  
 所選擇的文法會影響驅動程式處理語句的方式。 驅動程式必須將 SQL-92 SQL 和 ODBC 定義的逸出序列修改為 DBMS 特定的 SQL。 因為大部分的 SQL 文法都是以一或多個不同的標準為基礎，所以大部分的驅動程式幾乎不需要任何工作就能滿足這項需求。 通常只會包含搜尋 ODBC 所定義的 escape 序列，並以 DBMS 特定文法來取代它們。 當驅動程式發現文法無法辨識時，它會假設文法是 DBMS 專屬的，並在不修改資料來源的情況下傳遞 SQL 語句來執行。  
  
 因此，實際上有兩個要使用的文法選擇： SQL-92 文法（和 ODBC 轉義順序）和 DBMS 特定文法。 在這兩個中，只有 SQL-92 文法可互通，因此所有互通的應用程式都應該使用它。 無法互通的應用程式可以使用 SQL-92 文法或 DBMS 特定的文法。 DBMS 特定的文法有兩個優點：它們可以利用 SQL-92 未涵蓋的任何功能，而且速度會更快，因為驅動程式不需要修改它們。 您可以藉由設定 SQL_ATTR_NOSCAN 語句屬性來部分強制執行後者的功能，這會停止驅動程式搜尋並取代 escape 序列。  
  
 如果使用的是 SQL-92 文法，應用程式可以藉由呼叫**SQLNativeSql**來探索驅動程式修改的方式。 這在偵錯工具時通常很有用。 **SQLNativeSql**會接受 SQL 語句，並在驅動程式修改它之後傳回它。 因為此函式是在核心介面一致性層級中，所以所有驅動程式都支援此功能。
