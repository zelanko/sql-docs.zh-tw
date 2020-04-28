---
title: 靜態 SQL |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- static SQL [ODBC]
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- SQL statements [ODBC], static SQL
- embedded SQL [ODBC]
- SQL [ODBC], static SQL
ms.assetid: 667d92ec-fed9-4028-81d4-bb9ba867356a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55710d8ea734cba86ae5e4daa725f75e94e65a64
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81279900"
---
# <a name="static-sql"></a>靜態 SQL
[內嵌 Sql 範例](../../odbc/reference/embedded-sql-example.md)中所示的內嵌 sql 稱為靜態 SQL。 因為程式中的 SQL 語句是靜態的，所以稱為靜態 SQL;也就是說，它們不會在每次執行程式時變更。 如上一節所述，編譯器的其餘部分時，會編譯這些語句。  
  
 靜態 SQL 在許多情況下都能順利運作，而且可以用於任何可在程式設計時間判斷資料存取的應用程式中。 例如，訂單輸入程式一律會使用相同的語句來插入新訂單，而航空公司保留系統一律會使用相同的語句，將基座的狀態從 [可用] 變更為 [保留]。 這些語句都會透過使用主機變數來一般化;不同的值可以插入銷售訂單中，而且可以保留不同的基座。 因為這類語句可以在程式中硬式編碼，所以這類程式的優點是必須在編譯時期剖析、驗證和優化語句一次。 這會產生相對較快速的程式碼。
