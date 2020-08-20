---
description: 選擇 SQL 文法
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
ms.openlocfilehash: 7936631c830d65d58e69d6cd77a728dfd8e664b0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461580"
---
# <a name="choosing-an-sql-grammar"></a>選擇 SQL 文法
在建立 SQL 語句時，首先要做的決定是要使用的文法。 除了各種標準主體（例如 Open Group、ANSI 和 ISO）所提供的文法之外，幾乎每個 DBMS 廠商都會定義自己的文法，而每個都有不同的標準。  
  
 [附錄 C： Sql 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)，描述所有 ODBC 驅動程式都必須支援的最小 SQL 文法。 此文法是 SQL-92 專案層級的子集。 驅動程式可能會支援其他文法，以符合 SQL-92 所定義的中繼、完整或 FIPS 127-2 過渡等級。 如需詳細資訊，請參閱附錄 C： SQL 文法中的 [Sql 最小文法](../../../odbc/reference/appendixes/sql-minimum-grammar.md) 和 sql-92。  
  
 附錄 C 也定義了包含一般可用語言功能（例如外部聯結）之標準文法的 *escape 序列* ，這些功能未涵蓋在 SQL-92 文法中。 如需詳細資訊，請參閱本節稍後的「附錄 C： SQL 文法」和「 [Escape 序列](../../../odbc/reference/develop-app/escape-sequences.md)」中的[ODBC Escape 序列](../../../odbc/reference/appendixes/odbc-escape-sequences.md)。  
  
 所選擇的文法會影響驅動程式處理語句的方式。 驅動程式必須將 SQL-92 SQL 和 ODBC 定義的 escape 序列修改為 DBMS 特定的 SQL。 因為大部分的 SQL 文法都是根據一或多個不同的標準，所以大部分的驅動程式幾乎不需要任何工作就能滿足這項需求。 它通常只包含搜尋 ODBC 所定義的 escape 序列，並以 DBMS 特定文法來取代。 當驅動程式發現文法無法辨識時，它會假設文法是 DBMS 特定的，而且不會修改資料來源來執行 SQL 語句。  
  
 因此，有兩個要使用的文法選項： SQL-92 文法 (和 ODBC escape 序列) 和 DBMS 特定的文法。 在這兩種情況下，只有 SQL-92 文法可以互通，因此所有互通的應用程式都應該使用它。 無法互通的應用程式可以使用 SQL-92 文法或 DBMS 特定的文法。 DBMS 專屬的文法有兩個優點：它們可以利用 SQL-92 所未涵蓋的任何功能，而且它們的執行速度會更快，因為驅動程式不需要修改它們。 您可以藉由設定 SQL_ATTR_NOSCAN 語句屬性來部分強制執行第二個功能，這會阻止驅動程式搜尋和取代 escape 序列。  
  
 如果使用的是 SQL 92 文法，應用程式可以藉由呼叫 **SQLNativeSql**，來探索驅動程式如何修改它。 這在對應用程式進行偵錯工具時通常很有用。 **SQLNativeSql** 會接受 SQL 語句，並在驅動程式修改之後將它傳回。 因為此函式是在核心介面一致性層級中，所以所有驅動程式都支援此功能。
